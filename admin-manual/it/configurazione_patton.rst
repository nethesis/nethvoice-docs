=====================
Configurazione Patton
=====================

Introduzione
============

Come descritto ampliamente nel documento :doc:`Hardware <hardware>`, viene suggerito e supportato l'utilizzo di gateway esterni da integrare con il |product|. In questo documento verranno descritte la procedura di configurazione dei Patton e la configurazione in |product|.

.. note::   I Patton dalla versione '''6''' del proprio '''firmware''' supportano la configurazione tramite provisioning vedi anche :doc:`qui <wizard_provisioning>`

Creazione file di configurazione
================================

|product| introduce il modulo **Configurazione Patton** che semplifica notevolmente la configurazione di questi apparati.

Per creare il file di configurazione, procedere così:

-  Aprire la pagina **Configurazione Patton** e scegliere il modello del proprio **Patton**

    Il modello è individuabile dal codice che si trova collegandosi all'interfaccia web del Patton vedi la seconda immagine sotto.

.. image:: ../_static/patton.png
            :alt: Configurazione Patton
.. image:: ../_static/patton_01.png
            :alt: Configurazione Patton

.. note::   Nel caso non sia in elenco il proprio modello di Patton, utilizzarne un'altro con le stesse funzionalità e comunicare al supporto la mancanza

-  Specificare un nome per la configurazione, l'indirizzo IP del Patton, il gateway della rete e il mac address se si vuole utilizzare il provisioning per configurare il **Patton**

-  Per le porte **fxs** scegliere l'interno SIP collegato alla porta specificata. L'interno SIP deve essere precedentemente creato nell'apposita sezione.


-  Per le porte **fxo** scegliere il numero di telefono associato al numero di fascio autogenerato. L'interfaccia segnala a quale fascio sip verrà abbinata ogni porta, i fasci vengono automaticamente creati e sono disponibili nella sezione :doc:`Fasci <fasci_sip>`.

-  Per le porte **isdn** scegliere la tipologia delle porte, o punto-punto o punto-multipunto. L'interfaccia segnala a quale fascio sip verrà abbinata ogni porta, i fasci vengono automaticamente creati e sono disponibili nella sezione :doc:`Fasci <fasci_sip>`.

-  Per le porte **pri** l'interfaccia segnala a quale fascio sip verrà abbinata ogni porta, i fasci vengono automaticamente creati e sono disponibili nella sezione :doc:`Fasci <fasci_sip>`.

-  Dopo aver cliccato su Salva il modulo propone il link per scaricare la configurazione del Patton a seconda del firmware.
   Se è stato indicato il mac address è possibile applicare la configurazione tramite il provisioning.

Configurazione Patton
=====================

Gli apparati Patton vengono configurati attraverso un file di configurazione pre-formattato che va importato attraverso l'interfaccia web di amministrazione.

-  Collegare il Patton alla propria rete LAN, inserendo il cavo di rete nell'interfaccia WAN dello stesso.
-  Il Patton di default richiede un ip in DHCP, controllare dai log di NethService o NethSecurity qual'è IP che gli è stato assegnato.
-  Collegarsi all'interfaccia web, inserendo tale IP nel browser (username/password di default sono `administrator` e password vuota)
-  Spostarsi nel pannello `Import/Export` -> Import Configuration -> Selezionare il File di Configurazione (vedi paragrafo successivo)
-  Fare il Reload del Patton (**non cliccare su Saving Configuration**)
-  Al Reload assicurarsi che il Patton abbia assunto l'IP corretto (da file di configurazione), inserendo il nuovo IP nel browser
-  Salvare la configurazione con il pannello `Save`

