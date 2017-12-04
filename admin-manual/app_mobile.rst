==========
App mobile
==========

L'applicazione Scan&Play è disponibile su smartphone e permette di scansionare i MAC address dei telefoni per velocizzare la configurazione e il provisioning.

Requisiti
---------

- Presenza di un certificato valido sul server
- Raggiungibilità della porta HTTPS 443 dall'esterno
- Apertura del range di porte UDP dalla 10000 alla 20000 per consentire l'utilizzo del softphone WebRTC

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