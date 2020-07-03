=====================
Migrazione a Tancredi
=====================

È disponibile una procedura a riga di comando per migrare la 
configurazione dei telefoni di |product| dal sistema basato su 
Endpoint Manager di FreePBX a quello basato sul progetto Open Source Tancredi.

La procedura converte e importa nel database di Tancredi 
alcune delle configurazioni già presenti in quello di FreePBX.

Verranno importati:

* I telefoni supportati (MAC address) importati con la funzione
  Scansione rete di |product| e l'informazione sul modello ad essi associato

* Le credenziali SIP del telefono e l'associazione con l'interno/utente

Non sono importate invece le impostazioni quali tasti programmabili, 
template personalizzati e altre funzioni specifiche del telefono,
che possono essere rapidamente inserite dalla nuova interfaccia di
amministrazione di |product|. Fare per questo riferimento alla
:ref:`wizard2-provisioning-section`.

Precondizioni
=============

1.  La procedura è pensata per essere eseguita in un |product| con gli
    ultimi aggiornamenti installati, con attivo il sistema di provisioning
    basato su Endpoint Manager di FreePBX.

2.  Eseguire un backup completo del sistema
    prima di eseguire la migrazione.

3.  Aggiornare la versione del firmware dei telefoni all'ultima disponibile

Procedura di migrazione
=======================

1.  Eseguire il seguente comando da una shell di root ::

        tancredi-migration-helper

    Prestare attenzione ai messaggi generati dallo script e ad eventuali errori.
    I messaggi vengono scritti oltre che sul terminale anche in :file:`/var/log/tancredi/tancredi.log`.

    Per evitare perdite di dati lo script può essere lanciato una sola volta.
    Tuttavia aggiungendo l'argomento ``-f`` (force) ogni dato esistente nel DB
    di Tancredi viene eliminato e l'importazione da FreePBX eseguita nuovamente.

2.  Accedere all'interfaccia di amministrazione di |product| e verificare

    * il modello assegnato ad ogni dispositivo alla pagina
      :ref:`Telefoni <wizard2-telefoni>`,

    * le impostazioni di default e dei singoli modelli alla pagina 
      :ref:`Modelli <wizard2-modelli>`,

    * l'associazione degli utenti/interni con i dispositivi 
      alla pagina :ref:`Configurazioni <wizard2-configurazioni>`.

3.  Se in rete il server DHCP non è |product| assicurarsi che la sua configurazione
    è :ref:`compatibile con il provisioning dei telefoni <provisioning-support-section>`.

4.  Eseguire la procedura di *factory default* su ogni telefono

Problemi noti
=============

I seguenti messaggi possono comparire in :file:`/var/log/tancredi/tancredi.log` ::

Error adding 0C-38-3E-XX-XX-XX phone to RPS
-------------------------------------------

Quando un telefono viene aggiunto al DB di Tancredi il suo
URL di provisioning viene registrato nel servizio cloud di reindirizzamento
e provisioning (RPS). Questa chiamata remota potrebbe fallire 
per diversi motivi, tra cui

* la rete non è configurata correttamente

* il cloud non è raggiungibile

Il log di Tancredi riporta anche un comando *curl* con cui è possibile
ripetere la richiesta HTTP fallita ed ottenere ulteriori informazioni.


Ripristino della configurazione iniziale basata su Endpoint Manager
===================================================================

La procedura non altera il database di FreePBX. L'unica modifica è
la disabilitazione del servizio TFTP, utilizzato dai telefoni per
il provisioning con FreePBX.  È quindi possibile tornare indietro
alla situazione precedente alla migrazione,
almeno finché non si è applicato il *factory default* ai telefoni.

In questo caso il comando è ::

  tancredi-migration-helper -d

Quale sistema di provisioning è attivo?
=======================================

Per verificare il sistema di provisioning configurato
su |product| eseguire il seguente comando ::

  config getprop nethvoice ProvisioningEngine

Help in linea
=============

Con l'argomento -h (help) lo script stampa il riepilogo delle funzioni disponibili

.. code-block:: text

    # tancredi-migration-helper -h
    Usage: /usr/sbin/tancredi-migration-helper [-h|-f|-d]
    Import known devices in the Tancredi database, 
    then disable the TFTP service for FreePBX provisoning
    With no option, the procedure runs once. Accepted options
    -h     This help
    -f     Drop the Tancredi DB and import known devices from FreePBX again
    -d     Restore TFTP configuration for FreePBX provisioning

