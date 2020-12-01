==========
App mobile
==========


.. _nethcti_mobile:

|product_cti|
=============

L'applicazione mobile del |product_cti| è disponibile per iOS e Android ed è scaricabile dai rispettivi App Store.

I requisiti per utillizzare l'app sono:

- certificato valido installato sul |product|
- indirizzo FQDN del |product| raggiungibile e utilizzato nella configurazione dell'app (manualmente o nel |product_cti|)
- protocollo SIP TLS raggiungibile
- porta HTTPS raggiungibile

.. note:: In alternativa al FQDN del |product| è possibile usare un nome host e dominio configurato come alias per il server con gli stessi requisiti.
   Per usarlo al posto del FQDN utilizzare questi comandi sostituendo ad ALIAS il nome host seguito dal dominio (ad esempio host.dominio.com): ::

        config setprop nethvoice PublicHost ALIAS
        expand-template /etc/asterisk/nethcti_push_configuration.json
        expand-template /etc/nethcti/nethcti.json
        systemctl reload nethcti-server

L'app accede in SIP TLS al |product| che va abilitato sia lato firewall che nella configurazione di |product|.

Per prima cosa, sul Server Manager (porta 980), nella sezione :menuselection:`Accesso Centralino -> Accesso Esterno` abilitare il servizio SIP TLS.

Fatto questo, accedere all'interfaccia avanzata di |product|, andare in :menuselection:`Impostazioni  -> Impostazioni Asterisk SIP`:

- aprire il tab :guilabel:`Impostazioni Generali` ed impostare la sezione :guilabel:`Impostazioni NAT`.

- aprire il tab :guilabel:`Impostazioni PJSIP` e configurare la sezione :guilabel:`Impostazioni TLS/SSL/SRTP` come segue:

   * :guilabel:`Certificate Manager -> NethServer`
   * :guilabel:`SSL Method -> Default` 
   * :guilabel:`Verify Client -> No`
   * :guilabel:`Verify Server -> No`


Fatto questo, fare clic su Salva in fondo alla pagina.

A questo punto, fare clic sul pulsante arancione Applica Cambiamenti in alto a destra, e da ultimo riavviare Asterisk con il comando: ::

  asterisk -rx "core restart now"

Porte su cui è necessario raggiungere |product| per un utilizzo da remoto:

- 5061 TCP (SIP TLS)
- da 10000 a 20000 UDP (Audio)

Configurazione
--------------

Per configurare l'applicazione è necessario abilitare il campo :guilabel:`Mobile App` relativo all'utente desiderato nella pagina Configurationi del |product|.

Automaticamente verrà creato un nuovo interno SIP per l'utente selezionato necessario al funzionamento dell'applicazione.

Sarà poi sufficiente eseguire il login nell'applicazione e automaticamente verrà configurata utilizzando l'interno SIP a lei dedicato.

Per eseguire il login nell'applicazione sarà necessario dal menù di sinistra selezionare la voce :guilabel:`Login` per accedere alla sezione dalla quale eseguire l'azione necessaria.

Dalla sezione :guilabel:`Login` dell'applicazione è possibile accede in due modi:

- Inserendo l'indirizzo FQDN(o l'alias configurato come specificato sopra) del server e le credenziali nome utente e password dell'utente
- Scansionando il QRCode dalla sezione :guilabel:`dispositivi` nelle Impostazioni dell'interfaccia web del |product_cti| cliccando su genera QRcode nella card relativa alla App Mobile

L'applicazione mobile |product_cti| eseguirà l'autenticazione sul server nethcti e sarà quindi possibile consultare il log nethcti in caso di errore.

Una volta eseguito l'accesso l'applicazione riceverà le chiamate in arrivo anche durante il funzionamento in background e sarà possibile eseguire chiamate in uscita.

Nel caso in cui il comportamento dell'applicazione all'arrivo di una chiamata non sia come desiderato sarà possibile gestirlo dalle impostazioni avanzate del telefono relative all'applicazione |product_cti|.


.. _wave_mobile:

Wave
====

L'applicazione Wave integra un interno sui dispositivi mobili ed è installabile su base Android o iOS.

Come l'app del |product_cti| anche Wave accede in SIP TLS al |product| di conseguenza per permettere il corretto funzionamento dell'applicazione è necessario seguire i passi iniziali indicati nella sezione superiore per l'applicazione mobile del |product_cti|.

Una volta adattata la configurazione lato Server Manager e interfaccia avanzata è necessario configurare l'applicazione Wave in modo da garantire il corretto funzionamento del provisioning sul |product|.


Configurazione
--------------

.. note:: La configurazione tramite provisioning è possibile solo utilizzando la precedente versione, fare riferimento a
          :ref:`provisioning-section` e a :ref:`provisioning-migration-section`. 

É possibile configurare l'applicazione tramite il provisioning di |product|.

Per prima cosa collegare lo smartphone alla rete locale del |product| e andare in :guilabel:`Impostazioni -> Provisioning Settings`.

Impostare:

- Config Upgrade Via: TFTP
- Config percorso server : ip locale di |product|

Cliccare su Start Provisioning.

Questa operazione permetterà di aggiungere il Mac-Address dello smartphone a quelli dei device configurabili.

É utile conoscere il MAC Address dello smartphone che si vuole configurare, è possibile verificarlo nel momento della richiesta TFTP in /var/log/messages: ::

    Jan 10 15:26:44 nethvoice dnsmasq-tftp[16179]: file /var/lib/tftpboot/cfgDC0B34CED538.xml not found

il MAC Address dello smartphone in questo caso è DC:0B:34:CE:D5:38

Aprire il wizard di |product|, andare sulla pagina :menuselection:`Dispositivi` ed effettuare una nuova scansione, sarà presente una riga con "CTI App" come marca e GS Wave come modello.

Nella sezione :menuselection:`Utenti -> Configurazioni` del wizard associare il device all'utente voluto e cliccare su Configura e riavvia per pubblicare la configurazione.

Forzare il provisioning di nuovo con la procedura precedente per configurare l'applicazione: :menuselection:`Impostazioni -> Provisioning Settings -> Start Provisioning`

.. note:: Per consentire l'accesso da remoto alla rubrica di |product| ricordarsi di abilitare l'accesso da reti esterne alla rubrica centralizzata in |parent_product|


BLF
...

Per configurare i BLF e monitorare altri interni di |product| seguire questa procedura:

- In :guilabel:`Contatti -> SIP` creare i contatti necessari specificando il Nome, Cognome e l'interno SIP
- In :guilabel:`Impostazioni -> Impostazioni Avanzate -> Impostazioni Aggiuntive` attivare i BLF
- In :guilabel:`Impostazioni -> Impostazioni Avanzate -> Impostazioni Aggiuntive -> Elenco BLF` selezionare i contatti da utilizzare come BLF

I BLF verranno mostrati in Contatti -> SIP


Scan&Play
=========

.. _app_mobile:

L'applicazione Scan&Play è disponibile su smartphone e permette di scansionare i MAC address dei telefoni per velocizzare la configurazione e il provisioning.

.. note:: E' possibile usare l'app Scan & Play solo con la precedente versione, fare riferimento a
          :ref:`provisioning-section` e a :ref:`provisioning-migration-section`. 

Requisiti
---------

- Presenza di un certificato valido sul server
- Raggiungibilità della porta HTTPS 443 dall'esterno

Installazione
-------------

L'applicazione è disponibile ai seguenti link:

- Android: https://play.google.com/store/apps/details?id=it.nethesis.scanplay14
- iOS: https://itunes.apple.com/us/app/nethvoice-scan-play-14/id1277558637?ls=1&mt=8

É possibile comunque cercare la parola **macscan** nei diversi store e installarla senza il link diretto.

Utilizzo
--------

Appena avviata l'applicazione vi chiede le infomazioni di login:

- Username: l'username dell'utente amministratore del centralino con cui collegarsi (che è `admin`)
- Password: la password dell'utente admin con cui collegarsi
- Hostname: il nome o l'indirizzo IP del server (server in cui è installato il centralino)

Una volta effettuato il login:

- Premere il pulsante "Scan" per avviare la fotocamera dello smartphone
- Avvicinarsi al MAC address del telefono o della scatola del telefono
- L'applicazione riconosce il MAC address e ricava il fornitore del telefono
- Selezionare il modello di telefono
- Selezionare l'utente del centralino a cui associare il telefono
- Premere il pulsante "Salva" per salvare la configurazione

Collegare il telefono nella stessa rete del centralino e verificare che venga effettuato correttamente il provisioning del telefono.
