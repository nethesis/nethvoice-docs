======================
HA (High Availability)
======================

|product| supporta una configurazione in HA limitata ad alcuni scenari specifici.

Il cluster è composto da due nodi in modalità active-passive:
il nodo master (o nodo primario) fornisce il servizio, mentre il nodo slave (o nodo secondario) entra in gioco in caso
di fallimento del nodo master.
Entrambi i nodi condividono uno storage DRBD in modalità active-passive.

Questa configurazione supporta:

* Un IP virtuale collegati sulla rete green
* Servizi clusterizzati che salvano i dati sullo storage condiviso:

  * MySQL
  * Asterisk
  * NethCTI server


Inoltre, al fine di ridurre la complessità del sistema in alta affidabilità si tenga conto delle seguenti limitazioni.

* Gli aggiornamenti automatici sono disabilitati
* E' necessario configurare un server LDAP/Active Directory esterno per l'autenticazione.
* E' necessario configurare un server Jabber esterno per l'integrazione della chat nel CTI
* La rubrica centralizzata non può essere pubblicata su LDAP
* Non è disponibile il gruppo *voicemangers*: l'accesso ai report e alle pagine di configurazione deve
  essere effettuato obbligatoriamente usando l'utente *admin* la cui password è sincronizzata con quella
  dell'utente *root*
* E' necessario configurare un server DHCP esterno, e configurarlo affinchè i telefoni utilizzino
  come server TFTP l'IP virtuale del cluster

Il demone di monitoraggio (ARDAD) controlla periodicamente lo stato dei servizi.
Dal momento che alcuni servizi (es. asterisk, MySQL) sono in esecuzione solo sul nodo primario,
il demone potrebbe generare degli allarmi sul nodo secondario.
Questi allarmi possono essere silenziati dal Centro Servizi, all'interno del quale
ogni nodo del cluster ha la propria chiave di registrazione (LK).

Requisiti hardware
==================

La procedura prevede l'installazione su due nodi gemelli. Ogni nodo dovrà avere

* un disco o una partizione dedicata allo storage condiviso DRBD (Distributed Replicated Block Device)
* due interfacce di rete per creare un bond con ruolo *green*, entrambe le interfacce
  devono essere collegate agli switch della rete locale

E' necessario possedere due switch all'interno della LAN, per esempio SW1 e SW2.
Creare un bond su ciascun nodo usando due interfacce di rete. 
Ogni nodo deve essere collegato ad entrambi gli switch SW1 e SW2.


Fence device
------------

Ogni nodo dovrà essere collegato ad almeno un fence device già correttamente configurato.

Con il termine *fencing* si intende la disconnessione di un nodo dallo storage condiviso.
Il *fence device* è il dispositivo hardware che consente tale disconnessione usando
il metodo STONITH (Shoot The Other Node In The Head), ovvero togliendo l'alimentazione al nodo guasto.

Molti server possiedono un'interfaccia di gestione preinstallata conosciuta con vari nomi commerciali come
ILO (HP), DRAC (Dell) o BMC (IBM). Tutte queste interfacce rispettano lo standard IPMI e possono
essere utilizzate come dispositivi di fence.

Collegamenti esterni:

* lista dei dispositivi supportati: https://access.redhat.com/articles/28603
* maggiori informazioni sul fencing: http://clusterlabs.org/doc/crm_fencing.html

.. note::
   In questa guida sono riportati solo i comandi per gestire fence device di tipo IPMI.

Installazione
=============

Prima di iniziare:

* collegare i due nodi come previsto e assicurarsi che il nodo secondario sia spento
* assicurarsi che il nome host del nodo primario sia *ns1*. Esempio: ns1.mydomain.com. 
  Scegliere ora anche il dominio, che *non* potrà essere cambiato in seguito

Nodo primario
-------------

Le opzioni del cluster sono salvate all'interno della chiave di configurazione *ha* che deve essere
configurata specularmente su entrambi i nodi.

Eseguire i passi di configurazione come riportati di seguito.

* Configurare il bond sulle interfacce green.

* Configurare l'IP virtuale, ed informare il cluster sugli IP green di entrambi i nodi:

::

 config setprop ha VirtualIP <GREEN_IP_HA>
 config setprop ha NS1 <NS1_GREEN_IP>
 config setprop ha NS2 <NS2_GREEN_IP>


* Applicare le modifiche e avviare i servizi sul nodo primario: 

::

 signal-event nethserver-ha-save


Al termine della configurazione, il nodo primario è pronto ad erogare i servizi.
Per verificare lo stato del cluster, eseguire: ::

 pcs status


Nodo secondario
---------------

* Assicurarsi che l'hostname del nodo secondario sia *ns2* e che il dominio sia lo stesso del nodo primario
* Configurare l'IP virtuale, le opzioni NS1 e NS2, quindi applicare la configurazione:

  ::
 
   signal-event nethserver-ha-save


Passi finali
------------

* Abilitare lo STONITH, digitando su uno qualsiasi dei nodi il seguente comando: 

::

 pcs property set stonith-enabled=true

* Configurare i fence device, i comandi possono essere eseguiti su uno qualsiasi dei nodi.

  Esempio con nome dominio ``nethserver.org``:

  ::
 
    pcs stonith create ns2Stonith fence_ipmilan pcmk_host_list="ns2.nethserver.org" ipaddr="ns2-ipmi.nethserver.org" login=ADMIN passwd=ADMIN timeout=4 power_timeout=4 power_wait=4 stonith-timeout=4 lanplus=1 op monitor interval=60s
    pcs stonith create ns1Stonith fence_ipmilan pcmk_host_list="ns1.nethserver.org" ipaddr="ns1-ipmi.nethserver.org" login=ADMIN passwd=ADMIN timeout=4 power_timeout=4 power_wait=4 stonith-timeout=4 lanplus=1 op monitor interval=60s

  Dove ns1-ipmi.nethserver.org e ns2-ipmi.nethserver.org sono i nomi host associati agli IP delle interfacce di gestione.

  Inoltre, assicurarsi che la risorsa stonith risieda sul nodo corretto:

  ::

    pcs constraint location ns2Stonith prefers ns1.nethserver.org=INFINITY
    pcs constraint location ns1Stonith prefers ns2.nethserver.org=INFINITY

* Configurare un indirizzo mail a cui inviare le notifiche in caso di guasto:

::

  pcs resource create MailNotify ocf:heartbeat:MailTo params email="admin@nethserver.org" subject="Cluster notification"

* E' fortemente consigliato cambiare la password di root da interfaccia web su entrambi i nodi. 
  La password di root è infatti utilizzata per impartire ordini ai nodi del cluster.


Guasti e ripristino
===================

Un cluster a due nodi può tollerare solo un guasto alla volta.

.. note::
   Utilizzando i dispositivi di fence di tipo IPMI, il cluster non è in grado di gestire 
   la perdita di alimentazione di un nodo, in quanto il dispositivo di fence è alimentato dal nodo stesso.

   In questo caso è necessario confermare manualmente lo spegnimento del nodo eseguendo questo comando: ::

     pcs stonith confirm <failed_node_name>

Nodi guasti
-----------

Quando un nodo non risponde all'heartbeat, il nodo viene escluso dal cluster.
Tutti i servizi clusterizzati sono disabilitati al boot per evitare problemi in caso di fencing:
un nodo che è stato spento da un evento di fencing, necessita probabilmente di manutenzione prima di rientrare 
nel cluster.

Per inserire nuovamente il nodo nel cluster, eseguire: ::

 pcs cluster start


Fence device irraggiungibili
----------------------------

Il cluster controlla periodicamente lo stato dei dispositivi di fence configurati.
Se un dispositivo non è raggiungibile, verrà considerato in stato fermo (stopped).

Dopo aver ripristinato il dispositivo di fence, informare il cluster sullo stato
di ciascun dispositivo con il seguente comando: ::

  crm_resource --resource <stonith_name> --cleanup --node <node_name>

Disaster recovery
-----------------

In caso di guasto hardware, è possibile reinstallare il nodo è raggiungerlo al cluster.
I servizi clusterizzati saranno automaticamente configurati e i dati verranno sincronizzati fra i nodi.

Seguire questi passi.

1. Ripristinare il backup della configurazione del nodo. Se non si possiede il backup della configurazione,
   riconfigurare il server e assicurarsi di installare il pacchetto ``nethserver-ha``.
2. Eseguire l'evento per unire il nodo al cluster: ::

     signal-event nethserver-ha-save


Backup
======

Il backup deve essere configurato su entrambi i nodi ed eseguito su una condivisione di rete.
Solo il nodo primario effettuerà realmente il backup, il backup del nodo secondario
verrà automaticamente abilitato qualora il nodo primario sia guasto.

In caso di guasto di entrambi i nodi, reinstallare il nodo primario,
ripristinare il backup della configurazione e avviare il cluster: ::

 signal-event nethserver-ha-save

Infine ripristinare il backup dei date e, al termine, riavviare il sistema.

