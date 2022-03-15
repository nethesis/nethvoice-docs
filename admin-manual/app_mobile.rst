==========
App mobile
==========


.. _nethcti_mobile:

|product_cti|
=============

L'applicazione mobile del |product_cti| è disponibile per iOS e Android ed è scaricabile dai rispettivi App Store (controllare la versione di software minima richiesta nelle specifiche dell'App negli store).

I requisiti per utillizzare l'app sono:

- certificato valido installato sul |product|
- ip pubblico statico
- indirizzo FQDN del |product| raggiungibile e utilizzato nella configurazione dell'app (manualmente o nel |product_cti|)
- porta 443 HTTPS raggiungibile
- porta 6061 TCP raggiungibile
- range 10000-20000 UDP raggiungibile
- :guilabel:`Accesso SIPS esterno` deve essere abilitato nella pagina :guilabel:`Amministrazione -> Impostazioni` del wizard

Per far funzionare la App Mobile dalla stessa rete locale del |product| è necessario che sul firewall (più precisamente sull'apparato che gestisce il NAT dell'ip pubblico associato al |product|) sia abilita la funzione "hairpin NAT" denominata anche come NAT reflection / NAT hairpining / NAT on a stick / loopback NAT.

.. note:: In alternativa al FQDN del |product| è possibile usare un nome host e dominio configurato come alias per il server con gli stessi requisiti.
   Per usarlo al posto del FQDN utilizzare questi comandi sostituendo ad ALIAS il nome host seguito dal dominio (ad esempio host.dominio.com): ::

        config setprop nethvoice PublicHost ALIAS
        signal-event nethserver-nethvoice14-update
        signal-event nethcti-server3-update

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
