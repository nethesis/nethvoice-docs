
.. _provisioning-phone2-section:

=========================
Provisioning dei telefoni
=========================

.. hint::
    
    Fare riferimento a :ref:`provisioning-migration-section` e a
    :ref:`provisioning-section` per la versione precedente.


Cosa significa **Provisioning**? Provisioning è configurare i telefoni in
modalità automatica limitando al massimo le operazioni necessarie.



Configurazione di |product|
===========================

Operazioni da compiere su |product|:

#. Identificazione dei telefoni

#. Associazione dei telefoni agli utenti


Identificazione dei telefoni
----------------------------

L'indirizzo MAC è alla base del **Provisioning** di |product| in quanto
identifica il telefono in maniera univoca.

L'inserimento dell'indirizzo MAC dei telefoni non richiede il collegamento
del telefono alla rete. È infatti possibile inserire i MAC
address di telefoni ancora imballati.

In ogni caso l'inserimento degli indirizzi MAC dei telefoni può avvenire con
le seguenti modalità:

* Digitare o copiare l'indirizzo MAC da un foglio di
  calcolo, fattura o altro documento

* Scansionare le reti locali alla ricerca di apparati telefonici
  supportati, già accesi e collegati in rete

* Scansionare il codice a barre dell'indirizzo MAC del telefono tramite app
  per smartphone "Scan & Play"
 

Associazione dei telefoni agli utenti
-------------------------------------

La configurazione di un telefono è completa quando questo viene associato ad un
utente.

Ad ogni utente possono essere associati al massimo 8 dispositivi telefonici.

|product| assegna ad ogni dispositivo associato all'utente una numerazione
progressiva con il criterio seguente:

* ``Interno Principale`` - telefono principale, per esempio ``201``

* ``91+Interno Principale`` - telefono 2, per esempio ``91201``

* ``92+Interno Principale`` - telefono 3, per esempio ``92201``

* ...

Tuttavia dal punto di vista degli utenti, l'Interno Principale è l'unico numero
importante da ricordare.



Azioni da compiere sui telefoni
===============================

.. note::

    Consideriamo al **primo avvio** i telefoni nuovi, appena tolti dalla
    scatola, o che hanno subito il ripristino dei valori di fabbrica e non sono
    mai stati avviati.


I telefoni al **primo avvio** sono già in grado di raggiungere |product| per
ottenere la propria configurazione secondo i metodi supportati.

L'unica azione da compiere in questi casi è collegare il cavo Ethernet con PoE
(Power over Ethernet) al telefono. Qualora PoE non fosse disponibile sarà
necessario collegare anche il cavo di alimentazione del telefono.

.. warning::

    Verificare la compatibilità dei telefoni con i metodi di provisioning
    supportati. Leggere attentamente le sezioni seguenti

Nel caso un telefono sia già usato è possibile predisporlo all'associazione con
|product| tramite le procedure di **aggiornamento del firmware** e di
**ripristino dei valori di fabbrica**. Entrambe le procedure sono disponibili
tramite l'interfaccia web di amministrazione del telefono.

.. _provisioning-methods:

Metodi di provisioning
======================

I telefoni possono accedere alla propria configurazione mediante i protocolli
standard del web, HTTP o HTTPS (porta TCP 80 o 443).

Quando il MAC address del telefono è inserito in |product| viene generato un
URL (indirizzo) di provisioning. Per esempio: ::

    https://mio.centralino.cloud/provisioning/1234567890.1234/{mac}.cfg

Questo URL contiene un segreto (``1234567890.1234`` nell'esempio) che autentica
ed identifica il dispositivo che ne farà uso.

Per ottenere l'URL di provisioning il telefono al primo avvio
può utilizzare due metodi, **RPS** e **DHCP**. 

Il metodo **RPS** (Redirect & Provisioning Service) prevede l'inserimento dell'URL
di provisioning nel sito web del produttore del telefono. |product| è in grado
di effettuare questo inserimento automaticamente. Appena acceso il telefono
al primo avvio cerca di contattare il sito del produttore per ottenere l'URL di
provisioning.

Il metodo **DHCP** si basa sulla configurazione di OPTION 66 del protocollo
DHCP (Dynamic Host Configuration Protocol) in maniera specifica per ogni marca
di telefono. Se |product| svolge il ruolo di DHCP server della rete a cui sono
collegati i telefoni le impostazioni necessarie per raggiungere l'URL di
provisioning sono già configurate. In caso contrario e qualora **RPS** non sia
utilizzabile è necessario configurare il server DHCP di rete in maniera
opportuna.

Nel caso né RPS né DHCP funzionino è possibile accedere all'interfaccia web di
amministrazione del telefono ed immettere l'URL di provisioning manualmente. 
Ricordarsi di disattivare le altre modalità di provisioning, come DHCP e PNP.

L'URL di provisioning è visualizzato nell'interfaccia di amministrazione di
|product| per ogni telefono, tramite il pulsante :guilabel:`Info` alla pagina
:guilabel:`Dispositivi > Telefoni`.

In ogni caso, una volta ottenuto l'URL di provisioning, il telefono utilizza
sempre questo per accedere alla propria configurazione su |product|.

.. warning::

    Fare riferimento alla sezione :ref:`provisioning-support-section` per
    ulteriori informazioni sul supporto dei produttori a RPS e DHCP

Specifiche della configurazione dei telefoni
============================================

Se si vuole modificare o personalizzare le impostazioni di telefoni configurati
tramite il provisioning, accedere all'interfaccia web di amministrazione di
|product|, modificando le impostazioni a livello di *Default*, *Modello* o di 
*singolo telefono*.

I parametri modificabili comprendono:

* Lingua                                                         
* Fuso orario
* Formato data/ora                                        
* Toni
* Password utente admin                              
* Avviso di chiamata
* Suoneria                                                     
* Modalità di trasferimento
* Rubrica LDAP                                             
* VLAN
* Soft keys (Tasti del telefono sotto lo schermo)                                                    
* Line keys (Tasti linea)
* Exp keys  (Tasti linea dei moduli di espansione)
* Screen Saver e Sfondo

Fare riferimento a :ref:`wizard2-section` per maggiori informazioni.

.. warning:: 

   Non cambiare le impostazioni dall'interfaccia di amministrazione del
   telefono.

Ad ogni riavvio il telefono riprende le configurazioni dall'URL provisioning.
Eventuali modifiche eseguite dall'interfaccia di amministrazione del telefono
andranno perse.

Nelle sezioni successive sono descritte alcune impostazioni fornite da |product|.


Password di admin
-----------------

L'interfaccia web di amministrazione del telefono è accessibile con nome utente
``admin`` e password generata casualmente durante l'installazione di |product|.

La password è disponibile nell'interfaccia di amministrazione di |product|, alla
pagina :guilabel:`Modelli > Impostazioni di default`.


.. _provisioning2-aggiornamenti-automatici:

Aggiornamenti automatici
------------------------

Il telefono contatta automaticamente tutte le notti |product| per aggiornare la
propria configurazione. È possibile disabilitare del tutto l'aggiornamento
automatico.

In ogni caso il telefono scarica la configurazione tutte le volte che viene
riavviato.

.. _provisioning2-firmware-upgrade:

Aggiornamento firmware
----------------------

Il costruttore del telefono pubblica periodicamente nel proprio sito
web gli aggiornamenti al firmware per i vari modelli dei propri telefoni.

È possibile distribuire il firmware aggiornato a tutti i telefoni di
uno stesso modello oppure ad un singolo telefono. Il file del firmware
ottenuto dal sito del costruttore va caricato tramite l'interfaccia
di amministrazione di |product| rispettivamente in
:guilabel:`Modelli > Preferenze > Firmware` oppure in
:guilabel:`Configurazione > Dispositivi associati > Modifica >
Preferenze`.

Il nome del file può contenere solo lettere, numeri e i simboli ``._-()``.

I telefoni recepiscono l'aggiornamento secondo i tempi indicati
in :ref:`provisioning2-aggiornamenti-automatici`.

.. hint::

    Quando i telefoni hanno recepito l'aggiornamento, deselezionare
    il file del firmware nell'interfaccia di |product| per ridurre
    il traffico di rete.

Elenco delle pagine web per il download del firmware:

- `Yealink <http://support.yealink.com/documentFront/forwardToDocumentFrontDisplayPage>`_
- `Snom <https://service.snom.com/display/wiki/Firmware+Update+Center>`_
- `Fanvil <https://fanvil.com/Support/download.html>`_
- `Gigaset <https://teamwork.gigaset.com/gigawiki/pages/viewpage.action?pageId=37486876>`_
- `Sangoma <https://wiki.sangoma.com/display/PHON/Phone+Firmware+Release+Notes>`_


Telefoni supportati
===================


Fanvil
------

**Versione FIRMWARE 2.0 o superiore**

* X210
* X3, X3S, X3SP, X3G, X3SG, X3U
* X4, X4G, X4SG, X4U
* X5S, X5U
* X6, X6U


Yealink 
-------

**Versione FIRMWARE 0.84 o superiore**

* T19(P) E2, T21(P) E2, T23P/G, T27P/G, T29G
* T30/P, T31/P/G, T33P/G
* T40P/G, T41P/S/U, T42G/S/U, T43U, T46G/S/U, T48G/S/U, T49G
* T52S, T53/W, T54S/W, T56A, T57W, T58V/A, VP59

Snom 
----

**Versione FIRMWARE 8.7.5 o superiore**

* D120
* D305, D315, D345, D375, D385
* D710, D712, D715, D717, D725, D735, D745, D765, D785

Gigaset
-------

**Versione FIRMWARE 3.15.9 o superiore**

* Maxwell Basic, Maxwell 2, Maxwell 3, Maxwell 4
   
Sangoma
-------

**Versione FIRMWARE X.0.4.67 o superiore**

* S205, S206
* S300, S305
* S400, S405, S406 
* S500, S505
* S700, S705

.. _provisioning-support-section:

Compatibilità provisioning
==========================

La seguente tabella risassume i metodi di provisioning utilizzati da ogni
produttore al primo avvio del telefono.

.. list-table:: Metodi di provisioning per produttore
    :widths: 5 5 5 5 10
    :header-rows: 1

    * - Produttore
      - Metodo primario
      - Metodo secondario
      - DHCP option
      - DHCP option value
    * - Fanvil
      - RPS
      - DHCP
      - 66
      - ``http://IP_CENTRALINO/provisioning/$mac.cfg``
    * - Yealink
      - RPS
      - DHCP
      - 66
      - ``http://IP_CENTRALINO/provisioning/$MAC.cfg``
    * - Snom
      - RPS
      - DHCP
      - 66 e 67
      - ``http://IP_CENTRALINO`` e ``provisioning/{mac}.xml``
    * - Gigaset
      - DHCP [#f1]_
      - RPS
      - 114
      - ``http://IP_CENTRALINO/provisioning/%MACD.xml``
    * - Sangoma
      - RPS [#f2]_
      - DHCP
      - 66
      - ``http://IP_CENTRALINO/provisioning``

.. [#f1] Per i telefoni Gigaset assicurarsi che il server DHCP di rete, se 
         diverso da |product|, non fornisca OPTION 66

.. [#f2] Il servizio RPS di Sangoma non consente l'inserimento dell'URL di 
         provisioning da |product|. Inserire l'URL di provisioning manualmente 
         tramite il portale di Sangoma, o utilizzare il metodo DHCP.
