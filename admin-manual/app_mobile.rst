==========
App mobile
==========

.. _wave_mobile:

Wave
====

L'applicazione Wave integra un interno sui dispositivi mobile, è installabile su base Android o iOS.


.. note:: Ricordarsi di rendere accessibile da internet il |product| tramite il protocollo SIP TLS per un utilizzo da remoto


Porte su cui è necessario raggiungere |product| per un utilizzo da remoto:

- 5061 TCP (SIP TLS)
- da 10000 a 20000 UDP (Audio)
- 10389 TCP (Rubrica)


Configurazione
--------------

E' possibile configurare l'applicazione tramite il provisioning di |product|.

Per farlo collegare lo smartphone alla rete locale del |product| e andare in Impostazioni -> Provisioning Settings.

Impostare:

- Config Upgrade Via: TFTP
- Config percorso server : ip locale di |product|

Cliccare su Start Provisioning.

Questa operazione permetterà di aggiungere il Mac-Address dello smartphone a quelli dei device configurabili.

E' utile conoscere il MAC Address dello smartphone che si vuole configurare, è possibile verificarlo nel momento della richiesta TFTP in /var/log/messages: ::

    Jan 10 15:26:44 nethvoice dnsmasq-tftp[16179]: file /var/lib/tftpboot/cfgDC0B34CED538.xml not found

il MAC Address dello smartphone in questo caso è DC:0B:34:CE:D5:38

Aprire il wizard di |product|, andare sulla pagina "Dispositivi" ed effettuare una nuova scansione, sarà presente una riga con "CTI App" come marca e GS Wave come modello.

Nella sezione Utenti -> Configurazioni del wizard associare il device all'utente voluto e cliccare su Configura e riavvia per pubblicare la configurazione.

Forzare il provisioning di nuovo con la procedura precedente Impostazioni -> Provisioning Settings -> Start Provisioning per configurare l'applicazione.

.. note:: Per consentire l'accesso da remoto alla rubrica di |product| ricordarsi di abilitare l'accesso da reti esterne alla rubrica centralizzata in |parent_product|


BLF
...

Per configurare i BLF e monitorare altri interni di |product| seguire questa procedura:

- In Contatti -> SIP creare i contatti necessari specificando il Nome, Cognome e l'interno SIP
- In Impostazioni -> Impostazioni Avanzate -> Impostazioni Aggiuntive attivare i BLF
- In Impostazioni -> Impostazioni Avanzate -> Impostazioni Aggiuntive -> Elenco BLF selezionare i contatti da utilizzare come BLF

I BLF verranno mostrati in Contatti -> SIP


Scan&Play
=========

.. _app_mobile:

L'applicazione Scan&Play è disponibile su smartphone e permette di scansionare i MAC address dei telefoni per velocizzare la configurazione e il provisioning.

Requisiti
---------

- Presenza di un certificato valido sul server
- Raggiungibilità della porta HTTPS 443 dall'esterno

Installazione
-------------

L'applicazione è disponibile ai seguenti link:

- Android: https://play.google.com/store/apps/details?id=it.nethesis.scanplay14
- iOS: https://itunes.apple.com/us/app/nethvoice-scan-play-14/id1277558637?ls=1&mt=8

E' possibile comunque cercare la parola **macscan** nei diversi store e installarla senza il link diretto.

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
