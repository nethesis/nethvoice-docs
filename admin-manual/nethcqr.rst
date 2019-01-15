Call Query Routing
=============================

Descrizione
-----------

Il Call Query Routing di |product| ribalta il concetto di IVR tradizionale spostando dal chiamante allo stesso |product| la decisione di come trattare la chiamata in ingresso e quindi verso che destinazione sul centralino deve proseguire.

Riconoscendo il chiamante, grazie al numero telefonico o alla richiesta di un codice cliente, il |product| può interrogare database sia esterni che interni (MYSQL o MSSQL) chiedendo dei dati relativi al chiamante e in base alla risposta può poi comportarsi come configurato.

Si tratta quindi di uno strumento flessibile, che in tempo reale ottiene informazioni e poi si comporta in base a queste, ma queste informazioni possono variare nel tempo variando di conseguenza in comportamento del |product|.

L'esempio tipico di utilizzo del Call Query Routing è utilizzarlo per discriminare se un chiamante sia un cliente in regola con i pagamenti o no.

Il |product| chiederà questa informazione al database del software gestionale ed ottenuta la risposta si comporterà di conseguenza, ad esempio se si tratta di un cliente in regola la chiamata verrà fatta proseguire verso la coda di assistenza mentre se si tratta di un cliente insolvente la chiamata verrà dirottata verso gli interni dell'amministrazione e magari se si tratta di un potenziale cliente la chiamata verrà girata ai commerciali.

Le uniche condizioni necessarie al Call Query Routing sono l'accessibilità da parte del |product| ai database da interrogare e l'impostazione della query per fare l'interrogazione, di competenza di chi conosce il database.

É possibile con il numero del chiamante consultare subito un database per ottenere lo stato del cliente, oppure sempre partendo dal numero chiamante prima ricavare il codice cliente del chiamante per poi utilizzarlo nel database clienti. In caso di fallimento della procedura di scoperta del codice cliente è possibile avere come backup la richiesta di inserimento manuale del codice cliente.

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

Destinazione della chiamata per ogni condizione non specificata successivamente, di solito la più probabile. É anche la destinazione della chiamata in caso di un qualsiasi errore, sia esso di connessione al database o nell'effettuare la query.

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


