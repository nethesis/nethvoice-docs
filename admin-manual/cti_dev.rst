Panoramica
==========

Questa sezione della documentazione ha lo scopo di avviare lo sviluppatore alla
realizzazione di un'applicazione reale che sfrutti le REST API di |product_cti|.
Gli argomenti trattati sono quelli dell'autenticazione, dell'utilizzo delle REST API
e della comunicazione bidirezionale via WebSocket.

In tal modo lo sviluppatore sarà in grado di realizzare applicazioni in grado di mostrare
informazioni in tempo reale e di poter effettuare operazioni di ogni genere.

.. _authentication-ref-label:

Autenticazione
==============

Lo scopo della fase d’autenticazione è creare un token che sarà usato per le
operazioni future, quali l’invocazione delle REST API o per creare una connessione
permanente (WebSocket o TCP).


Eseguire il login
-----------------

1. Il client invia una richiesta HTTPS (POST) alla seguente rest api:

.. code-block:: bash

 https://<SERVER>/webrest/authentication/login

specificando lo *username* e *password* in formato JSON:

.. code-block:: json

 { "username": "my_user", "password": "my_password" }

2. Il client riceve una risposta standard HTTPS 401. Se l'autenticazione ha avuto successo la risposta contiene un *nonce* (una stringa) nello header HTTPS, altrimenti l'autenticazione è fallita. Un esempio di header è (il nonce è *06d15944d8ece69bdc97742b37c507970e2f6651*):

.. code-block:: bash

 www-authenticate: Digest 06d15944d8ece69bdc97742b37c507970e2f6651


3. Il client calcola il token:

.. code-block:: bash

 tohash = username + ':' + password + ':' + nonce
 token  = HMAC-SHA1(tohash, password)

4. Il client memorizza il token per usi futuri.

**Se il token d'autenticazione non viene mai usato, scade dopo un certo periodo di tempo (il default è mezz'ora).
Una nuova fase d'autenticazione è necessaria.**


Eseguire il logout
------------------

1. Il client invia una richiesta HTTPS (POST) alla seguente rest api:

.. code-block:: bash

    https://<SERVER>/webrest/authentication/logout

2. Il token viene rimosso dal server.


REST API
========

Le REST API sono dei Web Services che consentono l'interazione con il server |product_cti|. È uno strumento molto utile per l'integrazione e lo sviluppo.

.. note::

 Questo documento assume che il lettore possegga già una certa familiarità con le più comuni tecniche di programmazione e Web Services.

Come usare una API
------------------

Di seguito vengono elencate le caratteristiche comuni a tutte le REST API:

* una API viene invocata tramite l'invio di una richiesta HTTPS al server |product_cti| che risponde fornendo i dati richiesti o tramite un codice di stato o entrambi.
* I codici di stato delle risposte HTTPS sono quelli `standard <http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html>`_.
* Il formato utilizzato per lo scambio dati è `JSON <http://www.json.org/>`_.
* Tutte le risorse sono raggiungibili tramite l'urli base:

.. code-block:: bash

  https://<SERVER>/webrest/

* Per richiedere una API è necessario aggiungere un *patì* al baseurl che specifica la risorsa da richiedere. Per esempio:

.. code-block:: bash

  https://<SERVER>/webrest/phonebook/search

* Ogni richiesta deve contenere i parametri d'autenticazione per il controllo d'accesso, specificando lo header HTTPS ``Authorization``:

.. code-block:: bash

 Authorization: username:token

* Ogni richiesta viene *autenticata* e *autorizzata* del server |product_cti|.


Autenticazione
--------------

#. L'autenticazione di una richiesta REST viene eseguita dal server controllando la validità del token passato. Quindi, come fase preliminare, Il client deve eseguire il login e deve creare un token d'autenticazione come descritto :ref:`qui <authentication-ref-label>`.
#. Ogni richiesta deve contenere lo header HTTPS ``Authorization``:

.. code-block:: bash

    Authorization: username:token

**La validità del token d'autenticazione viene aggiornato ad ogni richiesta, altrimenti scade dopo un certo intervallo temporale (di default pari a un'ora). Dopo la scadenza è necessaria una nuova fase d'autenticazione.**


Autorizzazione
--------------

Ogni richiesta REST API viene autorizzata dal server che controlla i permessi utente configurati dall'amministratore attraverso l'interfaccia di |parent_product|.


Esempio d'uso con cURL
----------------------

L'esempio seguente mostra come eseguire una richiesta rest tramite `cURL <http://curl.haxx.se/>`_. Lo strumento si può rivelare utile per eseguire dei test e per comprendere il meccanismo delle chiamate con maggior dettaglio.

1. Supponiamo di volere effettuare la ricerca in rubrica del contatto *nethesis* per estrarre il numero telefonico. La prima operazione da eseguire è l'autenticazione (è necessaria solamente la prima volta per la costruzione del token).

.. code-block:: bash

 curl --insecure -i -X POST -d 'username=my_user&password=my_password' https://192.168.5.226/webrest/authentication/login

L'autenticazione ha successo e il server risponde con:

.. code-block:: bash

 HTTP/1.1 401 Unauthorized
 Date: Thu, 12 Jun 2014 13:01:43 GMT
 www-authenticate: Digest f4700adb35ad29ee16afe6c03c0196dfc74ec3b1
 Content-Length: 0
 Content-Type: text/plain

2. Estraiamo il nonce dall'header *www-authenticate*:

.. code-block:: bash

 f4700adb35ad29ee16afe6c03c0196dfc74ec3b1

3. Costruiamo il token d'autenticazione:

.. code-block:: bash

 tohash = "my_user:my_password:f4700adb35ad29ee16afe6c03c0196dfc74ec3b1"
 token  = HMAC-SHA1("my_user:my_password:f4700adb35ad29ee16afe6c03c0196dfc74ec3b1", "my_password") = "1d8062d1c85a8fe6983745a1ee318d1cd9b8bde1"

 $ echo -n "my_user:my_password:f4700adb35ad29ee16afe6c03c0196dfc74ec3b1" | openssl dgst -sha1 -hmac "my_password"
 (stdin)= 1d8062d1c85a8fe6983745a1ee318d1cd9b8bde1

4. Chiamiamo la rest api *phonebook/search*:

.. code-block:: bash

 curl --insecure -i -H "Authorization: my_user:1d8062d1c85a8fe6983745a1ee318d1cd9b8bde1" https://192.168.5.226/webrest/phonebook/search/nethesis

5. Il server invia la risposta in format JSON con i dati richiesti:

.. code-block:: json

 {
    "centralized": [
        {
            "id": 1916,
            "owner_id": "",
            "type": "Reseller",
            "homeemail": null,
            "workemail": "info@nethesis.it",
            "homephone": null,
            "workphone": "0721405516",
            "cellphone": "",
            "fax": "",
            "title": null,
            "company": "NETHESIS SRL ",
            "notes": "",
            "name": "",
            "homestreet": null,
            "homepob": null,
            "homecity": null,
            "homeprovince": null,
            "homepostalcode": null,
            "homecountry": null,
            "workstreet": "VIA DEGLI OLMI, 12",
            "workpob": null,
            "workcity": "PESARO",
            "workprovince": null,
            "workpostalcode": null,
            "workcountry": null,
            "url": "http://www.nethesis.it"
        }
    ],
    "nethcti": []
 }

Elenco delle API |product_cti|
------------------------------

.. _/astproxy: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_astproxy.html
.. _/authentication: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_authentication.html
.. _/custcard: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_custcard.html
.. _/historycall: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_historycall.html
.. _/histcallswitch: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_histcallswitch.html
.. _/phonebook: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_phonebook.html
.. _/streaming: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_streaming.html
.. _/voicemail: http://api.nethesis.it/nethcti-v3/classes/plugin_rest_voicemail.html

====================== ==================================================================================
Path                   Descrizione
====================== ==================================================================================
`/astproxy`_           Interazione con il server Asterisk
`/authentication`_     Funzionalità d'autenticazione
`/custcard`_           Funzionalità relative alle schede clienti
`/historycall`_        Storico delle chiamate del proprio utente
`/histcallswitch`_     Storico delle chiamate di tutti gli utenti del sistema
`/phonebook`_          Funzionalità relative alle rubriche
`/streaming`_          Funzionalità sulle sorgenti video
`/voicemail`_          Funzionalità relative alle voicemail
====================== ==================================================================================

WebSocket
=========

La connessione WebSocket viene utilizzata dal server per comunicare in tempo reale con tutti i client connessi (ad esempio per notificare gli eventi del server Asterisk).
Per stabilire una connessione WebSocket col server |product_cti| è necessaria una prima fase d'autenticazione.

Eseguire il login
-----------------

1. Il client esegue il login e crea un nuovo token d'autenticazione come descritto :ref:`qui <authentication-ref-label>`
2. Il client stabilisce una connessione websocket con il server sulla porta HTTPS 443:

.. code-block:: bash

 socket = new io('https://server.domain.com', {
   "upgrade": false,
   "transports": ['websocket'],
   "reconnection": true,
   "reconnectionDelay": 2000
 });

3. Il client invia il messaggio *login* al server attraverso la connessione websocket specificando *username* e *token* in formato JSON:

.. code-block:: bash

 socket.emit('login', { accessKeyId: username, token: token.toString() });

4. Se il login ha avuto successo il client riceve il messaggio *authe_ok*, altrimenti il messaggio *401* e il client viene disconnesso.

**Una volta completato il login con successo, il token ha validità infinita fino al riavvio del server.**

Sottoscrizione eventi
---------------------

Attraverso la connessione WebSocket vengono emessi i seguenti eventi:

.. _extenUpdate: http://api.nethesis.it/nethcti-v3/classes/com_nethcti_ws.html#event_extenUpdate
.. _queueMemberUpdate: http://api.nethesis.it/nethcti-v3/classes/com_nethcti_ws.html#event_queueMemberUpdate
.. _trunkUpdate: http://api.nethesis.it/nethcti-v3/classes/com_nethcti_ws.html#event_trunkUpdate
.. _queueUpdate: http://api.nethesis.it/nethcti-v3/classes/com_nethcti_ws.html#event_queueUpdate
.. _parkingUpdate: http://api.nethesis.it/nethcti-v3/classes/com_nethcti_ws.html#event_parkingUpdate
.. _wsClientLoggedIn: http://api.nethesis.it/nethcti-v3/classes/com_nethcti_ws.html#event_wsClientLoggedIn

========================= ===================================================================================
Evento                    Descrizione
========================= ===================================================================================
`extenUpdate`_            Aggiornamento di stato di un interno telefonico
*updateNewVoiceMessages*  Invia tutti i nuovi messaggi vocali in corrispondenza dell'arrivo di uno nuovo
*newVoiceMessageCounter*  Invia il numero di nuovi messaggi vocali in corrispondenza dell'arrivo di uno nuovo
`queueMemberUpdate`_      Aggiornamento di stato di un agente di una coda
`trunkUpdate`_            Aggiornamento di stato di un fascio
*extenRinging*            Notifica che un interno sta squillando e riporta l'identificativo del chiamante
`queueUpdate`_            Aggiornamento di stato di una coda
`parkingUpdate`_          Aggiornamento di stato di un parcheggio
`wsClientLoggedIn`_       Un utente ha effettuato il login a |product_cti|
*allWsClientDisonnection* Un utente non ha più nessuna connessione WebSocket attiva
*401*                     L'autenticazione è fallita
*authe_ok*                L'autenticazione è avvenuta con successo
========================= ===================================================================================

Ogni evento fornisce i dati relativi in formato JSON.

È possibile sottoscrivere un ascoltatore per ciascuno degli eventi. Un esempio è il seguente:

.. code-block:: javascript

 socket.on('extenUpdate', function (data) {
     // all the code here
 });
