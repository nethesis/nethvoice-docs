============
Applicazioni
============

.. _call_query_routing_ref_label:
   
Call Query Routing
==================

 
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

Collegamento a database MSSQL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Per il collegamento ad un database MSSQL è necessario preliminarmente configurare il collegamento ODBC, vedi nella documentazione `Rubrica Centralizzata <http://nethserver.docs.nethesis.it/it/latest/phonebook-mysql.html#configurazione-odbc>`_

Nome CQR
~~~~~~~~

Nome del CQR che poi verrà utilizzato da |product| nelle destinazioni dei vari moduli.

Descrizione CQR
~~~~~~~~~~~~~~~

Descrizione del CQR.

Opzioni CQR
-----------

Annuncio
~~~~~~~~

Messaggio che viene riprodotto al chiamante mentre il CQR viene utilizzato. Deve essere almeno della durata delle interrogazioni in modo da dare al |product| il tempo di effettuarle.

Tipo di database
~~~~~~~~~~~~~~~~

Tipo di database dove effettuare la query per ottenere un risultato sul quale basare come il |product| debba proseguire il flusso della chiamata.

URL Datatbase
~~~~~~~~~~~~~

URL per collegarsi al database per effettuare la query. In caso del |product| stesso inserire localhost.

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

Ad esempio: SELECT \`name\` FROM \`phonebook\` WHERE \`workphone\`= '%CID%' o SELECT \`name\` FROM \`phonebook\` WHERE \`customercode\` = '%CUSTOMERCODE%'

Destinazione di default
~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata per ogni condizione non specificata successivamente, di solito la più probabile. E' anche la destinazione della chiamata in caso di un qualsiasi errore, sia esso di connessione al database o nell'effettuare la query.

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

Ad esempio: SELECT\` customer\_code\` FROM \`phonebook\` WHERE \`caller\_id\` = '%CID%'

Codice Cliente Manuale
~~~~~~~~~~~~~~~~~~~~~~

Se abilitato nel caso la query del codice cliente non dia risultati viene richiesto l'inserimento manuale del codice cliente.

Annuncio Codice Cliente
~~~~~~~~~~~~~~~~~~~~~~~

Annuncio da riprodurre per richiedere l'inserimento del codice cliente manualmente. Viene proposto l'elenco delle :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Annuncio Errore Codice Cliente
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Annuncio da riprodurre in caso di errore nell'inserimento del codice cliente. Viene proposto l'elenco delle :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

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

Ad esempio: SELECT \`customer\_code\` FROM \`phonebook\` WHERE \`customer\_code\` = '%CODCLI%'

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

.. _conferenze_ref_label:

Conferenze
==========

Descrizione
-----------

Il modulo conferenze di |product| permette di mettere in comunicazione più chiamate contemporaneamente con delle politiche di permessi e di funzionamento che possono essere configurate nei dettagli.

E' importante sottolineare che è possibile mettere in comunicazione tra loro nella stessa chiamata non solo gli interni del |product| ma anche una qualsiasi chiamata effettuata o ricevuta semplicemente trasferendola al numero della Conferenza.

La Conferenza di |product| può avere un utente amministratore, diverso dai normali utenti, che dirige la conferenza, decide chi ne deve far parte e senza il quale la Conferenza non inizia. Questa differenziazione tra utenti avviene tramite l'inserimento di un codice PIN.

E' possibile inoltre limitare il numero di partecipanti e registrare la Conferenza.

Configurazione
--------------

Numero Conferenza
~~~~~~~~~~~~~~~~~

Il numero da assegnare alla Conferenza, non deve essere utilizzato in nessuna altra parte del |product|, che poi sarà utilizzato chiamandolo a trasferendoci una chiamata per entrare nella Conferenza.

Nome Conferenza
~~~~~~~~~~~~~~~

Nome descrittivo della Conferenza per riconoscerla facilmente all'interno della configurazione di |product|.

PIN utente
~~~~~~~~~~

Codice numerico che individuerà i membri della Conferenza di tipo utente. E' opzionale se si vuole fare distinzioni tra utenti e amministratore. Se non viene configurato non verrà chiesto.

PIN amministratore
~~~~~~~~~~~~~~~~~~

Codice numerico che individuerà l'amministratore della Conferenza. E' opzionale ma diventa obbligatorio se si attiva l'attesa dell'amministratore per iniziare la conferenza.

Opzioni Conferenza
------------------

Messaggio di ingresso
~~~~~~~~~~~~~~~~~~~~~

Messaggio da riprodurre ai chiamante che entra in Conferenza. Viene scelto tra le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>`.

Attendere l'amministratore
~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato la Conferenza non inizia se non è presente l'amministratore, individuato dalla richiesta di PIN.

Ottimizzazione del Parlante
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato |product| agisce sulla voce di chi sta parlando per isolarla meglio e renderla più chiara togliendo il rumore di fondo.

Rilevamento Speaker
~~~~~~~~~~~~~~~~~~~

Se attivato |product| individua il canale di chi sta parlando riuscendo a inviare meglio gli eventi della Conferenza.

Modalità silenziosa
~~~~~~~~~~~~~~~~~~~

Se attivato i suoni di entrata e di uscita dalla Conferenza non saranno riprodotti.

Conteggio Utente
~~~~~~~~~~~~~~~~

Se abilitato viene annunciato il conteggio degli utenti quando entrano nella Conferenza.

Ingresso/uscita utenti
~~~~~~~~~~~~~~~~~~~~~~

Se abilitato viene annunciato l'ingresso e l'uscita degli utenti.

Musica di Attesa
~~~~~~~~~~~~~~~~

Viene riprodotta la musica di attesa per gli utenti collegati prima che la Conferenza inizi.

Classe Musica di Attesa
~~~~~~~~~~~~~~~~~~~~~~~

La classe di :ref:`Musica di Attesa <musiche_di_attesa_ref_label>` da riprodurre ai chiamanti che aspettano l'inizio della Conferenza. Può essere ereditata dalle impostazioni già fatte sulla chiamata o sovrascritta da questa impostazione.

Permetti Menù
~~~~~~~~~~~~~

Permette l'accesso al menù, amministratore o utente, della Conferenza premendo \*

Registrare Conferenza
~~~~~~~~~~~~~~~~~~~~~

Se abilitato la Conferenza verrà registrata automaticamente.

Numero Massimo Partecipanti
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero massimo dei partecipanti che possono entrare nella Conferenza.

Silenzia quando collegato
~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato tutti gli utenti che entrano in Conferenza saranno silenziati. Per essere riattivati o si deve concedere l'accesso al menù della Conferenza o deve essere abilitata l'attesa dell'amministratore.


.. _disa_ref_label:

Disa
====

Descrizione
-----------

La DISA da la possibilità di chiamare dall'esterno ed ascoltare il tono di chiamata interno per poter fare qualsiasi chiamata interna o esterna, come se si fosse all'interno dell'azienda.

Il suo scopo principale è quello di fare delle chiamate dall'esterno presentandosi però con il numero telefonico delle linee collegate al |product|.

Può anche essere utilizzata per utilizzare i servizi telefonici del |product| dall'esterno come se si fosse in azienda.

Per entrare in una DISA la chiamata dovrà esserci destinata, a partire dalle :ref:`rotte in entrata <rotte_in_entrata_ref_label>` ad esempio.

Configurazione
--------------

Nome DISA
~~~~~~~~~

Nome per identificare la DISA

PIN
~~~

Per usufruire dei servizi della DISA si può prevedere la richiesta di un PIN.

Timeout Risposta
~~~~~~~~~~~~~~~~

E' il tempo in secondi che il sistema attende una risposta dopo aver fatto una chiamata.

Timeout Digitazione
~~~~~~~~~~~~~~~~~~~

E' il tempo in secondi che il sistema attende tra una digitazione e l'altra.

Richiedi Conferma
~~~~~~~~~~~~~~~~~

Permette di avere una conferma prima della richiesta della password, serve per chi utilizza linee che sembrano rispondere immediatamente.

ID Chiamante
~~~~~~~~~~~~

L'ID chiamante che avrà l'utente utilizzando la DISA, è opzionale. Il formato è "Nome Utente".

Contesto
~~~~~~~~

Indicare il contesto di Asterisk da cui partiranno le chiamate. Le chiamate da telefoni interni partono di default da from-internal.

Permetti Riaggancio
~~~~~~~~~~~~~~~~~~~

Consente di effettuare più chiamate una volta entrati nella DISA permettendo di riagganciare la linea e comporre un nuovo numero. Di default il codice per il riaggancio è \*.

.. _seguimi_ref_label:

Seguimi
=======

Descrizione
-----------

Il modulo Seguimi, o FollowMe, ha lo scopo di personalizzare il comportamento del |product| quando viene chiamato un interno, che sia sip, iax o dahdi.

Di default il Seguimi è disattivato, di conseguenza il |product| quando viene chiamato un interno si comporta con la modalità standard, cioè fa squillare l'interno per il tempo di squillo configurato nei dettagli dell'interno e se non c'è stata risposta o chiude la chiamata o la devia alla :ref:`Casella Vocale <casella_vocale_ref_label>` se attiva.

Il Seguimi quindi deve essere utilizzato per modificare il default ed ottenere il comportamento voluto.

Le possibilità sono innumerevoli ovviamente, si può, ad esempio, far compiere al |product| altre operazioni se la chiamata fallisce configurandole in destinazione se nessuna risposta.

Oppure si può quando viene chiamato l'interno, far squillare altri interni secondo varie :ref:`strategie di squillo <strategie_squillo_ref_label>`.

Il caso tipico, di solito, si ha quando più interni corrispondono ad un'unica utenza, ad esempio telefono fisso e cordless, e quindi si vuole farli squillare come se fossero un interno singolo, dando poi all'utente la possibilità di scegliere da quale apparecchio rispondere e magari considerare occupati tutti gli interni se uno è utilizzato.

Configurazione
--------------

Disattivato
~~~~~~~~~~~

Se selezionato il Seguimi è disattivato. La chiamata quindi sarà diretta all'interno seguendo la configurazione di default.

Tempo iniziale di squillo
~~~~~~~~~~~~~~~~~~~~~~~~~

Numero di secondi di squillo dell'interno primario prima di procedere con il Seguimi e quindi con le configurazioni della Lista Seguimi dove può essere inserito anche l'interno primario.

Per saltare questo e andare direttamente alla Lista Seguimi configurare zero.

Strategia di Squillo
~~~~~~~~~~~~~~~~~~~~

Strategia di squillo degli interni indicati nella Lista Seguimi. Per maggiori dettagli vedi :ref:`qui <strategie_squillo_ref_label>`.

Tempo di squillo
~~~~~~~~~~~~~~~~

Tempo di squillo in secondi degli interni indicati nella Lista Seguimi. Il massimo indicabile è 60 secondi.

Per la strategia di squillo hunt equivale al tempo di ogni singolo interno.

Lista Seguimi
~~~~~~~~~~~~~

Inserire qui gli interni da chiamare, uno per riga, può essere d'aiuto la selezione veloce subito sotto.

Se è necessario inserire un numero esterno, inserirlo con il # finale, ricordarsi di inserire anche il prefisso di chiamata se previsto nelle :ref:`Rotte in Uscita <Rotte_in_uscita_ref_label>`.

Ad esempio per chiamare 0721405516, inserire 0721405516# o se previsto come prefisso in uscita 0 inserire 00721405516#

Selezione Veloce Interno
~~~~~~~~~~~~~~~~~~~~~~~~

Selezione veloce di un interno da aggiungere alla Lista Seguimi dall'elenco degli interni disponibili.

Annuncio
~~~~~~~~

Messaggio audio da riprodurre al chiamante prima di entrare nel Seguimi, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Riproduci Musica di Attesa
~~~~~~~~~~~~~~~~~~~~~~~~~~

Se si seleziona una classe di :ref:`Musica di Attesa <musiche_di_attesa_ref_label>` invece di Squillo, al chiamante mentre è in attesa di risposta verrà fatta ascoltare questa invece del suono di squillo.

Prefisso ID Chiamante
~~~~~~~~~~~~~~~~~~~~~

Inserendo questo campo si aggiunge un prefisso all'id chiamante che verrà poi visualizzato sui telefoni che riceveranno la chiamata, serve a individuare che il telefono sta suonando per una chiamata entrata in questo Seguimi.

Ad esempio se si inserisce "Commerciale:" e si riceve una chiamata da un numero abbinato dal |product| ad un contatto, sul display del telefono che squilla verrà visualizzato "Commerciale:Contatto".

Alert Info
~~~~~~~~~~

Selezionando un Alert Info è possibile modificare la suoneria dei telefoni ip che suoneranno per una chiamata che è entrata in questo Seguimi vedi anche :ref:`qui <suoneria_differenziata_ref_label>`.

Configurazione Conferma di Chiamata
-----------------------------------

Conferma Chiamate
~~~~~~~~~~~~~~~~~

Attivare questa opzione se nella Lista Seguimi ci sono dei numeri esterni che hanno bisogno di conferma.

Ad esempio se è stato inserito un cellulare potrebbe andare in segreteria se occupato e/o non raggiungibile, e in quel caso la chiamata sarà persa.

Attivando questa opzione l'utente remoto dovrà digitare 1 sul proprio telefono per accettare la chiamata.

Questa opzione funziona solo con strategie di squillo ringall e ringall-prim.

Annuncio Remoto
~~~~~~~~~~~~~~~

Il messaggio da riprodurre alla persona che riceve la chiamata se è stato attivato Conferma Chiamate, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Annuncio Troppo-Tardi
~~~~~~~~~~~~~~~~~~~~~

Il messaggio da riprodurre alla persona che riceve la chiamata se la chiamata è stata già accettata prima di premere il tasto, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Modifica Configurazione Rotta in Ingresso
-----------------------------------------

Modalità
~~~~~~~~

*  **Predefinito** Invia il numero Chiamante se permesso dal Fascio, vedi :ref:`qui <fasci_sip_ref_label>` ad esempio.
*  **Fissa il Numero Chiamante** Invia sempre il numero Chiamante forzato.
*  **Numero Chiamante fissato per le chiamate Esterne** Invia il numero Chiamante forzato solo per le chiamate esterne, quelle interne si comportano normalmente.
*  **Utilizza il Numero Chiamato** Invia il numero che è stato composto come CID per le chiamate provenienti dall'esterno. Le chiamante interne si comportano normalmente. E' necessaria una :ref:`Rotta in Entrata <rotte_in_entrata_ref_label>` per questo numero.
*  **Forza il Numero Chiamato** Invia il numero che è stato composto come CID per le chiamate provenienti dall'esterno. Le chiamate interne si comportano normalmente.

Fissa il Numero Chiamante
~~~~~~~~~~~~~~~~~~~~~~~~~

Valore fisso per il numero Chiamante con alcune delle modalità configurate in Modalità.

Destinazione se nessuna risposta
--------------------------------

Destinazione della chiamata se non è ottenuto risposta per varie ragioni, sia perché è scaduto il tempo massimo di squillo che tutti gli interni indicati sono occupati, etc..

.. _ivr_ref_label:

IVR
===

Descrizione
-----------

Un IVR (Interactive Voice Responce) è un modulo di |product| che serve a permettere al chiamante di interagire nella chiamata effettuando delle scelte da tastiera.

E' di solito consiste in un messaggio audio che illustra le possibilità di scelta al chiamante e dal |product| che resta in ascolto dell'input del chiamante per poi riconoscerlo e comportarsi come è stato configurato.

Gli IVR possono essere infinitamente concatenati, cioè la scelta di un
IVR può far entrare in un altro IVR e così via...

.. warning:: Essendo slegato quello che spiega il messaggio audio dalle funzionalità configurate sul |product|, l'IVR è uno strumento molto potente in quanto può consentire funzionalità non annunciate o al chiamante può essere nascosto di trovarsi in un IVR consentendo le scelte solo a chi ne è al corrente.
 Ad esempio la chiamata può entrare in un IVR che annuncia solo le scelte 1,2,3 ma poi effettivamente il |product| è configurato anche per accettare le scelte 7,8,9 o ancora la chiamata entra in un IVR dove l'annuncio da il benvenuto ma non dice di fare scelte mentre il |product| è configurato per gestirle.

Configurazione
--------------

Nome IVR
~~~~~~~~

Questo campo definisce il nome, visibile sulla destra, di questo IVR.

Descrizione IVR
~~~~~~~~~~~~~~~

Descrizione di questo IVR

Opzioni IVR(DTMF)
-----------------

Annuncio
~~~~~~~~

:ref:`Registrazione di Sistema <registrazioni_di_sistema_ref_label>` da riprodurre quando si entra in questo IVR.

Chiamata Diretta
~~~~~~~~~~~~~~~~

Consente al chiamante di contattare direttamente gli interni, digitandone il numero. Può essere attiva sugli interni o disattivata.

Timeout
~~~~~~~

Il tempo in secondi dopo la riproduzione dell'annuncio che il |product| aspetterà una scelta del chiamante, per poi andare dopo aver esaurito i tentativi previsti, al messaggio di timeout, se configurato, e alla destinazione su timeout.

Tentativi su Invalido
~~~~~~~~~~~~~~~~~~~~~

Quante possibilità dare al chiamante se inserisce una scelta non prevista o non valida.

Messaggio Riprova su Opzione non Valida
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Messaggio da riprodurre al chiamante quando ha digitato una opzione non prevista o non valida, di solito per invitarlo a fare una scelta corretta.

Accoda Annuncio Originale
~~~~~~~~~~~~~~~~~~~~~~~~~

Se selezionato dopo aver riprodotto il messaggio di Opzione non valida il |product| ripeterà l'annuncio dell'IVR.

Messaggio su Destinazione non valida
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Messaggio da riprodurre al chiamante dopo che ha inserito una opzione non valida per il numero massimo dei tentativi consentiti.

Destinazione su Opzione non Valida
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata dopo che il messaggio su Destinazione non valida è stato riprodotto.

Tentativi su Timeout
~~~~~~~~~~~~~~~~~~~~

Numero di ripetizioni dell'annuncio dell'IVR dopo che è scattato il timeout in quanto il |product| non ha intercettato nessun tono DTMF.

Messaggio Riprova su Timeout
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Messaggio da riprodurre quando scatta il timeout dell'IVR.

Accoda Annuncio Originale
~~~~~~~~~~~~~~~~~~~~~~~~~

Se selezionato l'annuncio dell'IVR verrò riprodotto dopo il messaggio di riprova su timeout.

Messaggio Timeout
~~~~~~~~~~~~~~~~~

Messaggio da riprodurre al chiamante dopo che si sono esauriti i tentativi di timeout e il |product| non ha comunque intercettato toni DTMF.

Destinazione su Timeout
~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata dopo aver riprodotto il messaggio di timeout.

Ritorna all'IVR dopo Voicemail
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato, una chiamata entrata nell'IVR che ha avuto come esito una casella vocale, dopo aver lasciato il messaggio rientrerà nell'IVR per avere la possibilità di effettuare una scelta diversa.

Opzioni IVR
-----------

Per ogni opzione specificare la scelta del chiamante in INT, può essere un qualsiasi valore numerico di qualsiasi numero di cifre, e in Destinazione dove il |product| deve dirigere la chiamata.

Con il pulsante + è possibile aggiungere una opzione, per eliminarla cliccare sul pulsante elimina (bidone).

Selezionando Ritorna si da la possibilità di tornare su un IVR parente in caso di concatenazione di più IVR.

.. _destinazioni_varie_ref_label:

Destinazioni Varie
==================

Descrizione
-----------

Il modulo Destinazioni Varie ha lo scopo di creare come destinazione per gli altri moduli di |product| la chiamata verso un numero esterno o interno.

Quando il flusso della chiamata arriva ad una Destinazione Varia è come se si chiamasse il numero indicato da un interno.

Se si vuole creare una destinazione che possa essere utilizzata anche dagli interni usare il modulo :ref:`Applicazioni Varie <applicazioni_varie_ref_label>`.

Configurazione
--------------

Descrizione
~~~~~~~~~~~

Campo descrittivo per individuare la Destinazione creata.

Chiama
~~~~~~

Inserire qui il numero da chiamare in questa Destinazione. La chiamata verrà fatta come se si trattasse di una chiamata fatta da un interno.

.. _numeri_brevi_ref_label:

Numeri Brevi
============

Descrizione
-----------

Il modulo Numeri Brevi serve a configurare delle scorciatoie per chiamare i numeri telefonici più frequentemente contattati, in modo tale da non dover ogni volta digitare l'intero numero.

Digitando il codice dei Numeri Brevi, di default 99 ma è modificabile :ref:`qui <codici_servizi_ref_label>`, seguito dal numero breve assegnato al contatto, il |product| chiamerà il numero telefonico associato al contatto.

E' anche possibile selezionare un ordine dei Fasci da utilizzare per effettuare la chiamata che non sia quello delle :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` come se fosse una qualsiasi chiamata ma che sia riservato ai soli Numeri Brevi.

Il modulo Numeri Brevi può anche essere utilizzato semplicemente per aggiungere dei contatti alla rubrica del |product|, tutti i Numeri Brevi inseriti sono inclusi di default nella rubrica di |product|.

Utilizzando il menù di sinistra si può esportare i contatti presenti nei Numeri brevi in formato csv e importare nel modulo Numeri Brevi dei contatti sempre da file csv.

Il formato del file deve essere: ::

  Nome,Numero,Numero Breve

In ogni riga deve esserci un solo contatto.

Configurazione
--------------

Entrando nel modulo Numeri Brevi si ha innanzitutto la possibilità di avere l'elenco dei Numeri Brevi già inseriti, completo o diviso per iniziale.

E' inoltre possibile modificare i contatti già inseriti o cancellarli.

Trunk Sequence
--------------

In questa parte si può configurare l'ordine con cui il |product| tenterà di usare i fasci sip e/o iax e/o dahdi e/o zap e/o virtuali per effettuare la chiamata verso i Numeri Brevi. Il |product| scalerà da un fascio all'altro seguendo l'ordine di inserimento se il primo fascio risulterà occupato in altre conversazioni, non disponibile o non registrato.

Se non viene indicato nessun Fascio verranno utilizzate le regole delle :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

Questa possibilità di differenziare per i Numeri Brevi le politiche in uscita serve a consentire di bypassare eventuali regole di blocco solo e soltanto per i Numeri Brevi.

Campi della procedura di inserimento di un Numero Breve
-------------------------------------------------------

Nome Contatto
~~~~~~~~~~~~~

Campo anagrafico per individuare il contatto.

Numero di Telefono
~~~~~~~~~~~~~~~~~~

Il numero di telefono che sarà chiamato dal |product| se utilizzato il Numero Breve.

Numero Breve
~~~~~~~~~~~~

Numero da utilizzare dopo il codice per i Numeri Brevi per individuare il contatto e chiamarlo. Deve essere di almeno due cifre.

.. _paging_e_intercom_ref_label:

Paging e Intercom
=================

Descrizione
-----------

Il Paging è una funzionalità di |product| che consente di instaurare una chiamata verso un gruppo di interni direttamente sul loro vivavoce, senza che debbano rispondere.

Per il Paging è richiesto che il telefono coinvolto supporti questa funzionalità (Yealink, Snom, Grandstream e le principali marche di telefoni sip lo fanno) e che il Paging sia attivo.

Il Paging ha diverse modalità, può essere forzato su un interno occupato, silenzioso, con l'audio solo in un verso o in entrambi.

Di solito viene usato per dare comunicazioni su altoparlanti, megafoni etc.. dove è necessario far partire l'audio direttamente senza attendere la risposta dell'interno chiamato.

Configurazione
--------------

Interno Paging
~~~~~~~~~~~~~~

Indicare un numero, preferibilmente di almeno 3 cifre in modo da non avere sovrapposizioni con i :ref:`codici servizi <codici_servizi_ref_label>`, che sarà quello da chiamare per utilizzare il Paging.

Descrizione Gruppo
~~~~~~~~~~~~~~~~~~

Descrizione del Gruppo di Page per riconoscerlo tra gli altri.

Lista Apparati
~~~~~~~~~~~~~~

Selezionare tra gli interni i membri del Gruppo di Page, cioè gli interni che saranno chiamati digitando l'interno di Paging.

Utilizzare il tasto Ctrl per delle selezioni multiple.

Interni Occupati
~~~~~~~~~~~~~~~~

Stabilire come il |product| deve comportarsi in caso di interno occupato.

*  **Salta** ignora gli interni che sono occupati lasciando il Paging solo per quelli liberi.
*  **Forza** non controlla se gli interni sono occupati e fa partire il Paging su tutti i membri del gruppo, a seconda delle configurazioni dell'interno e del telefono una eventuale comunicazione in corso potrebbe essere interrotta o messa in attesa.
*  **Silenziosa** per gli interni occupati il |product| cerca di effettuare una intromissione sulla chiamata senza che il chiamante remoto possa sentire nulla. A seconda delle funzionalità del telefono se questa operazione fallisce non verrà fatto nessun Paging.

Duplex
~~~~~~

Il Paging ha di solito l'audio in sola andata, per gli annunci, selezionando questa opzione invece l'audio sarà bidirezionale come se si trattasse di una conferenza istantanea.

Gruppo Page Predefinito
~~~~~~~~~~~~~~~~~~~~~~~

|product| può avere un gruppo di Paging predefinito. Selezionando questa opzione si potrà aggiungere o togliere interni dal gruppo con i codici predefiniti. Se esiste già un gruppo predefinito spuntando questa opzione verrà tolta dal precedente gruppo.

.. _parcheggi_ref_label:

Parcheggi
=========

Descrizione
-----------

Il modulo Parcheggi di |product| permette di mettere in attesa una chiamata, parcheggiare, non sul proprio telefono ma sul centralino, questo perché questa chiamata deve essere poi ripresa non da chi la ha parcheggiata ma da un altro interno.

Attivando il parcheggio il |product| crea un interno di Parcheggio, a cui trasferire le chiamate per parcheggiarle, ed un numero di parcheggi dove le chiamate resteranno in attesa.

Parcheggiando una chiamata trasferendola all'interno di Parcheggio, il |product| risponderà con l'interno dove è stata parcheggiata. A questo punto basterà chiamare questo interno per prendere la chiamata.

L'uso tipico si ha quando la centralinista dopo aver ricevuto una chiamata non sa dove trasferirla perché non c'è una corrispondenza tra interni e persone e quindi parcheggia la chiamata e annuncia all'interessato magari usando un altoparlante che c'è una chiamata all'interno di parcheggio che il centralino le ha fornito. Per prendere la chiamata quindi, l'interessato dovrà chiamare da un qualsiasi telefono l'interno del parcheggio.

Configurazione
--------------

Attiva Parcheggio Chiamate
~~~~~~~~~~~~~~~~~~~~~~~~~~

Spuntare l'opzione per attivare il parcheggio.

Interno Parcheggio
~~~~~~~~~~~~~~~~~~

L'interno a cui chiamare per attivare il parcheggio.

Numero intervallo interni
~~~~~~~~~~~~~~~~~~~~~~~~~

Numero di interni di parcheggio, in pratica il numero massimo di chiamate che si possono parcheggiare contemporaneamente. Il |product| attiverà a partire dall'interno di parcheggio il numero di interni selezionato.

Timeout Parcheggio
~~~~~~~~~~~~~~~~~~

Il timeout di default prima di far ritornare una chiamata parcheggiata alla destinazione specificata, interno che l'ha parcheggiata o altro.

Classe Musica di Attesa
~~~~~~~~~~~~~~~~~~~~~~~

La classe di musica di attesa che verrà riprodotta a una chiamata parcheggiata salvo precedenti configurazioni nel flusso della chiamata.

Contesto Parcheggio
~~~~~~~~~~~~~~~~~~~

Contesto di Asterisk a cui far appartenere le chiamate parcheggiate.

Abilita Gestione campo Lampade
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitando questa scelta il |product| crea degli hints BLF per gli interni di parcheggio, rendendoli monitorabili ad esempio dai tasti lampade dei telefoni ip.

Utilizza il prossimo Slot
~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitando questa funzionalità la chiamata verrà parcheggiata nell'interno successivo al precedente e non sul primo disponibile. Serve a dare continuità numerica ai parcheggi.

Abilita Annunci ADSI
~~~~~~~~~~~~~~~~~~~~

Seleziona questa funzionalità se si utilizzano dei telefoni analogici abilitati ADSI.

Comportamento Ritorno Chiamata
------------------------------

Tono su Pickup
~~~~~~~~~~~~~~

Tono da riprodurre quando una chiamata viene recuperata.

Capacità di Trasferimento
~~~~~~~~~~~~~~~~~~~~~~~~~

Abilita o disabilita il trasferimento della chiamata tramite :ref:`DTMF <funzionalita_base_ref_label>` una volta ripresa la chiamata dal parcheggio.

Capacità di RiParcheggio
~~~~~~~~~~~~~~~~~~~~~~~~

Abilita o disabilita i toni DTMF per parcheggiare di nuovo una chiamata presa dal parcheggio.

Registrazione audio su Richiesta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilita o disabilita i toni DTMF per registrare l'audio della chiamata ripresa dal parcheggio.

Chiusura chiamata con DTMF
~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilita o disabilita i toni DTMF per chiudere la chiamata una volta presa dal parcheggio.

Alert-info Parcheggio
~~~~~~~~~~~~~~~~~~~~~

Alert-info da aggiungere alla chiamata. Serve a modificare la suoneria, vedi :ref:`qui <suoneria_differenziata_ref_label>`.

Prefisso ID Chiamante
~~~~~~~~~~~~~~~~~~~~~

Stringa da aggiungere all'ID Chiamante della chiamata parcheggiata prima di inoltrarla all'origine o su altra destinazione(timeout).

Annuncio
~~~~~~~~

Messaggio da riprodurre al chiamante prima di riportarlo all'origine o su altra destinazione(timeout).

Destinazione Alternativa
------------------------

Comportamento Destinazione di Ritorno
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata parcheggiata dopo il timeout. La chiamata può tornare a chi l'ha parcheggiata od una destinazione alternativa da selezionare qui. In entrambi i casi si attivano verranno attivate le configurazioni attivate sopra. Se chi ha parcheggiato la chiamata non è disponibile, verrà utilizzata la destinazione alternativa.

.. _code_ref_label:

Code
====

Descrizione
-----------

Le Code sono uno dei due modi per |product|, l'altro sono i :ref:`Gruppi di Chiamata <gruppi_di_chiamata_ref_label>`, per distribuire una chiamata verso più interni.

Le Code a differenza dei :ref:`Gruppi di Chiamata <gruppi_di_chiamata_ref_label>` sono uno strumento professionale per gestire la chiamata in ingresso, offrendo numerose possibilità e funzionalità accessorie, comunque una Coda configurata minimamente ha le funzionalità dei :ref:`Gruppi di Chiamata <gruppi_di_chiamata_ref_label>`.

Queste potenzialità vengono dal fatto che a differenza dei :ref:`Gruppi di Chiamata <gruppi_di_chiamata_ref_label>`, la chiamata in ingresso nella Coda rimane sul |product|, ed è il centralino che contatta i vari interni secondo le politiche configurate e attiva le varie funzionalità della Coda.

La Coda quando configurata diventa un vero e proprio oggetto del |product|, gli viene associato un numero e a questo numero può essere contattata.

Le Code inoltre hanno tutta una reportistica dedicata per valutarne le performance e analizzarne le statistiche, vedi :doc:`qui <report_code>`.

Configurazione
--------------

Coda Numero
~~~~~~~~~~~

Numero da assegnare alla Coda. E' consigliato utilizzare un numero a tre cifre per non sovrapporsi ad esempio ai :ref:`Codici Servizi <codici_servizi_ref_label>`. Chiamare questo numero per entrare in Coda o trasferire i chiamanti in questa Coda. Gli agenti della Coda dovranno chiamare questo numero seguito da \* per entrare nella Coda, seguito da \*\* per uscirne.

Ad esempio se la coda è la 401:

*  401\* per entrare
*  401\** per uscire

Nome Coda
~~~~~~~~~

Campo descrittivo della Coda, per facilitarne l'individuazione.

Password Coda
~~~~~~~~~~~~~

Se configurata verrà chiesta agli agenti che tentano di loggarsi alla Coda. Deve essere numerica.

Genera Hints per Apparati
~~~~~~~~~~~~~~~~~~~~~~~~~

Se selezionato verranno creati degli hint individuali per ogni interno che fa parte della Coda. E' utilizzabile come BLF sui telefoni per avere un pulsante per login e logout dalla Coda e generare i BLF di stato relativi alla Coda.

Il formato è ::

  *45INTERNO*CODA

dove \*45 è il codice funzione per il login e logout (valore di default configurabile nei :ref:`Codici Servizi <codici_servizi_ref_label>`), INTERNO è il numero dell'interno, CODA è il numero della coda.

Conferma Chiamata
~~~~~~~~~~~~~~~~~

Attivare questa opzione se tra gli agenti ci sono dei numeri esterni o degli interni con il :ref:`Seguimi <seguimi_ref_label>` attivato o eventuali chiamate trasferite su numeri esterni.

Ad esempio se è stato inserito un cellulare potrebbe andare in segreteria se occupato e/o non raggiungibile, e in quel caso la chiamata sarà persa.

Attivando questa opzione l'utente remoto dovrà digitare 1 sul proprio telefono per accettare la chiamata.

Annuncia Conferma Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~

Annuncio riprodotto agli agenti con Conferma attivata nella Coda per notificare la chiamata e fornire informazioni prima di rispondere. Se impostato a Default verrà riprodotto il messaggio standard di conferma a meno che un agente non abbia il :ref:`Seguimi <seguimi_ref_label>` e su questo ci sia un messaggio alternativo.

Nome Prefisso Identificativo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserendo questo campo si aggiunge un prefisso all'id chiamante che verrà poi visualizzato sui telefoni che riceveranno la chiamata, serve a individuare che il telefono sta suonando per una chiamata entrata in questa Coda.

Ad esempio se si inserisce "Commerciale:" e si riceve una chiamata da un numero abbinato dal |product| ad un contatto, sul display del telefono che squilla verrà visualizzato "Commerciale:Nome".

Prefisso Tempo di Attesa
~~~~~~~~~~~~~~~~~~~~~~~~

Se abilitato l'ID Chiamante avrà come prefisso il tempo di attesa totale nella Coda, così che l'agente che risponde potrà sapere subito quanto ha aspettato il chiamante. Sarà arrotondato al minuto nella forma Mnn dove nn rappresenta il numero di minuti. Se la chiamata è stata trasferita da un agente all'altro il tempo di attesa sarà sempre quello da quando la chiamata è entrata in coda a meno che non sia variata anche la Coda.

Alert Info
~~~~~~~~~~

Selezionando un Alert Info è possibile modificare la suoneria dei telefoni ip che suoneranno per una chiamata che è entrata in questa Coda vedi anche :ref:`qui <suoneria_differenziata_ref_label>`.

Agenti Statici
~~~~~~~~~~~~~~

Gli agenti statici sono interni che si intendono sempre attivi come membri di una Coda, non hanno bisogno di login/logout. Inserire gli interni uno per riga, è possibile inserire interni di sistemi remoti o numeri esterni come ad esempio un cellulare. Opzionalmente è possibile inserire la penalità separata dalla virgola, che può essere usata in particolari :ref:`Strategie di Squillo <strategie_squillo_ref_label>`. La penalità è crescente, un agente con penalità più alta suonerà dopo un agente con penalità più bassa.

Ad esempio: 

::

  201,2
  202,3
  203,2
  204,1

Con la :ref:`Strategie di Squillo <strategie_squillo_ref_label>` squillano tutti suonerà il primo agente disponibile con la priorità più bassa, quindi 204 poi eventualmente 201 e 203 e infine 202.

Selezione Veloce Interno
~~~~~~~~~~~~~~~~~~~~~~~~

Selezione veloce di un interno da aggiungere alla Coda come agente statico dall'elenco degli interni disponibili.

Membri Dinamici
~~~~~~~~~~~~~~~

I membri dinamici della Coda sono interni che possono fare login/logout nella Coda. Le penalità possono essere indicate come per gli agenti statici e applicate nel momento del login. Gli interni qui elencati non saranno loggati nella coda automaticamente.

Selezione Veloce Interno
~~~~~~~~~~~~~~~~~~~~~~~~

Selezione veloce di un interno da aggiungere alla Coda come agente dinamico dall'elenco degli interni disponibili.

Solo Agenti Dinamici
~~~~~~~~~~~~~~~~~~~~

Restringe gli agenti dinamici ai soli interni indicati in membri dinamici se attivata, dando un messaggio di accesso negato a chi proverà a loggarsi nella Coda non essendo in elenco.

Restrizioni Agenti
~~~~~~~~~~~~~~~~~~

Selezionare come la Coda deve contattare gli agenti

*  **Chiama come Digitato** gli agenti verranno contattati come se fosse una chiamata interna. La chiamata quindi seguirà eventuali :ref:`Seguimi <seguimi_ref_label>` o inoltri impostati. E' il comportamento standard.
*  **Blocca Seguimi o Inoltro Chiamata** tutti gli agenti interni verranno contattati solo al loro interno, verranno ignorati inoltri o :ref:`Seguimi <seguimi_ref_label>`, i numeri esterni saranno contattati come digitati
*  **Solo Interni** la Coda chiamerà gli agenti interni secondo la regola Blocca Seguimi o Inoltro Chiamata, tutti gli altri numeri verranno ignorati

Opzioni Generali Coda
---------------------

Strategia di squillo
~~~~~~~~~~~~~~~~~~~~

Vedi :ref:`qui <strategie_squillo_ref_label>`.

Auto-completamento (Autofill)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attivando questa opzione se si ha più di un agente libero, ogni singola chiamata viene inviata ai singoli agenti liberi secondo la strategia di squillo selezionata. Se disattivata tutte le chiamate vengono messe in attesa finché la prima chiamata in Coda non viene risposta.

Salta Agenti Occupati
~~~~~~~~~~~~~~~~~~~~~

Configurare come la Coda deve trattare gli agenti occupati, se saltarli e in che modo.

-  **No** gli agenti occupati non saranno saltati, se si tratta di interni con l':ref:`Avviso di Chiamata <funzionalita_base_ref_label>` attivo ad esempio suoneranno.
-  **Si** gli agenti occupati verranno saltati. Questo significa che eventuali interni con l':ref:`Avviso di Chiamata <funzionalita_base_ref_label>` attivo se al telefono su una linea verranno comunque considerati occupati.
-  **Si + (ringinuse=no)** gli agenti occupati verranno saltati in più verrà settato il parametro ringinuse a no per la Coda, che comporta che verranno trattati alla stessa maniera gli agenti esterni, collegati da remoto o attraverso il :ref:`Seguimi <seguimi_ref_label>`, così che la Coda non invierà una chiamata a questi interni se occupati.
-  **Solo chiamate in coda (ringinuse=no)** gli agenti che appartengono a più Code verranno considerati raggiungibili solo da una chiamata proveniente da qualsiasi Coda alla volta.

Peso Coda (Weight)
~~~~~~~~~~~~~~~~~~

E' possibile configurare un peso per ogni Coda, in modo tale che ad un agente loggato su due Code vengano smistate prima le chiamate della Coda con il peso più alto.

Classe Musica di Attesa
~~~~~~~~~~~~~~~~~~~~~~~

La :ref:`Musica di Attesa <musiche_di_attesa_ref_label>` da riprodurre al chiamante mentre resta in attesa. Lasciare eredita se è già stata impostata in un modulo precedente, ad esempio nelle :ref:`Rotte in Entrata <rotte_in_entrata_ref_label>`.

Squillo invece che Musica
~~~~~~~~~~~~~~~~~~~~~~~~~

Attivare l'opzione per dare un tono di libero ai chiamanti in attesa e non una :ref:`Musica di Attesa <musiche_di_attesa_ref_label>`. Se attivato anche gli annunci periodici verranno ignorati.

Annuncio Raggiungimento
~~~~~~~~~~~~~~~~~~~~~~~

L'annuncio da riprodurre al chiamante prima di entrare in Coda, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Registra chiamate
~~~~~~~~~~~~~~~~~

Le chiamate entranti nella Coda possono essere registrate ed è possibile sceglierne il formato audio tra wav, wav49 e gsm.

Modalità Registrazione
~~~~~~~~~~~~~~~~~~~~~~

Se è stata attivata la registrazione è possibile scegliere se la registrazione deve includere il tempo di attesa o deve partire quando la chiamata viene risposta.

Aggiustamento volume chiamante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se è stata attivata la registrazione è possibile modificare il volume di registrazione del chiamante aumentandolo o diminuendolo.

Aggiustamento volume Agente
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se è stata attivata la registrazione è possibile modificare il volume di registrazione dell'agente aumentandolo o diminuendolo.

Marca chiamate risposte altrove
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato le chiamate risposte da altri agenti non saranno visualizzate sul telefono come perse, il telefono deve supportare la funzionalità.

Tempi e Opzioni Agente
----------------------

Tempo Massimo di Attesa
~~~~~~~~~~~~~~~~~~~~~~~

Il tempo massimo in secondi che un chiamante deve restare in attesa di risposta una volta entrato nella Coda, configurare 0 per illimitato

Modalità Tempo Massimo di Attesa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Modalità di calcolo del tempo massimo di attesa

*  **Strict** se configurato allo scadere del tempo massimo la chiamata viene fatta uscire dalla Coda
*  **Rilassato** se configurato se una chiamata arriva al tempo massimo di attesa e c'è almeno un agente il cui telefono sta squillando, l'attesa viene prolungata per il tempo di timeout agente

Timeout Agenti
~~~~~~~~~~~~~~

Numero di secondi che il telefono dell'agente suona prima di essere considerato irraggiungibile. L'opzione può essere entrare in conflitto con il :ref:`tempo di squillo predefinito <impostazioni_generali_ref_label>` o con le impostazioni dell':ref:`interno <interni_sip_ref_label>`.

Pausa su Timeout
~~~~~~~~~~~~~~~~

Se attivato gli agenti considerati irraggiungibili, quindi per i quali una chiamata è andata in timeout, verranno messi forzatamente in pausa o solo per la Coda interessata o per tutte le Code in cui sono collegati.

Timeout su Riavvio Agenti
~~~~~~~~~~~~~~~~~~~~~~~~~

Se abilitato il timeout agente verrà resettato se si riceve un Occupato o Rifiuto. Utile se gli agenti possono rifiutare una chiamata.

Riprova la chiamata dopo
~~~~~~~~~~~~~~~~~~~~~~~~

Il numero di secondi di attesa prima di riprovare a contattare tutti gli agenti. Scegliendo "Non Riprovare" la chiamata, se il primo tentativo non ha ottenuti risposte, uscirà dalla Coda.

Wrap-Up-Time
~~~~~~~~~~~~

Numero di secondi che occorre aspettare prima di considerare libero un agente che ha appena chiuso una chiamata. Il default è 0, nessun ritardo.

Ritardo Membri
~~~~~~~~~~~~~~

Numero di secondi di ritardo prima che l'agente sia collegato con il chiamante o ascolti l'annuncio agente.

Annuncio Agente
~~~~~~~~~~~~~~~

Annuncio riprodotto prima che l'agente si colleghi con il chiamante, serve di solito a specificare all'agente da che Coda arriva la chiamata, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Riporta Tempo di attesa
~~~~~~~~~~~~~~~~~~~~~~~

Attivare questa opzione se si desidera comunicare all'agente il tempo di attesa del chiamante prima di collegarli in comunicazione.

Capacità Opzioni
----------------

Num. Massimo Chiamanti
~~~~~~~~~~~~~~~~~~~~~~

Il numero massimo i chiamate che possono stare in attesa nella Coda, 0 per illimitato.

Raggiungi coda vuota
~~~~~~~~~~~~~~~~~~~~

Politica per la gestione delle nuove chiamate in arrivo nella Coda. Le possibilità sono:

*  **Si** permetti alle chiamate di entrare in coda anche quando non ci sono agenti loggati o sono tutti in pausa.
*  **No** le chiamate non entreranno in Coda se non ci sono agenti loggati nella Coda.
*  **Strict** stesso comportamento di **Si** ma più restrittivo, la chiamata viene ammessa se ci sono agenti in grado di rispondere, quindi attivi, magari occupati in altre chiamate al momento, altrimenti viene rifiutata.
*  **Molto Stringente** come **Strict** ma l'agente deve essere in grado di rispondere subito, deve esserci quindi almeno un agente libero, altrimenti la chiamata viene rifiutata.
*  **Rilassato** come **No** ma la chiamata viene ammessa se ci sono agenti in pausa che potrebbero tornare disponibili.

Lascia quando coda vuota
~~~~~~~~~~~~~~~~~~~~~~~~

Politica per le chiamate potenzialmente uscenti dalla Coda. Le possibilità sono:

*  **Si** i chiamanti usciranno se non ci sono agenti loggati nella Coda o sono tutti in pausa.
*  **No** i chiamanti non usciranno mai dalla Coda se non alla scadenza del tempo massimo di attesa.
*  **Strict** come **Si** ma più restrittivo, la chiamata rimane in Coda solo se ci sono agenti in grado di rispondere, quindi attivi, non importa se occupati al telefono, altrimenti la chiamata lascia la Coda.
*  **Molto Stringente** come **Strict** ma la chiamata rimane in Coda solo se ci sono agenti in grado di rispondere subito, deve esserci quindi almeno un agente libero, altrimenti la chiamata lascia la Coda.
*  **Rilassato** come **Si** ma la chiamata rimane in Coda se ci sono agenti in pausa che potrebbero tornare disponibili.

Limite Penality Membri
~~~~~~~~~~~~~~~~~~~~~~

Può essere impostato un limite per ignorare le impostazioni di penalità se ci sono pochi agenti rispetto alle chiamate in Coda. Se selezionato gli tutti agenti con penalità minore in caso di necessità saranno equiparati.

Annuncio Posizione Chiamanti
----------------------------

Frequenza
~~~~~~~~~

Tempo in secondi della frequenza dell'annuncio di posizione e tempo di attesa stimato al chiamante. Selezionare 0 per disattivare.

Annuncio Posizione
~~~~~~~~~~~~~~~~~~

Se attivato al chiamante verrà comunicata la sua posizione in Coda secondo la frequenza configurata.

Annuncio Tempo di attesa
~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato al chiamante verrà comunicata l'attesa prevista in Coda. Può essere attivato con la frequenza configurata o una tantum. Attese sotto
il minuto non verranno comunicate.

Annunci Periodici
-----------------

Menu IVR di Uscita
~~~~~~~~~~~~~~~~~~

E' possibile durante l'attesa del chiamante nella Coda proporre un :ref:`IVR <ivr_ref_label>` che ad esempio proponga un uscita alternativa dalla Coda (in questo caso l':ref:`IVR <ivr_ref_label>` deve avere una sola opzione) o che serve semplicemente a riprodurre periodicamente un annuncio, ad esempio pubblicitario.

Frequenza di Ripetizione
~~~~~~~~~~~~~~~~~~~~~~~~

Frequenza di ripetizione del menù dell':ref:`IVR <ivr_ref_label>`, 0 per disattivarlo.

Eventi, Statistiche e Avanzate
------------------------------

Evento quando si chiama
~~~~~~~~~~~~~~~~~~~~~~~

Se attivato |product| genererà degli eventi del manager: AgentCalled, AgentDump, AgentConnect e AgentComplete.

Evento su Stato Membri
~~~~~~~~~~~~~~~~~~~~~~

Se attivato |product| genererà l'evento del manager: QueueMemberStatus.

Livello Servizio
~~~~~~~~~~~~~~~~

Usato per le Statistiche di SLA.

Filtro Regex Agenti
~~~~~~~~~~~~~~~~~~~

Permette di specificare con una espressione regolare che agenti ammettere alla Coda. Questo può essere utilizzato per restringere gli agenti ad un intervallo di interni, non permettere caratteri come \*, etc.. Vedi :ref:`qui <pattern_ref_label>` per le espressioni regolari.

Destinazione dopo fallimento
----------------------------

Destinazione della chiamata se questa esce dalla Coda per qualsiasi motivo. A seconda della configurazione della Coda può anche non avvenire mai.

.. _gruppi_di_chiamata_ref_label:

Gruppi di Chiamata
==================

Descrizione
-----------

Il Gruppo di Chiamata è uno dei due modi per |product|, l'altro sono le :ref:`Code <code_ref_label>`, per distribuire una chiamata verso più interni.

Il Gruppo di Chiamata consente una gestione elementare rispetto alle :ref:`Code <code_ref_label>`, infatti la chiamata viene elaborata e poi distribuita ai vari interni, a differenza delle :ref:`Code <code_ref_label>` dove la chiamata rimane in carico sempre al |product| e può essere gestita con molte possibilità in più.

Il Gruppo di Chiamata quando configurato diventa un vero e proprio oggetto del |product|, gli viene associato un numero e a questo numero può essere contattato.

Configurazione
--------------

Gruppo di Chiamata Numero
~~~~~~~~~~~~~~~~~~~~~~~~~

Numero da assegnare al Gruppo di Chiamata. Di default vengono proposti numeri a partire dal 600. E' consigliato mantenere un numero a tre cifre per non sovrapporsi ad esempio ai :ref:`Codici Servizi <codici_servizi_ref_label>`.

Descrizione Gruppo
~~~~~~~~~~~~~~~~~~

Campo descrittivo del Gruppo di Chiamata.

Strategia di Squillo
~~~~~~~~~~~~~~~~~~~~

Vedi :ref:`qui <strategie_squillo_ref_label>`.

Ring Time
~~~~~~~~~

Il tempo in secondi che un telefono membro del Gruppo di Chiamata squilla. In caso di strategia di squillo hunt se riferisce al tempo di squillo del singolo utente.

Lista Interni
~~~~~~~~~~~~~

Lista dei membri del Gruppo di Chiamata, uno per riga, può essere d'aiuto la selezione veloce subito sotto.

Se è necessario inserire un numero esterno, inserirlo con il # finale, ricordarsi di inserire anche il prefisso di chiamata se previsto nelle Rotte in Uscita.

Ad esempio per chiamare 0721405516, inserire 0721405516# o se previsto come prefisso in uscita 0 inserire 00721405516#

Gli interni che non hanno # alla fine non andranno al :ref:`Seguimi <seguimi_ref_label>`.

Selezione Veloce Interno
~~~~~~~~~~~~~~~~~~~~~~~~

Selezione veloce di un interno da aggiungere al Gruppo di Chiamata dall'elenco degli interni disponibili.

Annuncio
~~~~~~~~

Messaggio audio da riprodurre al chiamante prima di entrare nel Gruppo di Chiamata, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Riproduci Musica di Attesa
~~~~~~~~~~~~~~~~~~~~~~~~~~

Se si seleziona una classe di :ref:`Musica di Attesa <musiche_di_attesa_ref_label>` invece di Squillo, al chiamante mentre è in attesa di risposta verrà fatta ascoltare questa invece del suono di squillo.

Prefisso ID Chiamante
~~~~~~~~~~~~~~~~~~~~~

Inserendo questo campo si aggiunge un prefisso all'id chiamante che verrà poi visualizzato sui telefoni che riceveranno la chiamata, serve a individuare che il telefono sta suonando per una chiamata entrata in questo Gruppo di Chiamata.

Ad esempio se si inserisce "Commerciale:" e si riceve una chiamata da un numero abbinato dal |product| ad un contatto , sul display del telefono che squilla verrà visualizzato "Commerciale:Nome".

Alert Info
~~~~~~~~~~

Selezionando un Alert Info è possibile modificare la suoneria dei telefoni ip che suoneranno per una chiamata che è entrata in questo Gruppo di Chiamata vedi anche :ref:`qui <suoneria_differenziata_ref_label>`.

Ignora Impostazioni Trasf. Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato verrà ignorato per tutti gli interni membri del Gruppo di Chiamata l'attivazione di un qualsiasi tipo di :ref:`Trasferimento di Chiamata <funzionalita_base_ref_label>`.

Gli interni inseriti con il # ignorano questa opzione.

Salta Agenti Occupati
~~~~~~~~~~~~~~~~~~~~~

Se attivato i membri del Gruppo di Chiamata al telefono verranno considerati occupati anche se configurati per ricevere più chiamate contemporaneamente, ad esempio con l':ref:`Avviso di Chiamata <funzionalita_base_ref_label>`.

Abilita Pickup Chiamata
~~~~~~~~~~~~~~~~~~~~~~~

Se abilitato sarà permesso utilizzare il :ref:`Pickup Diretto <funzionalita_base_ref_label>` con il numero del Gruppo di Chiamata, se disattivato sarà possibile fare :ref:`Pickup Diretto <funzionalita_base_ref_label>` solo sugli interni.

Conferma Chiamate
~~~~~~~~~~~~~~~~~

Attivare questa opzione se nella Lista Interni ci sono dei numeri esterni che hanno bisogno di conferma.

Ad esempio se è stato inserito un cellulare potrebbe andare in segreteria se occupato e/o non raggiungibile, e in quel caso la chiamata sarà persa.

Attivando questa opzione l'utente remoto dovrà digitare 1 sul proprio telefono per accettare la chiamata.

Questa opzione funziona solo con strategie di squillo ringall.

Annuncio Remoto
~~~~~~~~~~~~~~~

Il messaggio da riprodurre alla persona che riceve la chiamata se è stato attivato Conferma Chiamate, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Annuncio Troppo-Tardi
~~~~~~~~~~~~~~~~~~~~~

Il messaggio da riprodurre alla persona che riceve la chiamata se la chiamata è stata già accettata prima di premere il tasto, vengono proposte tutte le :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Cambia Configurazione Caller ID Esterno
---------------------------------------

Modalità
~~~~~~~~

*  **Predefinito** Invia il numero Chiamante se permesso dal Fascio, vedi :ref:`qui <fasci_sip_ref_label>` ad esempio.
*  **Numero Chiamante Fissato** Invia sempre il numero Chiamante fissato.
*  **Numero Chiamante fissato per le chiamate in uscita** Invia il numero Chiamante fissato solo per le chiamate esterne, quelle interne si comportano normalmente.
*  **Usa il Numero Digitato** Invia il numero che è stato composto come CID per le chiamate provenienti dall'esterno. Le chiamante interne si comportano normalmente. E' necessaria una :ref:`Rotta in Entrata <rotte_in_entrata_ref_label>` per questo numero.
*  **Forza il Numero Digitato** Invia il numero che è stato composto come CID per le chiamate provenienti dall'esterno. Le chiamate interne si comportano normalmente.

Numero Chiamante Fissato
~~~~~~~~~~~~~~~~~~~~~~~~

Valore fisso per il numero Chiamante con alcune delle modalità configurate in Modalità.

Registrazione Chiamata
----------------------

Registra Chiamata
~~~~~~~~~~~~~~~~~

E' possibile registrare l'audio delle chiamate che entrano in questo Gruppo di Chiamata, non registrarle mai o su richiesta.

Destinazione se nessuna risposta
--------------------------------

Destinazione della chiamata se non è ottenuto risposta per varie ragioni, sia perché è scaduto il tempo massimo di squillo che tutti gli interni indicati sono occupati, etc..

Evitare di indicare il Gruppo di Chiamata stesso in modo da non creare dei circoli viziosi che potrebbero creare difficoltà al |product|.
