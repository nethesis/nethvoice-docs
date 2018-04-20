|product|: Call Query Routing
=============================

Descrizione
-----------

Il Call Query Routing di |product| ribalta il concetto di IVR tradizionale spostando dal chiamante allo stesso |product| la decisione di come trattare la chiamata in ingresso e quindi verso che destinazione sul centralino deve proseguire.

Riconoscendo il chiamante, grazie al numero telefonico o alla richiesta di un codice cliente, il |product| può interrogare database sia esterni che interni (MYSQL o MSSQL) chiedendo dei dati relativi al chiamante e in base alla risposta può poi comportarsi come configurato.

Si tratta quindi di uno strumento flessibile, che in tempo reale ottiene informazioni e poi si comporta in base a queste, ma queste informazioni possono variare nel tempo variando di conseguenza in comportamento del |product|.

L'esempio tipico di utilizzo del Call Query Routing è utilizzarlo per discriminare se un chiamante sia un cliente in regola con i pagamenti o no.

Il |product| chiederà questa informazione al database del software gestionale ed ottenuta la risposta si comporterà di conseguenza, ad esempio se si tratta di un cliente in regola la chiamata verrà fatta proseguire verso la coda di assistenza mentre se si tratta di un cliente insolvente la chiamata verrà dirottata verso gli interni dell'amministrazione e magari se si tratta di un potenziale cliente la chiamata verrà girata ai commerciali.

Le uniche condizioni necessarie al Call Query Routing sono l'accessibilità da parte del |product| ai database da interrogare e l'impostazione della query per fare l'interrogazione, di competenza di chi conosce il database.

E' possibile con il numero del chiamante consultare subito un database per ottenere lo stato del cliente, oppure sempre partendo dal numero chiamante prima ricavare il codice cliente del chiamante per poi utilizzarlo nel database clienti. In caso di fallimento della procedura di scoperta del codice cliente è possibile avere come backup la richiesta di inserimento manuale del codice cliente.

Configurazione
--------------

Per il collegamento ad un database MSSQL è necessario preliminarmente configurare il collegamento ODBC, vedi nella documentazione `Rubrica Centralizzata <http://nethserver.docs.nethesis.it/it/latest/phonebook-mysql.html#configurazione-odbc>`_


Nome CQR
~~~~~~~~

Nome del CQR che poi verrà utilizzato da |product| nelle destinazioni dei vari moduli.

Descrizione CQR
~~~~~~~~~~~~~~~

Descrizione del CQR.

Risoluzione Codice Cliente
--------------------------

Usa Codice Cliente
~~~~~~~~~~~~~~~~~~

Se abilitato, il CQR è attivato per la ricerca del codice cliente. Il Codice cliente viene ricavato dal numero del chiamante tramite la query apposita, nel caso la procedura non desse risultati e fosse stata abilita la voce Codice Cliente Manuale verrà chiesto dal |product| l'inserimento del codice.

Tipo Db Codice Cliente
~~~~~~~~~~~~~~~~~~~~~~

Tipo di database dove effettuare la query per il codice cliente.

URL db codice cliente
~~~~~~~~~~~~~~~~~~~~~

URL per collegarsi al database per effettuare la query per ricavare il codice cliente.

Nome db codice cliente
~~~~~~~~~~~~~~~~~~~~~~

Nome del database dove effettuare la query codice cliente, nel caso di sorgente MSSQL nome configurato nella connessione ODBC(nomeDSN).

Username db codice cliente
~~~~~~~~~~~~~~~~~~~~~~~~~~

Username per il collegamento al database per la query codice cliente.
Accertarsi che abbia i permessi d'accesso.

Password db codice cliente
~~~~~~~~~~~~~~~~~~~~~~~~~~

Password dell'utente per accedere al database.

Query codice cliente
~~~~~~~~~~~~~~~~~~~~

Query per ottenere il codice cliente partendo dal numero chiamante.
%CID% verrà sostituito con il numero chiamante.

Ad esempio: 

::

  SELECT `customer_code` FROM `phonebook` WHERE `caller_id` = '%CID%'


Codice Cliente Manuale
~~~~~~~~~~~~~~~~~~~~~~

Se abilitato nel caso la query del codice cliente non dia risultati viene richiesto l'inserimento manuale del codice cliente.

Annuncio Codice Cliente
~~~~~~~~~~~~~~~~~~~~~~~

Annuncio da riprodurre per richiedere l'inserimento del codice cliente manualmente. Viene proposto l'elenco delle Registrazioni di Sistema già caricate.

Annuncio Errore Codice Cliente
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Annuncio da riprodurre in caso di errore nell'inserimento del codice cliente. Viene proposto l'elenco delle Registrazioni di Sistema già caricate.

Lunghezza Codice Cliente
~~~~~~~~~~~~~~~~~~~~~~~~

Lunghezza del codice cliente nel caso si arrivi all'inserimento manuale.

Numero Tentativi
~~~~~~~~~~~~~~~~

Numero di tentativi disponibile per inserire un codice cliente valido manualmente.

Query Controllo Codice Cliente
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Query da effettuare dopo l'inserimento del codice cliente manualmente per controllarle la validità.

I parametri di collegamento utilizzati sono quelli indicati per la Query Codice Cliente.

Formattare la query in modo da far ritornare un qualsiasi risultato in caso di codice cliente corretto, mentre non devono ritornare risultati in caso di codice cliente errato.

%CODCLI% verrà sostituito con il codice cliente inserito.

Ad esempio: 

::
  
  SELECT `customer_code` FROM `phonebook` WHERE `customer_code` = '%CODCLI%'

Opzioni CQR
-----------

Annuncio
~~~~~~~~

Messaggio che viene riprodotto al chiamante mentre il CQR viene utilizzato. Deve essere almeno della durata delle interrogazioni in modo da dare al |product| il tempo di effettuarle.

Tipo di database
~~~~~~~~~~~~~~~~

Tipo di database dove effettuare la query per ottenere un risultato sul quale basare come il |product| debba proseguire il flusso della chiamata.

URL Database
~~~~~~~~~~~~~

URL per collegarsi al database per effettuare la query. In caso del |product| stesso inserire ``localhost``.

Nome Database
~~~~~~~~~~~~~

Nome del database al quale collegarsi, nel caso di sorgente MSSQL nome configurato nella connessione ODBC(nomeDSN).

Username
~~~~~~~~

Username per il collegamento al database. Accertarsi che l'utente abbia i permessi di accesso.

Password
~~~~~~~~

Password dell'utente per accedere al database.

Query
~~~~~

Query da effettuare una volta avvenuto il collegamento con il database.

La query si baserà sul numero chiamante nel caso non sia abilitata la richiesta di codice cliente o direttamente sul codice cliente ricavato dalla query del codice cliente da configurare successivamente.

Sono da inserire nella query %CID% che verrà sostituito con il numero del chiamante nel primo caso o %CUSTOMERCODE% nel caso di utilizzo del codice cliente.

Ad esempio: 

::

  SELECT `name` FROM `phonebook` WHERE `workphone`= '%CID%'  
  
  SELECT `name` FROM `phonebook` WHERE `customercode` = '%CUSTOMERCODE%'

Destinazione di default
~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata per ogni condizione non specificata successivamente, di solito la più probabile. E' anche la destinazione della chiamata in caso di un qualsiasi errore, sia esso di connessione al database o nell'effettuare la query.

Voci NethCQR
------------

Posizione
~~~~~~~~~

La posizione indica l'ordine con il quale il |product| valuterà il risultato che ha ritornato la query.

Condizione
~~~~~~~~~~

Inserire qui i possibili risultati della query, uno per riga.

Destinazione
~~~~~~~~~~~~

Destinazione della chiamata se il risultato della query coincide con la condizione inserita.

Elimina
~~~~~~~

Cancella una riga errata o non più necessaria.


|product|: installazione codec g729
===================================

Per installare ed attivare il codec g729 Open Source ecco la procedura (comporta il riavvio di Asterisk e quindi l'eventuale caduta di chiamate in corso):

.. code-block:: bash

  cd /usr/lib64/asterisk/modules/
  wget http://asterisk.hosting.lv/bin/codec_g729-ast130-gcc4-glibc-x86_64-pentium4.so
  mv codec_g729-ast130-gcc4-glibc-x86_64-pentium4.so codec_g729.so
  chmod 755 codec_g729.so
  systemctl restart asterisk

Il codec g729 Open Source non è compatibile con la versione a pagamento di Digium, che si può installare seguendo la procedura che vi forniranno con l'acquisto.

E' possibile, quindi, utilizzare contemporaneamente solo una delle due versioni di g729, Open Source o Digium.

|product|: configurazione dell'IP locale
========================================

In fase di provisioning, l'IP usato come IP del centralino è l'IP della prima rete ``green`` (rete locale). 
Questo può essere modificato da linea di comando, per esempio se si hanno :index:`reti green multiple`.
Se si desidera forzare un determinato indirizzo IP, esempio ``192.168.123.11``, utilizzare i seguenti comandi: ::

  config setprop nethvoice LocalIP 192.168.123.11
  signal-event nethserver-nethvoice14-update

|product|: configurazione del transport PJSIP
=============================================

In |product| il modulo `chan_pjsip` di Asterisk è configurato per stare in ascolto su tutti gli indirizzi di tutte le reti green.
È possibile che sia necessario cambiare questa configurazione in situazioni particolari.
Se si desidera che chan_pjsip stia in ascolto anche sulle RED ed i loro alias, eseguire i comandi: ::

  config setprop nethvoice PJSIPBind all
  signal-event nethserver-nethvoice14-update

Se invece si desidera fare delle personalizzazioni maggiori, come ad esempio escludere una rete green, è possibile farlo dall'interfaccia della configurazione avanzata:
:menuselection:`Asterisk SIP Settings --> Chan PJSIP Settings`.
Sarà poi necessario abilitare le configurazioni avanzate :guilabel:`Show Advanced Settings` e fare le opportune modifiche. 


.. note::

   Se la visualizzazione delle configurazioni avanzate è abilitata, le impostazioni di transport **non** 
   verranno più sovrascritte in caso di aggiornamento o modifica delle interfacce di rete.

|product_cti|: attivazione debug
================================

Di default il file di log riporta solamente messaggi di *warning* ed *errori*.
È possibile innalzare il livello di debug per avere maggiori informazioni:

.. code-block:: bash

  config setprop nethcti-server LogLevel info
  signal-event nethcti-server3-update

.. warning::
  Innalzando il livello la dimensione del file di log aumenta rapidamente.

Per ripristinare il livello di default:

.. code-block:: bash

  config setprop nethcti-server LogLevel warn
  signal-event nethcti-server3-update


|product_cti|: disattivazione della modalità di Click2Call automatico
=====================================================================

Necessità di sollevare la cornetta telefonica.

In alcuni scenari potrebbe essere utile disattivare la funzionalità, ad esempio nel caso in cui
il centralino telefonico è in cloud ed i telefoni siano in LAN dietro NAT. Per disattivare:

.. code-block:: bash

  config setprop nethcti-server AutoC2C disabled
  signal-event nethcti-server3-update

Per ripristinare il valore di default:

.. code-block:: bash

  config setprop nethcti-server AutoC2C enabled
  signal-event nethcti-server3-update


|product_cti|: utilizzo di un server chat esterno
=================================================

È possibile configurare un server chat presente su un'altra macchina:

.. code-block:: bash

  config setprop nethcti-server JabberUrl <BOSH_URL>
  signal-event nethcti-server3-update

Per esempio:

.. code-block:: bash

  config setprop nethcti-server JabberUrl https://nethserver.mydomain.it/http-bind
  signal-event nethcti-server3-update

Per ripristinare il default:

.. code-block:: bash

  config setprop nethcti-server JabberUrl ""
  signal-event nethcti-server3-update

.. note::
  Il server chat specificato deve supportare `XMPP <https://en.wikipedia.org/wiki/XMPP>`_ su protocollo `BOSH <https://en.wikipedia.org/wiki/BOSH_(protocol)>`_.
  `NethServer <http://docs.nethserver.org/it/v7/chat.html>`_ lo supporta di default.


|product_cti|: configurazione di un prefisso telefonico
=======================================================

È possibile configurare un prefisso telefonico per qualsiasi chiamata:

.. code-block:: bash

  config setprop nethcti-server Prefix <PREFISSO>
  signal-event nethcti-server3-update


Per ripristinare il default:

.. code-block:: bash

  config setprop nethcti-server Prefix ""
  signal-event nethcti-server3-update


|product_cti|: configurazione Softphone WebRTC
==============================================

Il softphone WebRTC utilizza il `Gateway Janus <https://github.com/meetecho/janus-gateway>`_
installato direttamente nel centralino telefonico.

Janus-gateway può operare in tre differenti modalità di NAT:

1. STUN (default)
2. ICE
3. 1:1 (NAT)

Per la configurazione del NAT e delle opzioni, sono disponibili quattro proprietà sotto la
chiave *janus-gateway* del database di configurazione:

1. NatMode: <stun|ice|1:1>
2. StunServer: indirizzo del server STUN da usare. Il default è *stun1.l.google.com*. Viene ignorato se la modalità non è STUN
3. StunPort: porta del server STUN. Il default è 19302. Viene ignorato se la modalità non è STUN
4. PublicIP: è l'indirizzo IP pubblico del server su cui è in esecuzione janus-gateway. Viene ignorato se la modalità non è 1:1

In alcuni scenari d'utilizzo l'audio delle telefonate potrebbe non funzionare e conseguentemente le chiamate
vengono terminate automaticamente dal centralino dopo un certo intervallo temporale. In questi casi
è necessario configurare correttamente il WebRTC in base all'architettura di rete utilizzata.

*Esempio*

Nel caso si utilizzi un centralino in cloud dietro NAT, è necessario configurare il WebRTC come segue:

.. code-block:: bash

  config setprop janus-gateway NatMode 1:1
  config setprop janus-gateway PublicIP <DOMAIN OR PUBLIC IP>
  signal-event nethserver-janus-update


