===========
Moduli Base
===========

.. _annunci_ref_label:

Annunci
=======

Descrizione
-----------

Gli annunci hanno lo scopo di riprodurre nel flusso della chiamata una :ref:`Registrazione di Sistema <registrazioni_di_sistema_ref_label>`.

Configurazione
--------------

Descrizione
~~~~~~~~~~~

Inserire una descrizione per individuare l'annuncio.

Registrazione
~~~~~~~~~~~~~

Scegliere tra tutte le Registrazioni di Sistema caricate sul |product|.

Ripeti
~~~~~~

Se l'annuncio prevede di essere riascoltato da parte del chiamante, selezionare qui il tasto per riascoltarlo.

Permetti Salta
~~~~~~~~~~~~~~

Per permettere al chiamante di saltare l'annuncio, spuntare qui.

Ritorna All'IVR
~~~~~~~~~~~~~~~

Se l'annuncio viene utilizzato in un IVR, spuntare qui per tornare all'IVR dopo la riproduzione dell'annuncio.

Non Rispondere al Canale
~~~~~~~~~~~~~~~~~~~~~~~~

Spuntando questa opzione non viene aperto il canale audio prima di riprodurre l'annuncio, l'apertura del canale audio causa un ritardo di circa un secondo che può non essere gradito.

Destinazione dopo la riproduzione
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Selezionare come far proseguire la chiamata tra tutte le funzionalità configurate in |product|.

.. _annunci__tts_ref_label:

Annunci TTS
===========

Descrizione
-----------

Gli annunci TTS hanno lo scopo di riprodurre nel flusso della chiamata la lettura di un testo da parte del sintonizzatore vocale.
Il file audio non viene creato al momento del salva sul modulo ma solo quando |product| ne avrà bisogno nel flusso della chiamata collegandosi 
via internet al sintonizzatore.

|product| gestisce una cache per non creare ogni volta i messaggi utilizzati più spesso che di default è di 250 MB.

Per vedere il valore di cache configurato dare il comando 

::

   config getprop nethvoice tts-maxsize

Per cambiare il valore, ad esempio a 500 MB

::

   config setprop nethvoice tts-maxsize 500
   expand-template /etc/freepbx.conf


Configurazione
--------------

Descrizione
~~~~~~~~~~~

Inserire una descrizione per individuare l'annuncio TTS.

TTS Engine
~~~~~~~~~~

Motore per la sintesi vocale, scegliere tra uno di quelli supportati

Username/Client ID
~~~~~~~~~~~~~~~~~~

Username o client ID per la connessione al motore TTS

Password
~~~~~~~~

Password per la connessione al motore TTS

Testo
~~~~~

Inserire il testo da riprodurre.

Lingua TTS
~~~~~~~~~~

La lingua del sintonizzatore vocale, non verranno fatte traduzioni del testo inserito, se non viene inserita verrà utilizzata la lingua della chiamata.

Velocità di Riproduzione TTS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La velocità di lettura del testo da parte del sintonizzatore vocale.

Ripeti
~~~~~~

Se l'annuncio prevede di essere riascoltato da parte del chiamante, selezionare qui il tasto per riascoltarlo.

Permetti Salta
~~~~~~~~~~~~~~

Per permettere al chiamante di saltare l'annuncio, spuntare qui.

Ritorna All'IVR
~~~~~~~~~~~~~~~

Se l'annuncio viene utilizzato in un IVR, spuntare qui per tornare all'IVR dopo la riproduzione dell'annuncio.

Destinazione dopo la riproduzione
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Selezionare come far proseguire la chiamata tra tutte le funzionalità configurate in |product|.

.. _interni_iax_ref_label:

Interni IAX
===========

Configurazione
--------------

Interno Utente
~~~~~~~~~~~~~~

Numero di Interno per Contattare l'utente. Utilizzare un numero univoco.

Nome visualizzato
~~~~~~~~~~~~~~~~~

L'identificativo per le chiamate provenienti da questo interno.

Alias Numero Identificativo
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il numero identificativo Chiamante per le chiamate interne, se differente dal numero interno. E' usato per mascherare un numero differente, come ad esempio per un'utente che ha due interni, magari uno fisso e un cordless, e vuole che il chiamante sia sempre lo stesso interno indipendentemente che chiami dal telefono fisso o dal telefono cordless.

Alias SIP
~~~~~~~~~

Impostare un nome da aggiungere all'interno quando viene chiamato. Serve le chiamate dirette sip interne.

Opzioni Apparato
----------------

secret
~~~~~~

Password per questo interno, deve essere almeno di 6 caratteri e contenere almeno 2 lettere e 2 numeri. 

transfer
~~~~~~~~

Capacità trasferimento IAX.

host
~~~~

Host per questo apparato, normalmente dynamic per i telefoni

type
~~~~

Tipo di configurazione lato **Asterisk** per l'interno. Normalmente friend per i telefoni.

*  **user** entità su **Asterisk** che può fare chiamate.
*  **peer** entità su **Asterisk** a cui vengono mandate le chiamate, tipicamente un Provider Voip.
*  **friend** entrambe le modalità **user** e **peer**, quindi entità in grado di fare e ricevere chiamate.

port
~~~~

Porta di utilizzo del telefono. Tipicamente la 4569 essendo IAX.

qualify
~~~~~~~

Configurato a yes si attiva l'invio periodico di un pacchetto dal |product| verso il telefono, tipicamente ogni minuto. Viene usato per monitorare lo stato del collegamento |product|-telefono e ad esempio considerare il telefono offline se il tempo di comunicazione diventa troppo elevato.

disallow
~~~~~~~~

Codecs disattivati. E' possibile indicarne anche più di uno, ad esempio ulaw&alaw o tutti con all.

allow
~~~~~

Codecs permessi. E' possibile indicarne anche più di uno, ad esempio ulaw&alaw, l'ordine indica la priorità, o tutti con all. Tutti i codecs permessi nelle :ref:`Impostazioni IAX <impostazioni_iax_ref_label>` sono permessi se non specificati in disallow.

dial
~~~~

Comando per chiamare questo interno.

accountcode
~~~~~~~~~~~

Accountcode per questo interno.

mailbox
~~~~~~~

Mailbox per questo interno.

deny
~~~~

Range di indirizzi ip dai quali non accettare accesso per questo interno. Inserire in modalità rete/maschera di rete.

permit
~~~~~~

Range di indirizzi ip dai quali accettare accesso per questo interno.  Inserire in modalità rete/maschera di rete.

requirecalltoken
~~~~~~~~~~~~~~~~

Impostazioni di sicurezza IAX.

Selezione Passante/ID assegnato
-------------------------------

Sezione per configurare una Selezione Passante che faccia suonare direttamente l'Interno.

Le Selezioni Passanti già configurate vengono elencate in fondo e cliccandoci si viene inoltrati alla :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` corrispondente.

Descrizione Selezione Passante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Descrizione della Selezione Passante diretta a questo Interno.

Aggiungi Selezione Passante
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire il numero della Selezione Passante associata a questo interno.
Deve essere nello stesso formato fornito dal gestore telefonico.

Aggiungi ID in Entrata
~~~~~~~~~~~~~~~~~~~~~~

Aggiunge un ID Chiamante per un instradamento specifico di Selezione Passante. Una Selezione Passante deve essere specificata nel box superiore. Oltre alle sequenze di chiamata standard, è possibile inserire i parametri Private, Blocked, Unknown, Restricted, Anonymous e Unavailable per catturare le chiamate nei casi speciali, se il gestore trasmette questo tipo di informazione.

Call Camp-On Services
---------------------

Gestione del servizio di Richiama su Occupato. Se nelle :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>` del Modulo Richiama su Occupato è configurato Usa le Impostazioni di default a Vero sarà possibile configurare per ogni Interno solo il Chiamante e il Chiamato.

Forcing default settings
~~~~~~~~~~~~~~~~~~~~~~~~

Se presente indica che le opzioni di default sono attivate per tutti gli interni. E' possibile cambiare questa opzione e/o le opzioni comuni nelle :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>`.

Configurazione Chiamante
~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_agent\_policy. Permette di attivare Richiama su Occupato per un utente e impostare la modalità di tecnologia che verrà utilizzata quando si inserisce la funzione. Nella maggior parte dei casi deve essere scelto 'generic' a meno che non ci sono telefoni progettati per lavorare con funzionalità specifiche.

Configurazione Chiamato
~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_monitor\_policy. Utilizzato per controllare se altri telefoni sono autorizzati per il Richiama su Occupato per un interno. In caso affermativo, si imposta la modalità di tecnologia utilizzata per monitorare lo stato del numero da richiamare. Se il supporto a nessuna tecnologia specifica è disponibile, allora dovrebbe essere impostato su un *generic*. In questa modalità, una richiamata verrà avviata per l'estensione quando cambia da uno stato di NotInUse InUse. Se era occupata al primo tentativo, succederà quando la chiamata corrente finirà. Se semplicemente non ha risposto, allora questa sarà la prossima volta che si utilizza questo telefono per effettuare o rispondere a una chiamata e poi si riaggancia. E' possibile impostare questo per trarre vantaggio dal supporto *native* della tecnologia, se disponibile, e automaticamente avere fallback di 'generic' non impostandolo a *always*.

Timeout Chiamante per Richiama
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_offer\_timer. Entro quanti secondi dopo aver chiamato una estensione occupata o non disponibile poter richiedere il Richiama su Occupato.

Timeout Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: ccbs\_available\_timer. Quanto tempo una richiesta di Richiama su Occupato deve rimane attiva, in secondi, prima di scadere se l'estensione chiamata era occupata al primo tentativo.

Timeout Richiama su Non Risposta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: ccnr\_available\_timer. Quanto tempo una richiesta di Richiamata su Non Risposta deve rimanere attiva, in secondi, prima di scadere se l'estensione chiamata non ha risposto al primo tentativo.

Timeout di Richiamata
~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_recall\_timer. Ogni quanto in secondi richiamare un chiamante che ha come Configurazione Chiamante *Generic Device*. Questo non ha effetto se configurato altrimenti.

Numero Massimo di Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_max\_agents. Valido solo per gli interni con supporto alla modalità *native* per Il Richiama su Occupato. Questo è il numero di massimo di Richiama su Occupato possibile per interno. Gli interni con la modalità *generic* possono gestirne solo una per volta e questo parametro sarà ignorato.

Modalità di Richiamata del Chiamante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Affects Asterisk: cc\_agent\_dialstring. Se non è impostata una richiesta di richiamata viene selezionato direttamente al dispositivo specifico che ha effettuato la chiamata. Se si utilizza il supporto 'native' la tecnologia potrebbe essere la modalità preferita. Con *internal* (richiamata Standard) partirà una chiamata al chiamante come se qualcun altro sul centralino avesse effettuato la chiamata, il che significa che la chiamata può interessare il Seguimi. Per evitare il Seguimi, scegliere *CallBack Extension* (estensione richiamata).

Massimo Numero Chiamanti Accodati
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_max\_monitors. Questo è il numero massimo di chiamanti a cui è permesso accodare un richiesta di richiamata.

Annuncio per Estensione Richiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Per mandare un annuncio all'estensione che viene richiamata quando il telefono è contattato.

Alert-Info Richiamata su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Una suoneria particolare può essere utilizzata per il Richiama su Occupato. Solo se l'interno è in modalità *generic* e la modalità di richiamata è Richiamata Diretta.

Prefisso ID Chiamante
~~~~~~~~~~~~~~~~~~~~~

Un prefisso ID chiamante opzionale può essere utilizzato per la richiamata. Funziona solo se la modalità dell'interno è *generic*.

Alert-Info per il chiamato
~~~~~~~~~~~~~~~~~~~~~~~~~~

Una suoneria differenziata configurata per essere mandata all'estensione da richiamare.

Prefisso ID Chiamante per il chiamato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Un prefisso Id Chiamante opzionale può essere inviato all'estensione che viene richiamato.

Casella Vocale
--------------

Vedi :ref:`qui <casella_vocale_ref_label>`.

Lingua
------

Codice Lingua
~~~~~~~~~~~~~

Il codice lingua utilizzato dall'Interno. Tutti i messaggi di sistema verranno riprodotti in questa lingua.

Opzioni Interno
---------------

ID in Uscita
~~~~~~~~~~~~

Sovrascrive l'Identificativo Chiamante quando si chiama attraverso un Fascio. Lasciare vuoto per disabilitarlo.

Formato: "nome chiamante" <###########>.

Contesto Personalizzato
~~~~~~~~~~~~~~~~~~~~~~~

E' possibile indicare per l'interno un Contesto Personalizzato che ne limiti o aumenti le funzionalità permesse. Vedi :ref:`qui <contesti_personalizzati_ref_label>`.

Tempo di squillo
~~~~~~~~~~~~~~~~

Numero di squilli prima di direzionare la chiamata alla casella vocale.
Il valore predefinito è configurabile :ref:`qui <impostazioni_generali_ref_label>`.  Se la casella vocale è disattivata questa opzione sarà ignorata.

Tempo di squillo inoltro di chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero di secondi prima di inviare la chiamata alla Casella vocale o alla destinazione specificata in caso di trasferimento di chiamata su occupato o non disponibile. Impostando a *Sempre* la chiamata non verrà deviata ma l'interno continuerà a squillare. Predefinito userà il tempo di squillo impostato sopra.

Limite di chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero massimo chiamate in uscita contemporanee che l'interno può fare.

Avviso di chiamata
~~~~~~~~~~~~~~~~~~

Attivazione/Disattivazione dell'Avviso di Chiamata, vedi :ref:`qui <funzionalita_base_ref_label>`.

Risposta Automatica Interna
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato a *Intercom* l'interno risponderà automaticamente alle chiamate interne, la funzionalità deve essere anche supportata dal telefono. Le chiamate esterne si comporteranno normalmente.

Controllo Chiamata
~~~~~~~~~~~~~~~~~~

Se attivato verrà chiesto ai chiamanti delle chiamate esterne di dire il proprio nome, che sarà successivamente riprodotto all'utente per permettere di accettare o rifiutare la chiamata. Il controllo con memorizzazione verifica il chiamante una volta solo tramite il numero identificativo, quello senza memorizzazione chiederà sempre il chiamante.

Chiamate senza pin
~~~~~~~~~~~~~~~~~~

Abilitando questa opzione, l'interno potrà bypassare ogni richiesta di pin sulle :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

ID di Emergenza
~~~~~~~~~~~~~~~

Se inserito sarà utilizzato questo ID quando si chiamerà attraverso una :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` impostata come di Emergenza.

Rilevamento stato della Coda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se l'Interno è un agente di una :ref:`Coda <code_ref_label>`, la Coda tenta di determinare lo stato dell'Interno per capire se può essere chiamato.  In situazioni particolari, come ad esempio un :ref:`Seguimi <seguimi_ref_label>` configurato con un numero esterno, lo stato dell'Interno potrebbe essere non corretto. L'opzione *Ignore State* costringerà la Coda a contattare sempre l'Interno.

Opzioni Registrazione
---------------------

Gestione chiamate in entrata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in entrata su questo Interno da fonti esterne.

Gestione chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in uscita da questo Interno da fonti esterne.

Gestione chiamate in entrata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in entrata su questo Interno da altri interni.

Gestione chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in uscita da questo Interno da altri interni.

Registrazione Chiamate su Richiesta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitare o disabilitare la possibilità di registrare una chiamata in corso su richiesta. Vedi anche :ref:`qui <funzionalita_base_ref_label>`.

Priorità di Registrazione
~~~~~~~~~~~~~~~~~~~~~~~~~

Priorità di Registrazione relativa ad altri interni quando c'è un conflitto tra un Interno che vuole registrare una chiamata ed uno che invece non vorrebbe permetterlo. Il valore più alto dei due determina se registrare o meno, con un pareggio valgono le impostazioni generali.

Servizi Dettatura
-----------------

Servizio
~~~~~~~~

Attivazione/Disattivazione del servizio.

Formato Dettatura
~~~~~~~~~~~~~~~~~

Formato del file audio.

Indirizzo Email
~~~~~~~~~~~~~~~

Indirizzo mail a cui inviare le dettature complete.

.. warning::  L'indirizzo mittente della mail sarà @dominio del |product|, nel caso la posta non sia gestita direttamente dal |product| un dominio fittizio potrebbe portare problemi sull'invio della mail, vedi la documentazione di |product_service|.

VmX Locater
-----------

VmX Locater™
~~~~~~~~~~~~

Attiva/Disattiva VmX Locater

Utilizza quando
~~~~~~~~~~~~~~~

Selezionare se utilizzare VmX Locater quando l'interno è Non Disponibile e/o Occupato

Istruzioni Casella Vocale
~~~~~~~~~~~~~~~~~~~~~~~~~

Deselezionare per dare un beep dopo il messaggio di benvenuto delle caselle vocali.

Preme 0
~~~~~~~

Alla pressione dello 0 la chiamata va all'operatore. Deselezionare e indicare una destinazione alternativa in caso si voglia cambiare il comportamento di default.

Preme 1
~~~~~~~

Destinazione della chiamata alla pressione del tasto 1. Possono essere indicati numerazioni interne ed esterne.

Preme 2
~~~~~~~

Destinazione della chiamata alla pressione del tasto 2. Possono essere indicati numerazioni interne ed esterne.

Destinazioni opzionali
----------------------

Nessuna risposta
~~~~~~~~~~~~~~~~

Configurare la destinazione della chiamata se non risposta.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Nessuna Risposta.

Occupato
~~~~~~~~

Configurare la destinazione della chiamata su Occupato.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Occupato.

Non raggiungibile
~~~~~~~~~~~~~~~~~

Configurare la destinazione della chiamata su Non Raggiungibile.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Non Raggiungibile.

.. _interni_sip_ref_label:

Interni SIP
===========


Configurazione
--------------

Interno Utente
~~~~~~~~~~~~~~

Numero di Interno per Contattare l'utente. Utilizzare un numero univoco.

Nome visualizzato
~~~~~~~~~~~~~~~~~

L'identificativo per le chiamate provenienti da questo interno.

Alias Numero Identificativo
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il numero identificativo Chiamante per le chiamate interne, se differente dal numero interno. E' usato per mascherare un numero differente, come ad esempio per un'utente che ha due interni, magari uno fisso e un cordless, e vuole che il chiamante sia sempre lo stesso interno indipendentemente che chiami dal telefono fisso o dal telefono cordless.

Alias SIP
~~~~~~~~~

Impostare un nome da aggiungere all'interno quando viene chiamato. Serve le chiamate dirette sip interne.

Opzioni Apparato
----------------

secret
~~~~~~

Password per questo interno, deve essere almeno di 6 caratteri e contenere almeno 2 lettere e 2 numeri.

dtmfmode
~~~~~~~~

La modalità DTMF usata da questo interno. E' consigliabile usare RFC 2833 se supportata dal telefono.

canreinvite
~~~~~~~~~~~

Politica di reinvite per l'interno.

host
~~~~

Host per questo apparato, normalmente dynamic per i telefoni

trustrpid
~~~~~~~~~

Modalità per le impostazioni RPID(Remote Party ID) per questo telefono.
Normalmente deve essere SI per far funzionare la funzionalità CONNECTEDLINE() se supportata dal telefono.

sendrpid
~~~~~~~~

Modalità di invio delle informazioni RPID(Remote Party ID) al telefono.

type
~~~~

Tipo di configurazione lato **Asterisk** per l'interno. Normalmente
friend per i telefoni. 

*  **user** entità su **Asterisk** che può fare chiamate.
*  **peer** entità su **Asterisk** a cui vengono mandate le chiamate, tipicamente un Provider Voip.
*  **friend** entrambe le modalità **user** e **peer**, quindi entità in grado di fare e ricevere chiamate.

nat
~~~

Parametro per configurare il nat per questo interno. Tipicamente sono configurazioni da fare globalmente :ref:`qui <impostazioni_Sip_ref_label>`

port
~~~~

Porta di utilizzo del telefono. Tipicamente la 5060 essendo SIP.

qualify
~~~~~~~

Configurato a yes si attiva l'invio periodico di un pacchetto dal |product| verso il telefono, tipicamente ogni minuto. Viene usato per monitorare lo stato del collegamento |product|-telefono e ad esempio considerare il telefono offline se il tempo di comunicazione diventa troppo elevato.

qualifyfreq
~~~~~~~~~~~

Frequenza dell'invio di un pacchetto se l'opzione qualify è a yes.

transport
~~~~~~~~~

Configura la modalità di trasporto dei dati tra TCP, UDP e TLS.

encryption
~~~~~~~~~~

Modalità criptata per le comunicazioni |product|-telefono. E' supportato solo la modalità SRTP, per attivarla anche il telefono deve supportarla.

directmedia
~~~~~~~~~~~

Impostazioni di reinvite per l'interno, impostare a No questo parametro per client WebRTC

.. _interni_sip_videosupport_ref_label:

videosupport
~~~~~~~~~~~~

Supporto a chiamata video dell'interno, impostare a No questo parametro per client WebRTC.

icesupport
~~~~~~~~~~

Supporto a Interactive Connectivity Establishment, impostare a Si questo parametro per client WebRTC.

avpf
~~~~

Audio Video Profile per rtcp, impostare a Si questo parametro per client WebRTC.

.. _interni_sip_callgroup_ref_label:

callgroup
~~~~~~~~~

Gruppo di appartenenza dell'interno. L'interno può appartenere a anche a più gruppi contemporaneamente. E' una impostazione usata per il :ref:`Pickup Generale <funzionalita_base_ref_label>`. Ad esempio configurando 1,3-5 l'interno apparterrà ai gruppi 1,3,4,5.

.. _interni_sip_pickupgroup_ref_label:

pickupgroup
~~~~~~~~~~~

Gruppo di Pick Up. Utilizzato per il :ref:`Pickup Generale <funzionalita_base_ref_label>`, indica digitando \*8 le chiamate di quali gruppi possono essere intercettate.  Possono essere indicati anche più gruppi, ad esempio configurando 1,3-5 l'interno potrà intercettare le chiamate che suonano in interni appartenenti ai gruppi 1,3,4,5.

disallow
~~~~~~~~

Codecs disattivati. E' possibile indicarne anche più di uno, ad esempio ulaw&alaw o tutti con all.

allow
~~~~~

Codecs permessi. E' possibile indicarne anche più di uno, ad esempio ulaw&alaw, l'ordine indica la priorità, o tutti con all. Tutti i codecs permessi nelle :ref:`Impostazioni SIP <impostazioni_sip_ref_label>` sono permessi se non specificati in disallow.

dial
~~~~

Comando per chiamare questo interno.

accountcode
~~~~~~~~~~~

Accountcode per questo interno.

mailbox
~~~~~~~

Mailbox per questo interno.

vmexten
~~~~~~~

Interno per contattare la casella vocale per questo interno. Lasciare vuoto per default.

deny
~~~~

Range di indirizzi ip dai quali non accettare accesso per questo interno. Inserire in modalità rete/maschera di rete.

permit
~~~~~~

Range di indirizzi ip dai quali accettare accesso per questo interno.
Inserire in modalità rete/maschera di rete.

Selezione Passante/ID assegnato
-------------------------------

Sezione per configurare una Selezione Passante che faccia suonare direttamente l'Interno.

Le Selezioni Passanti già configurate vengono elencate in fondo e cliccandoci si viene inoltrati alla :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` corrispondente.

Descrizione Selezione Passante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Descrizione della Selezione Passante diretta a questo Interno.

Aggiungi Selezione Passante
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire il numero della Selezione Passante associata a questo interno.
Deve essere nello stesso formato fornito dal gestore telefonico.

Aggiungi ID in Entrata
~~~~~~~~~~~~~~~~~~~~~~

Aggiunge un ID Chiamante per un instradamento specifico di Selezione Passante. Una Selezione Passante deve essere specificata nel box superiore. Oltre alle sequenze di chiamata standard, è possibile inserire i parametri Private, Blocked, Unknown, Restricted, Anonymous e Unavailable per catturare le chiamate nei casi speciali, se il gestore trasmette questo tipo di informazione.

Call Camp-On Services
---------------------

Gestione del servizio di Richiama su Occupato. Se nelle :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>` del Modulo Richiama su Occupato è configurato Usa le Impostazioni di default a Vero sarà possibile configurare per ogni Interno solo il Chiamante e il Chiamato.

Forcing default settings
~~~~~~~~~~~~~~~~~~~~~~~~

Se presente indica che le opzioni di default sono attivate per tutti gli interni. E' possibile cambiare questa opzione e/o le opzioni comuni nelle :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>`.

Configurazione Chiamante
~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_agent\_policy. Permette di attivare Richiama su Occupato per un utente e impostare la modalità di tecnologia che verrà utilizzata quando si inserisce la funzione. Nella maggior parte dei casi deve essere scelto 'generic' a meno che non ci sono telefoni progettati per lavorare con funzionalità specifiche.

Configurazione Chiamato
~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_monitor\_policy. Utilizzato per controllare se altri telefoni sono autorizzati per il Richiama su Occupato per un interno. In caso affermativo, si imposta la modalità di tecnologia utilizzata per monitorare lo stato del numero da richiamare. Se il supporto a nessuna tecnologia specifica è disponibile, allora dovrebbe essere impostato su un *generic*. In questa modalità, una richiamata verrà avviata per l'estensione quando cambia da uno stato di NotInUse InUse. Se era occupata al primo tentativo, succederà quando la chiamata corrente finirà. Se semplicemente non ha risposto, allora questa sarà la prossima volta che si utilizza questo telefono per effettuare o rispondere a una chiamata e poi si riaggancia. E' possibile impostare questo per trarre vantaggio dal supporto *native* della tecnologia, se disponibile, e automaticamente avere fallback di 'generic' non impostandolo a *always*.

Timeout Chiamante per Richiama
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_offer\_timer. Entro quanti secondi dopo aver chiamato una estensione occupata o non disponibile poter richiedere il Richiama su Occupato.

Timeout Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: ccbs\_available\_timer. Quanto tempo una richiesta di Richiama su Occupato deve rimane attiva, in secondi, prima di scadere se l'estensione chiamata era occupata al primo tentativo.

Timeout Richiama su Non Risposta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: ccnr\_available\_timer. Quanto tempo una richiesta di Richiamata su Non Risposta deve rimanere attiva, in secondi, prima di scadere se l'estensione chiamata non ha risposto al primo tentativo.

Timeout di Richiamata
~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_recall\_timer. Ogni quanto in secondi richiamare un chiamante che ha come Configurazione Chiamante *Generic Device*. Questo non ha effetto se configurato altrimenti.

Numero Massimo di Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_max\_agents. Valido solo per gli interni con supporto alla modalità *native* per Il Richiama su Occupato. Questo è il numero di massimo di Richiama su Occupato possibile per interno. Gli interni con la modalità *generic* possono gestirne solo una per volta e questo parametro sarà ignorato.

Modalità di Richiamata del Chiamante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Affects Asterisk: cc\_agent\_dialstring. Se non è impostata una richiesta di richiamata viene selezionato direttamente al dispositivo specifico che ha effettuato la chiamata. Se si utilizza il supporto 'native' la tecnologia potrebbe essere la modalità preferita. Con *internal* (richiamata Standard) partirà una chiamata al chiamante come se qualcun altro sul centralino avesse effettuato la chiamata, il che significa che la chiamata può interessare il Seguimi. Per evitare il Seguimi, scegliere *CallBack Extension* (estensione richiamata).

Massimo Numero Chiamanti Accodati
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_max\_monitors. Questo è il numero massimo di chiamanti a cui è permesso accodare un richiesta di richiamata.

Annuncio per Estensione Richiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Per mandare un annuncio all'estensione che viene richiamata quando il telefono è contattato.

Alert-Info Richiamata su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Una suoneria particolare può essere utilizzata per il Richiama su Occupato. Solo se l'interno è in modalità *generic* e la modalità di richiamata è Richiamata Diretta.

Prefisso ID Chiamante
~~~~~~~~~~~~~~~~~~~~~

Un prefisso ID chiamante opzionale può essere utilizzato per la richiamata. Funziona solo se la modalità dell'interno è *generic*.

Alert-Info per il chiamato
~~~~~~~~~~~~~~~~~~~~~~~~~~

Una suoneria differenziata configurata per essere mandata all'estensione da richiamare.

Prefisso ID Chiamante per il chiamato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Un prefisso Id Chiamante opzionale può essere inviato all'estensione che viene richiamato.


Casella Vocale
--------------

Vedi :ref:`qui <casella_vocale_ref_label>`.

Lingua
------

Codice Lingua
~~~~~~~~~~~~~

Il codice lingua utilizzato dall'Interno. Tutti i messaggi di sistema verranno riprodotti in questa lingua.

Opzioni Interno
---------------

ID in Uscita
~~~~~~~~~~~~

Sovrascrive l'Identificativo Chiamante quando si chiama attraverso un Fascio. Lasciare vuoto per disabilitarlo.

Formato: "nome chiamante" <###########>.

Contesto Personalizzato
~~~~~~~~~~~~~~~~~~~~~~~

E' possibile indicare per l'interno un Contesto Personalizzato che ne limiti o aumenti le funzionalità permesse. Vedi :ref:`qui <contesti_personalizzati_ref_label>`.

Tempo di squillo
~~~~~~~~~~~~~~~~

Numero di squilli prima di direzionare la chiamata alla casella vocale.
Il valore predefinito è configurabile :ref:`qui <impostazioni_generali_ref_label>`.
Se la casella vocale è disattivata questa opzione sarà ignorata.

Tempo di squillo inoltro di chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero di secondi prima di inviare la chiamata alla Casella vocale o alla destinazione specificata in caso di trasferimento di chiamata su occupato o non disponibile. Impostando a *Sempre* la chiamata non verrà deviata ma l'interno continuerà a squillare. Predefinito userà il tempo di squillo impostato sopra.

Limite di chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero massimo chiamate in uscita contemporanee che l'interno può fare.

Avviso di chiamata
~~~~~~~~~~~~~~~~~~

Attivazione/Disattivazione dell'Avviso di Chiamata, vedi :ref:`qui <funzionalita_base_ref_label>`.

Risposta Automatica Interna
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato a *Intercom* l'interno risponderà automaticamente alle chiamate interne, la funzionalità deve essere anche supportata dal telefono. Le chiamate esterne si comporteranno normalmente.

Controllo Chiamata
~~~~~~~~~~~~~~~~~~

Se attivato verrà chiesto ai chiamanti delle chiamate esterne di dire il proprio nome, che sarà successivamente riprodotto all'utente per permettere di accettare o rifiutare la chiamata. Il controllo con memorizzazione verifica il chiamante una volta solo tramite il numero identificativo, quello senza memorizzazione chiederà sempre il chiamante.

Chiamate senza pin
~~~~~~~~~~~~~~~~~~

Abilitando questa opzione, l'interno potrà bypassare ogni richiesta di pin sulle :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

ID di Emergenza
~~~~~~~~~~~~~~~

Se inserito sarà utilizzato questo ID quando si chiamerà attraverso una :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` impostata come di Emergenza.

Rilevamento stato della Coda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se l'Interno è un agente di una :ref:`Coda <code_ref_label>`, la Coda tenta di determinare lo stato dell'Interno per capire se può essere chiamato.  In situazioni particolari, come ad esempio un :ref:`Seguimi <seguimi_ref_label>` configurato con un numero esterno, lo stato dell'Interno potrebbe essere non corretto. L'opzione *Ignore State* costringerà la Coda a contattare sempre l'Interno.

Opzioni Registrazione
---------------------

Gestione chiamate in entrata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in entrata su questo Interno da fonti esterne.

Gestione chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in uscita da questo Interno da fonti esterne.

Gestione chiamate in entrata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in entrata su questo Interno da altri interni.

Gestione chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in uscita da questo Interno da altri interni.

Registrazione Chiamate su Richiesta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitare o disabilitare la possibilità di registrare una chiamata in corso su richiesta. Vedi anche :ref:`qui <funzionalita_base_ref_label>`.

Priorità di Registrazione
~~~~~~~~~~~~~~~~~~~~~~~~~

Priorità di Registrazione relativa ad altri interni quando c'è un conflitto tra un Interno che vuole registrare una chiamata ed uno che invece non vorrebbe permetterlo. Il valore più alto dei due determina se registrare o meno, con un pareggio valgono le impostazioni generali.

Servizi Dettatura
-----------------

Servizio
~~~~~~~~

Attivazione/Disattivazione del servizio.

Formato Dettatura
~~~~~~~~~~~~~~~~~

Formato del file audio.

Indirizzo Email
~~~~~~~~~~~~~~~

Indirizzo mail a cui inviare le dettature complete.


.. warning::   L'indirizzo mittente della mail sarà @dominio del |product|, nel caso la posta non sia gestita direttamente dal |product| un dominio fittizio potrebbe portare problemi sull'invio della mail, vedi l a documentazione del |product_service|.

VmX Locater
-----------

VmX Locater™
~~~~~~~~~~~~

Attiva/Disattiva VmX Locater

Utilizza quando
~~~~~~~~~~~~~~~

Selezionare se utilizzare VmX Locater quando l'interno è Non Disponibile e/o Occupato

Istruzioni Casella Vocale
~~~~~~~~~~~~~~~~~~~~~~~~~

Deselezionare per dare un beep dopo il messaggio di benvenuto delle caselle vocali.

Preme 0
~~~~~~~

Alla pressione dello 0 la chiamata va all'operatore. Deselezionare e indicare una destinazione alternativa in caso si voglia cambiare il comportamento di default.

Preme 1
~~~~~~~

Destinazione della chiamata alla pressione del tasto 1. Possono essere indicati numerazioni interne ed esterne.

Preme 2
~~~~~~~

Destinazione della chiamata alla pressione del tasto 2. Possono essere indicati numerazioni interne ed esterne.

Destinazioni opzionali
----------------------

Nessuna risposta
~~~~~~~~~~~~~~~~

Configurare la destinazione della chiamata se non risposta.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Nessuna Risposta.

Occupato
~~~~~~~~

Configurare la destinazione della chiamata su Occupato.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Occupato.

Non raggiungibile
~~~~~~~~~~~~~~~~~

Configurare la destinazione della chiamata su Non Raggiungibile.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Non Raggiungibile.

Gestione Terminali
------------------

Gestione Provisioning per l'Interno.

Cancella
~~~~~~~~

Cancella le configurazioni.

Indirizzo MAC
~~~~~~~~~~~~~

Indirizzo MAC del telefono.

Marca
~~~~~

La marca del telefono.

Modello
~~~~~~~

Modello del telefono.

Linea
~~~~~

Numero di linee da configurare.

Template
~~~~~~~~

Template di configurazione, vedi :ref:`qui <provisioning_gestione_template_terminali_ref_label>`.

Reboot
~~~~~~

Riavvia il telefono per applicare le modifiche.

.. _interni_dahdi_ref_label:

Interni DAHDI
=============


Configurazione
--------------

Interno Utente
~~~~~~~~~~~~~~

Numero di Interno per Contattare l'utente. Utilizzare un numero univoco.

Nome visualizzato
~~~~~~~~~~~~~~~~~

L'identificativo per le chiamate provenienti da questo interno.

Alias Numero Identificativo
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il numero identificativo Chiamante per le chiamate interne, se differente dal numero interno. E' usato per mascherare un numero differente, come ad esempio per un'utente che ha due interni, magari uno fisso e un cordless, e vuole che il chiamante sia sempre lo stesso interno indipendentemente che chiami dal telefono fisso o dal telefono cordless.

Alias SIP
~~~~~~~~~

Impostare un nome da aggiungere all'interno quando viene chiamato. Serve le chiamate dirette sip interne.

Opzioni Interno
---------------

ID in Uscita
~~~~~~~~~~~~

Sovrascrive l'Identificativo Chiamante quando si chiama attraverso un Fascio. Lasciare vuoto per disabilitarlo.

Formato: "nome chiamante" <###########>.

Contesto Personalizzato
~~~~~~~~~~~~~~~~~~~~~~~

E' possibile indicare per l'interno un Contesto Personalizzato che ne limiti o aumenti le funzionalità permesse. Vedi :ref:`qui <contesti_personalizzati_ref_label>`.

Tempo di squillo
~~~~~~~~~~~~~~~~

Numero di squilli prima di direzionare la chiamata alla casella vocale.
Il valore predefinito è configurabile :ref:`qui <impostazioni_generali_ref_label>`.
Se la casella vocale è disattivata questa opzione sarà ignorata.

Tempo di squillo inoltro di chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero di secondi prima di inviare la chiamata alla Casella vocale o alla destinazione specificata in caso di trasferimento di chiamata su occupato o non disponibile. Impostando a *Sempre* la chiamata non verrà deviata ma l'interno continuerà a squillare. Predefinito userà il tempo di squillo impostato sopra.

Limite di chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero massimo chiamate in uscita contemporanee che l'interno può fare.

Avviso di chiamata
~~~~~~~~~~~~~~~~~~

Attivazione/Disattivazione dell'Avviso di Chiamata, vedi :ref:`qui <funzionalita_base_ref_label>`.

Risposta Automatica Interna
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se attivato a *Intercom* l'interno risponderà automaticamente alle chiamate interne, la funzionalità deve essere anche supportata dal telefono. Le chiamate esterne si comporteranno normalmente.

Controllo Chiamata
~~~~~~~~~~~~~~~~~~

Se attivato verrà chiesto ai chiamanti delle chiamate esterne di dire il proprio nome, che sarà successivamente riprodotto all'utente per permettere di accettare o rifiutare la chiamata. Il controllo con memorizzazione verifica il chiamante una volta solo tramite il numero identificativo, quello senza memorizzazione chiederà sempre il chiamante.

Chiamate senza pin
~~~~~~~~~~~~~~~~~~

Abilitando questa opzione, l'interno potrà bypassare ogni richiesta di pin sulle :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

ID di Emergenza
~~~~~~~~~~~~~~~

Se inserito sarà utilizzato questo ID quando si chiamerà attraverso una :ref:`Rotta In Uscita <rotte_in_uscita_ref_label>` impostata come di Emergenza.

Rilevamento stato della Coda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se l'Interno è un agente di una :ref:`Coda <code_ref_label>`, la Coda tenta di determinare lo stato dell'Interno per capire se può essere chiamato. 
In situazioni particolari, come ad esempio un :ref:`Seguimi <seguimi_ref_label>` configurato con un numero esterno, lo stato dell'Interno potrebbe essere non corretto. L'opzione *Ignore State* costringerà la Coda a contattare sempre l'Interno.

Opzioni Apparato
----------------

Nessuna essendo tecnologia DAHDI.

Selezione Passante/ID assegnato
-------------------------------

Sezione per configurare una Selezione Passante che faccia suonare direttamente l'Interno.

Le Selezioni Passanti già configurate vengono elencate in fondo e cliccandoci si viene inoltrati alla :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` corrispondente.

Descrizione Selezione Passante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Descrizione della Selezione Passante diretta a questo Interno.

Aggiungi Selezione Passante
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire il numero della Selezione Passante associata a questo interno.
Deve essere nello stesso formato fornito dal gestore telefonico.

Aggiungi ID in Entrata
~~~~~~~~~~~~~~~~~~~~~~

Aggiunge un ID Chiamante per un instradamento specifico di Selezione Passante. Una Selezione Passante deve essere specificata nel box superiore. Oltre alle sequenze di chiamata standard, è possibile inserire i parametri Private, Blocked, Unknown, Restricted, Anonymous e Unavailable per catturare le chiamate nei casi speciali, se il gestore trasmette questo tipo di informazione.

Call Camp-On Services
---------------------

Gestione del servizio di Richiama su Occupato. Se nelle :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>` del Modulo Richiama su Occupato è configurato Usa le Impostazioni di default a Vero sarà possibile configurare per ogni Interno solo il Chiamante e il Chiamato.

Forcing default settings
~~~~~~~~~~~~~~~~~~~~~~~~

Se presente indica che le opzioni di default sono attivate per tutti gli interni. E' possibile cambiare questa opzione e/o le opzioni comuni nelle :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>`.

Configurazione Chiamante
~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_agent\_policy. Permette di attivare Richiama su Occupato per un utente e impostare la modalità di tecnologia che verrà utilizzata quando si inserisce la funzione. Nella maggior parte dei casi deve essere scelto 'generic' a meno che non ci sono telefoni progettati per lavorare con funzionalità specifiche.

Configurazione Chiamato
~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_monitor\_policy. Utilizzato per controllare se altri telefoni sono autorizzati per il Richiama su Occupato per un interno. In caso affermativo, si imposta la modalità di tecnologia utilizzata per monitorare lo stato del numero da richiamare. Se il supporto a nessuna tecnologia specifica è disponibile, allora dovrebbe essere impostato su un *generic*. In questa modalità, una richiamata verrà avviata per l'estensione quando cambia da uno stato di NotInUse InUse. Se era occupata al primo tentativo, succederà quando la chiamata corrente finirà. Se semplicemente non ha risposto, allora questa sarà la prossima volta che si utilizza questo telefono per effettuare o rispondere a una chiamata e poi si riaggancia. E' possibile impostare questo per trarre vantaggio dal supporto *native* della tecnologia, se disponibile, e automaticamente avere fallback di 'generic' non impostandolo a *always*.

Timeout Chiamante per Richiama
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_offer\_timer. Entro quanti secondi dopo aver chiamato una estensione occupata o non disponibile poter richiedere il Richiama su Occupato.

Timeout Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: ccbs\_available\_timer. Quanto tempo una richiesta di Richiama su Occupato deve rimane attiva, in secondi, prima di scadere se l'estensione chiamata era occupata al primo tentativo.

Timeout Richiama su Non Risposta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: ccnr\_available\_timer. Quanto tempo una richiesta di Richiamata su Non Risposta deve rimanere attiva, in secondi, prima di scadere se l'estensione chiamata non ha risposto al primo tentativo.

Timeout di Richiamata
~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_recall\_timer. Ogni quanto in secondi richiamare un chiamante che ha come Configurazione Chiamante *Generic Device*. Questo non ha effetto se configurato altrimenti.

Numero Massimo di Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_max\_agents. Valido solo per gli interni con supporto alla modalità *native* per Il Richiama su Occupato. Questo è il numero di massimo di Richiama su Occupato possibile per interno. Gli interni con la modalità *generic* possono gestirne solo una per volta e questo parametro sarà ignorato.

Modalità di Richiamata del Chiamante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Affects Asterisk: cc\_agent\_dialstring. Se non è impostata una richiesta di richiamata viene selezionato direttamente al dispositivo specifico che ha effettuato la chiamata. Se si utilizza il supporto 'native' la tecnologia potrebbe essere la modalità preferita. Con *internal* (richiamata Standard) partirà una chiamata al chiamante come se qualcun altro sul centralino avesse effettuato la chiamata, il che significa che la chiamata può interessare il Seguimi. Per evitare il Seguimi, scegliere *CallBack Extension* (estensione richiamata).

Massimo Numero Chiamanti Accodati
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asterisk: cc\_max\_monitors. Questo è il numero massimo di chiamanti a cui è permesso accodare un richiesta di richiamata.

Annuncio per Estensione Richiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Per mandare un annuncio all'estensione che viene richiamata quando il telefono è contattato.

Alert-Info Richiamata su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Una suoneria particolare può essere utilizzata per il Richiama su Occupato. Solo se l'interno è in modalità *generic* e la modalità di richiamata è Richiamata Diretta.

Prefisso ID Chiamante
~~~~~~~~~~~~~~~~~~~~~

Un prefisso ID chiamante opzionale può essere utilizzato per la richiamata. Funziona solo se la modalità dell'interno è *generic*.

Alert-Info per il chiamato
~~~~~~~~~~~~~~~~~~~~~~~~~~

Una suoneria differenziata configurata per essere mandata all'estensione da richiamare.

Prefisso ID Chiamante per il chiamato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Un prefisso Id Chiamante opzionale può essere inviato all'estensione che viene richiamato.

Casella Vocale
--------------

Vedi :ref:`qui <casella_vocale_ref_label>`.

Device Options
--------------

Scegliere il canale FXS per questo interno

Lingua
------

Codice Lingua
~~~~~~~~~~~~~

Il codice lingua utilizzato dall'Interno. Tutti i messaggi di sistema verranno riprodotti in questa lingua.

Opzioni Registrazione
---------------------

Gestione chiamate in entrata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in entrata su questo Interno da fonti esterne.

Gestione chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in uscita da questo Interno da fonti esterne.

Gestione chiamate in entrata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in entrata su questo Interno da altri interni.

Gestione chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Politica di registrazione delle chiamate in uscita da questo Interno da altri interni.

Registrazione Chiamate su Richiesta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitare o disabilitare la possibilità di registrare una chiamata in corso su richiesta. Vedi anche :ref:`qui <funzionalita_base_ref_label>`.

Priorità di Registrazione
~~~~~~~~~~~~~~~~~~~~~~~~~

Priorità di Registrazione relativa ad altri interni quando c'è un conflitto tra un Interno che vuole registrare una chiamata ed uno che invece non vorrebbe permetterlo. Il valore più alto dei due determina se registrare o meno, con un pareggio valgono le impostazioni generali.

Servizi Dettatura
-----------------

Servizio
~~~~~~~~

Attivazione/Disattivazione del servizio.

Formato Dettatura
~~~~~~~~~~~~~~~~~

Formato del file audio.

Indirizzo Email
~~~~~~~~~~~~~~~

Indirizzo mail a cui inviare le dettature complete.


.. warning:: L'indirizzo mittente della mail sarà @dominio del |product|, nel caso la posta non sia gestita direttamente dal |product| un dominio fittizio potrebbe portare problemi sull'invio della mail, vedi la documentazione di |product_service|.
   }}

VmX Locater
-----------

VmX Locater™
~~~~~~~~~~~~

Attiva/Disattiva VmX Locater

Utilizza quando
~~~~~~~~~~~~~~~

Selezionare se utilizzare VmX Locater quando l'interno è Non Disponibile e/o Occupato

Istruzioni Casella Vocale
~~~~~~~~~~~~~~~~~~~~~~~~~

Deselezionare per dare un beep dopo il messaggio di benvenuto delle voicemail.

Preme 0
~~~~~~~

Alla pressione dello 0 la chiamata va all'operatore. Deselezionare e indicare una destinazione alternativa in caso si voglia cambiare il comportamento di default.

Preme 1
~~~~~~~

Destinazione della chiamata alla pressione del tasto 1. Possono essere indicati numerazioni interne ed esterne.

Preme 2
~~~~~~~

Destinazione della chiamata alla pressione del tasto 2. Possono essere indicati numerazioni interne ed esterne.

Destinazioni opzionali
----------------------

Nessuna risposta
~~~~~~~~~~~~~~~~

Configurare la destinazione della chiamata se non risposta.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Nessuna Risposta.

Occupato
~~~~~~~~

Configurare la destinazione della chiamata su Occupato.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Occupato.

Non raggiungibile
~~~~~~~~~~~~~~~~~

Configurare la destinazione della chiamata su Non Raggiungibile.

Prefisso CID
~~~~~~~~~~~~

Il prefisso CID da aggiungere a questa chiamata prima di indirizzarla alla destinazione su Non Raggiungibile.

.. _gestione_multipla_interni_ref_label:

Gestione Multipla Interni
=========================

Il modulo gestione multipla interni serve ad eseguire operazioni di massa su gruppi di interni.

Creazione
---------

E' possibile creare interni in maniera seriale indicando un intervallo e configurando le seguenti opzioni

* nome interni, è utilizzabile il carattere %{EXTEN} per indicare il numero interno
* contesto vedi :ref:`contesti_personalizzati_ref_label`
* avviso di chiamata vedi :ref:`funzionalita_base_ref_label`
* tipo di telefono, fisico adatto a telefoni SIP ip o WebRTC
* destinazioni opzionali su nessuna risposta, occupato e non raggiungibile
* tempo di squillo
* callgroup vedi :ref:`interni_sip_callgroup_ref_label`
* pickupgroup vedi :ref:`interni_sip_pickupgroup_ref_label`
* codec permessi
* codec non permessi
* modificare l'ID in uscita, è utilizzabile il carattere %{EXTEN} per indicare il numero interno o anche una parte di esso, ad esempio 072140551%{EXTEN:1} in caso di intero 201 equivale a 0721405511 (%{EXTEN:1} -> 1), 07214055%{EXTEN:2} in caso di intero 201 equivale a 0721405501 (%{EXTEN:2} -> 01) etc.
* selezione passante, è utilizzabile il carattere %{EXTEN} per indicare il numero interno o anche una parte di esso, ad esempio 072140551%{EXTEN:1} in caso di intero 201 equivale a 0721405511 (%{EXTEN:1} -> 1), 07214055%{EXTEN:2} in caso di intero 201 equivale a 0721405501 (%{EXTEN:2} -> 01) etc.
* descrizione selezione passante, è utilizzabile il carattere %{EXTEN} per indicare il numero interno


Modifica
--------

Gli interni posso essere raggruppati per intervallo o per nome oltre ovviamente ad essere selezionati singolarmente o tutti.

Sugli interni selezionati è possibile modificare:

* modificare il nome visualizzato
* modificare il contesto, vedi :ref:`contesti_personalizzati_ref_label`
* modificare lo stato dell'avviso di chiamata, vedi :ref:`funzionalita_base_ref_label`.
* modificare la tipologia di telefono fisico o WebRTC, se si trasforma un interno WebRTC in fisico è necessario un riavvio di |product|
* modificare le destinazioni opzionali su nessuna risposta, occupato e non raggiungibile
* modificare il tempo di squillo
* modificare il callgroup vedi :ref:`interni_sip_callgroup_ref_label`
* modificare il pickupgroup vedi :ref:`interni_sip_pickupgroup_ref_label`
* modificare i codec permessi
* modificare i codec non permessi 
* modificare l'ID in uscita, è utilizzabile il carattere %{EXTEN} per indicare il numero interno o anche una parte di esso, ad esempio 072140551%{EXTEN:1} in caso di intero 201 equivale a 0721405511 (%{EXTEN:1} -> 1), 07214055%{EXTEN:2} in caso di intero 201 equivale a 0721405501 (%{EXTEN:2} -> 01) etc.

Ogni valore non selezionato verrà ignorato e lasciato alla configuirazione attuale.
Il modulo consente anche la cancellazione massiva di gruppi di interni.

.. _musiche_di_attesa_ref_label:

Musica di Attesa
================

Le musica di attesa permettono di configurare che file audio il |product| debba riprodurre in una chiamata messa in attesa o in tutte quelle situazioni dove un modulo di |product|, come ad esempio le :ref:`rotte in entrata <rotte_in_entrata_ref_label>`, :ref:`rotte in uscita <rotte_in_uscita_ref_label>`, le :ref:`code <code_ref_label>` o i :ref:`gruppi di chiamata <gruppi_di_chiamata_ref_label>`, sostituisce il classico suono di squillo.

Per utilizzare solo un determinato gruppo di files musicali in ogni occorrenza, le musiche di attesa si dividono in **categorie**.

Sulla destra nel box verde vengono elencate le categorie di musica di attesa presenti.

La categoria **predefinito** è la musica di attesa che viene usata di default, quando ad esempio un interno mette in attesa un altro interno.

Per creare una nuova categoria di musica di attesa utilizzare la funzionalità in alto a destra.

E' possibile caricare file .wav e file .mp3 che il |product| convertirà in .wav.

Per caricare un file selezionarlo tramite l'apposito box e poi cliccare su Carica.

Al momento dell'upload si può regolare il volume del file musicale interagendo con il menu Aggiustamento Volume.

Selezionare la categoria se si vuole caricare il file in una categoria specifica, diversa dal predefinito.

Esiste anche la possibilità di utilizzare come musica di attesa uno streaming audio, aggiungendo una apposita categoria di streaming.

.. _configurazione_gateway_ref_label:


Configurazione Gateway
======================

 :ref:`Configurazione Gateway <configurazione_gateway_generale_ref_label>`

.. _configurazione_failover_ref_label:


Configurazione Failover
=======================

Il modulo Failover consente di realizzare un altro |product| con la configurazione gemella da utilizzare come centralino di failover per i client telefonici.

Il caso di uso tipico è quello di una configurazione con |product| master remoto e un |product| slave locale e i client telefonici locali con un account sia sul |product| master sia su quello slave, in modo tale che se il collegamento con il |product| master viene interrotto è possibile utilizzare il |product| slave come failover.

La configurazione quindi, va fatta tutta sul |product| master e poi tramite il modulo Failover copiata sul |product| slave, possono essere anche più di uno i |product| slave configurabili. 

L'unica condizione necessaria al funzionamento del modulo Failover è che ci sia una connessione SSH tra il |product| e i |product| slave senza richiesta di password, quindi con uno scambio di chiavi SSH, scambiare manualmente le chiavi SSH per consentire la connessione SSH senza password dal master allo slave o lanciare dalla shell del |product| master il comando 

::

 /var/lib/asterisk/bin/failover_setup.sh 

che prova a farlo in automatico chiedendo solo la password del |product|.

Configurazione
--------------

La configurazione richiede l'inserimento dell'indirizzo del |product| slave e della porta SSH, è possibile scegliere se sincronizzare anche il database dello storico delle chiamate CDR e le :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>`.

Una volta fatta la configurazione è possibile testare la connessione e la sincronizzazione con i pulsanti dedicati.

Se attivato la sincronizzazione tra il |product| master e il |product| slave viene effettuata ogni 10 minuti.


.. _wizard_provisioning_ref_label:

Wizard Provisioning
===================


Descrizione
-----------

Il modulo Wizard Provisioning nasce con l'intento di facilitare la procedura di Provisioning e di diventare la base per configurare interamente e con pochi click il |product|.

Da questo modulo inizia la procedura di Provisioning degli apparati telefonici supportati, basta indicare nel tab **Dispositivi non configurati** la rete di ricerca e cliccare sul pulsante **Trova nuovi Dispositivi** per dare inizio alla scansione della rete.

Configurazione
--------------

Il risultato della scansione viene caricato in qualche secondo nella pagina.

Si ottiene un elenco di tutti gli apparati telefonici individuati dalla scansione non abbinati ad un interno con il loro indirizzo ip, il loro mac address e il costruttore.

Il modulo tenterà anche tramite una connessione http di individuare il modello dell'apparecchio telefonico, se questa ricerca avrà esito positivo verrà indicato, altrimenti verrà lasciata la possibilità di inserirlo a mano.

Premendo il pulsante della colonna **Azione** è possibile associare un interno libero all'apparato.

E' anche possibile creare un nuovo interno da associare all'apparecchio rilevato: basta indicare il numero di interno, il nome da associare all'interno e la password, vedi :ref:`qui <interni_sip_ref_label>` per maggiori informazioni sugli interni.

Una volta fatta l'associazione di un apparato telefonico con un interno, preesistente o nuovo, il |product| creerà il file di configurazione nella directory di tftp, vedi :ref:`qui <provisioning_ref_label>`, e riavvierà l'apparato (questa operazione potrebbe non andare a buon fine con certi modelli di telefono) in modo tale da passargli all'avvio la nuova configurazione.

Riguardo ai gateway telefonici supportati invece, il pulsante porta al modulo per configurarli, vedi :ref:`qui <configurazione_gateway_generale_ref_label>`, oppure alla loro interfaccia web se non supportati.

Dopo aver associato l'apparecchio telefonico ad un :ref:`interno <interni_sip_ref_label>` la configurazione viene elencata nel tab **Dispositivi Associati**  dove è possibile andare a modificare il template di configurazione o eliminarlo.


.. _registrazioni_di_sistema_ref_label:

Registrazioni di  Sistema
=========================

Descrizione
-----------

Le registrazioni di sistema sono lo strumento per caricare sul |product| dei file audio, di solito di servizio, per poi poterli usare tramite i moduli che lo consentono, ad esempio gli :ref:`annunci <annunci_ref_label>`, le :ref:`code <code_ref_label>`, i :ref:`gruppi di chiamata <gruppi_di_chiamata_ref_label>`, :ref:`IVR <ivr_ref_label>` etc..

Ogni modulo che può tra le sue funzionalità riprodurre un file audio di solito attinge alle registrazioni di sistema.

E' possibile inoltre catturare una registrazione fatta direttamente da un interno del |product|.

Configurazione
--------------

Registrazione da un interno
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Fase 1
^^^^^^

Dopo aver utilizzato i codici servizi dedicati, vedi :ref:`qui <funzionalita_base_ref_label>`, da un interno, indicare l'interno nell'apposito box e cliccare su vai.

La pagina verrà ricaricata, il |product| ha individuato nel frattempo il file audio.

Fase 2
^^^^^^

Inserire una descrizione nel campo Nome per riconoscere il file audio, dopo aver cliccato su Salva, la registrazione di sistema comparirà nell'elenco nel box verde a destra.

Registrazione da File
~~~~~~~~~~~~~~~~~~~~~

Fase 1
^^^^^^

Caricare il file audio tramite l'apposito box e cliccare su CARICA.

Il file **deve essere** .wav (registrato per esempio con il Registratore di Microsoft Windows) del formato PCM, 16Bit, 8000Hz e mono.

Questo perché il |product| non fa nessuna operazione sul file caricato, tipo conversione etc.., per non intaccarne la qualità, per questo il file deve essere già del formato con il quale il |product| gestisce le registrazioni di sistema.

Verrà fatto l'upload del file e la pagina sarà ricaricata.

Fase 2
^^^^^^

Inserire una descrizione nel campo Nome per riconoscere il file audio, dopo aver cliccato su Salva, la registrazione di sistema comparirà nell'elenco nel box verde a destra.

Nell'elenco delle registrazioni sulla destra si trovano le registrazioni interne.
r
Nelle registrazioni interne sono elencati tutti i file audio del |product| che vengono utilizzati per le funzionalità standard.

E' possibile, selezionando uno di questi files, sostituirlo con un file personalizzato o con un altro file già caricato.

Registrazione caricata
~~~~~~~~~~~~~~~~~~~~~~

Selezionando una registrazione caricata è possibile:

Lista
^^^^^

Viene visualizzato qui dove è utilizzata la registrazione di sistema.

Cambia Nome
^^^^^^^^^^^

Nome per la registrazione di sistema.

Nome Descrittivo
^^^^^^^^^^^^^^^^

Campo descrittivo per individuare la registrazione di sistema.

Collega ad un Codice Servizio
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Attivare questa opzione per attivare un codice di servizio che permetterà di cambiare direttamente questa registrazione. Il codice di servizio viene indicato dopo.

Password Codice Servizio
^^^^^^^^^^^^^^^^^^^^^^^^

Password per proteggere l'accesso al codice di servizio. Deve essere numerica.

File
^^^^

Viene indicato il file audio associato alla registrazione di sistema, è possibile cambiarlo, accodarne degli altri, ascoltarlo, cambiare l'ordine di riproduzione.

.. _registrazioni__tts_ref_label:

Registrazioni TTS
=================

Descrizione
-----------

Le registrazioni TTS sono lo strumento per creare sul |product| dei files audio tramite la lettura di un testo da parte del sintonizzatore vocale.

Una volta creata una registrazione TTS automaticamente viene creata anche una :ref:`registrazione di sistema <registrazioni_di_sistema_ref_label>` che consente di utilizzare il file audio creato tramite i moduli che lo prevedono, ad esempio gli :ref:`annunci <annunci_ref_label>`, le :ref:`code <code_ref_label>`, i :ref:`gruppi di chiamata <gruppi_di_chiamata_ref_label>`, :ref:`IVR <ivr_ref_label>` etc..


Configurazione
--------------

Nome
~~~~

Inserire un nome per individuare la registrazione TTS.

Descrizione
~~~~~~~~~~~

Descrizione per questa registrazione TTS

TTS Engine
~~~~~~~~~~

Motore per la sintesi vocale, scegliere tra uno di quelli supportati

Username/Client ID
~~~~~~~~~~~~~~~~~~

Username o client ID per la connessione al motore TTS

Password
~~~~~~~~

Password per la connessione al motore TTS

Testo
~~~~~

Inserire il testo da riprodurre.

Lingua TTS
~~~~~~~~~~

La lingua del sintonizzatore vocale, non verranno fatte traduzioni del testo inserito.

Velocità di Riproduzione TTS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La velocità di lettura del testo da parte del sintonizzatore vocale.

.. _fasci_iax_ref_label:

Fasci IAX
=========

Descrizione
-----------

I Fasci IAX permettono di collegare il |product| a delle fonti telefoniche tramite il protocollo IAX.

I Fasci IAX vengono tipicamente usati per collegare due |product| remoti, vedi :ref:`qui <collegamenti_remoti_ref_label>`.

Se il Fascio è utilizzato in qualche :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` viene notificato in alto.

Sul menù di sinistra si trovano tutti i Fasci già creati, se evidenziati in grigio i Fasci sono disabilitati.

Configurazione
--------------

Nome Fascio
~~~~~~~~~~~

Nome descrittivo per individuare il Fascio.

Identificativo Chiamante in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ID Chiamante per le chiamate in uscita con questo Fascio.

Formato: <###########>. Può essere anche usato il formato "hidden" <#########> per nascondere l'ID Chiamante se supportato dal gestore della linea.

Opzioni CID
~~~~~~~~~~~

Determina a quali CID sarà consentito utilizzare questo Fascio. 
Gli ID di emergenza definiti sugli interni, vedi :ref:`qui <interni_sip_ref_label>`, potranno **sempre** usare questo Fascio se è in una Rotta di Emergenza.

*  **Permetti tutti i CID**: tutti gli ID Chiamante, inclusi quelli esterni inoltrati dalle chiamate esterne, avranno accesso a questo Fascio.
*  **Blocca CID esterni**: blocca i CID risultanti da una chiamata esterna inoltrata dal sistema. I CID interni hanno accesso.
*  **Rimuovi CNAM**: il CNAM verrà rimosso dai CID che passano per questo Fascio.
*  **Forza CID Fascio**: usa sempre il CID definito in questo Fascio a meno che non faccia parte di una rotta di emergenza con un CID di emergenza definito per l'interno.

Numero Massimo di Canali
~~~~~~~~~~~~~~~~~~~~~~~~

Controlla il numero massimo di canali (chiamate contemporanee) che possono essere usate da questo fascio, incluso le chiamate entranti e uscenti. Lasciare vuoto per nessun limite.

Disabilita il fascio
~~~~~~~~~~~~~~~~~~~~

Permette di disabilitare il Fascio da tutte le :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` dove è presente.

Controlla Guasti Fascio
~~~~~~~~~~~~~~~~~~~~~~~

Se impostato su Attiva, immettere il nome di uno script caricato sul |product| che sarà chiamato per notificare il malfunzionamento del Fascio.

Regole per le Chiamate in Uscita
--------------------------------

E' possibile sul Fascio limitare le chiamate permesse per questo Fascio.  
Questa limitazione arriva dopo quella possibile sulle :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>`.

*  Anteponi: inserire le cifre che il |product| aggiungerà al numero chiamato prima di effettuare la chiamata. Non è possibile per ovvie ragioni usare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.
*  Prefisso: inserire le cifre che devono essere tolte dal |product| a partire dall'inizio del numero chiamato prima di effettuare la chiamata. Non è possibile per ovvie ragioni usare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.
*  Modello Corrispondente: inserire il modello di chiamata in uscita che la Rotta in Uscita deve considerare. E' possibile utilizzare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.

Wizard Regole di Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~

Con il menù del Wizard Modelli di chiamata è possibile caricare uno tra i tipi di chiamata che si trovano in elenco, con o senza prefisso d'uscita.

Prefisso Chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire qui un prefisso da aggiungere a tutte le chiamate in uscita.

Impostazioni in Uscita
----------------------

Nome Fascio
~~~~~~~~~~~

Nome da dare alla parte PEER del Fascio. Deve essere univoco, non può essere comune a più Fasci.

Dettagli PEER
~~~~~~~~~~~~~

Parametri per la connessione PEER del Fascio. L'ordine delle righe è importante.

Impostazioni in Entrata
-----------------------

Contesto UTENTE (USER)
~~~~~~~~~~~~~~~~~~~~~~

Inserire l'utente per la parte USER del Fascio.

Dettagli UTENTE
~~~~~~~~~~~~~~~

Parametri per configurare la parte USER del Fascio. L'ordine delle righe è importante.

Stringa di registrazione
~~~~~~~~~~~~~~~~~~~~~~~~

Stringa di registrazione del Fascio. Può essere richiesta da alcuni provider Voip ad esempio.

.. _fasci_sip_ref_label:

Fasci SIP
=========

Descrizione
-----------

I Fasci SIP permettono di collegare il |product| a delle fonti telefoniche tramite il protocollo SIP.

I Fasci SIP si usano ad esempio per collegare un provider Voip, vedi :ref:`qui <configurazione_provider_voip_ref_label>` e i Gateway, vedi :ref:`qui <configurazione_gateway_ref_label>`.

Se il Fascio è utilizzato in qualche :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` viene notificato in alto.

Sul menù di sinistra si trovano tutti i Fasci già creati, se evidenziati in grigio i Fasci sono disabilitati.

Configurazione
--------------

Nome Fascio
~~~~~~~~~~~

Nome descrittivo per individuare il Fascio.

Identificativo Chiamante in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ID Chiamante per le chiamate in uscita con questo Fascio.

Formato: <###########>. Può essere anche usato il formato "hidden" <#########> per nascondere l'ID Chiamante se supportato dal gestore della linea.

Opzioni CID
~~~~~~~~~~~

Determina a quali CID sarà consentito utilizzare questo Fascio. 
Gli ID di emergenza definiti sugli interni, vedi :ref:`qui <interni_sip_ref_label>`, potranno **sempre** usare questo Fascio se è in una Rotta di Emergenza.

-  **Permetti tutti i CID**: tutti gli ID Chiamante, inclusi quelli esterni inoltrati dalle chiamate esterne, avranno accesso a questo Fascio.
-  **Blocca CID esterni**: blocca i CID risultanti da una chiamata esterna inoltrata dal sistema. I CID interni hanno accesso.
-  **Rimuovi CNAM**: il CNAM verrà rimosso dai CID che passano per questo Fascio.
-  **Forza CID Fascio**: usa sempre il CID definito in questo Fascio a meno che non faccia parte di una rotta di emergenza con un CID di emergenza definito per l'interno.

Numero Massimo di Canali
~~~~~~~~~~~~~~~~~~~~~~~~

Controlla il numero massimo di canali (chiamate contemporanee) che possono essere usate da questo fascio, incluso le chiamate entranti e uscenti. Lasciare vuoto per nessun limite.

Disabilita il fascio
~~~~~~~~~~~~~~~~~~~~

Permette di disabilitare il Fascio da tutte le :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` dove è presente.

Controlla Guasti Fascio
~~~~~~~~~~~~~~~~~~~~~~~

Se impostato su Attiva, immettere il nome di uno script caricato sul |product| che sarà chiamato per notificare il malfunzionamento del Fascio.

Protocollo T38
~~~~~~~~~~~~~~

Se attivato, il protocollo T38 sarà abilitato per inviare fax utilizzando questo Fascio.

Regole per le Chiamate in Uscita
--------------------------------

E' possibile sul Fascio limitare le chiamate permesse per questo Fascio. 
Questa limitazione arriva dopo quella possibile sulle :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>`.

*  Anteponi: inserire le cifre che il |product| aggiungerà al numero chiamato prima di effettuare la chiamata. Non è possibile per ovvie ragioni usare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.
*  Prefisso: inserire le cifre che devono essere tolte dal |product| a partire dall'inizio del numero chiamato prima di effettuare la chiamata. Non è possibile per ovvie ragioni usare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.
*  Modello Corrispondente: inserire il modello di chiamata in uscita che la Rotta in Uscita deve considerare. E' possibile utilizzare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.

Wizard Regole di Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~

Con il menù del Wizard Modelli di chiamata è possibile caricare uno tra i tipi di chiamata che si trovano in elenco, con o senza prefisso d'uscita.

Prefisso Chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire qui un prefisso da aggiungere a tutte le chiamate in uscita.

Impostazioni in Uscita
----------------------

Nome Fascio
~~~~~~~~~~~

Nome da dare alla parte PEER del Fascio. Deve essere univoco, non può essere comune a più Fasci.

Dettagli PEER
~~~~~~~~~~~~~

Parametri per la connessione PEER del Fascio. L'ordine delle righe è importante.

Impostazioni in Entrata
-----------------------

Contesto UTENTE (USER)
~~~~~~~~~~~~~~~~~~~~~~

Inserire l'utente per la parte USER del Fascio.

Dettagli UTENTE
~~~~~~~~~~~~~~~

Parametri per configurare la parte USER del Fascio. L'ordine delle righe è importante.

Stringa di registrazione
~~~~~~~~~~~~~~~~~~~~~~~~

Stringa di registrazione del Fascio. Può essere richiesta da alcuni provider Voip ad esempio.

.. _fasci_dahdi_ref_label:

Fasci DAHDI
===========

Descrizione
-----------

I Fasci DAHDI permettono di collegare il |product| a delle fonti telefoniche tramite schede interne.

Se il Fascio è utilizzato in qualche :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` viene notificato in alto.

Sul menù di sinistra si trovano tutti i Fasci già creati, se evidenziati in grigio i Fasci sono disabilitati.

Configurazione
--------------

Nome Fascio
~~~~~~~~~~~

Nome descrittivo per individuare il Fascio.

Identificativo Chiamante in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ID Chiamante per le chiamate in uscita con questo Fascio.

Formato: <###########>. Può essere anche usato il formato "hidden" <#########> per nascondere l'ID Chiamante se supportato dal gestore della linea.

Opzioni CID
~~~~~~~~~~~

Determina a quali CID sarà consentito utilizzare questo Fascio. 
Gli ID di emergenza definiti sugli interni, vedi :ref:`qui <interni_sip_ref_label>`, potranno **sempre** usare questo Fascio se è in una Rotta di Emergenza.

*  **Permetti tutti i CID**: tutti gli ID Chiamante, inclusi quelli esterni inoltrati dalle chiamate esterne, avranno accesso a questo Fascio.
*  **Blocca CID esterni**: blocca i CID risultanti da una chiamata esterna inoltrata dal sistema. I CID interni hanno accesso.
*  **Rimuovi CNAM**: il CNAM verrà rimosso dai CID che passano per questo Fascio.
*  **Forza CID Fascio**: usa sempre il CID definito in questo Fascio a meno che non faccia parte di una rotta di emergenza con un CID di emergenza definito per l'interno.

Numero Massimo di Canali
~~~~~~~~~~~~~~~~~~~~~~~~

Controlla il numero massimo di canali (chiamate contemporanee) che possono essere usate da questo fascio, incluso le chiamate entranti e uscenti. Lasciare vuoto per nessun limite.

Disabilita il fascio
~~~~~~~~~~~~~~~~~~~~

Permette di disabilitare il Fascio da tutte le :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>` dove è presente.

Controlla Guasti Fascio
~~~~~~~~~~~~~~~~~~~~~~~

Se impostato su Attiva, immettere il nome di uno script caricato sul |product| che sarà chiamato per notificare il malfunzionamento del Fascio.

Regole per le Chiamate in Uscita
--------------------------------

E' possibile sul Fascio limitare le chiamate permesse per questo Fascio.
Questa limitazione arriva dopo quella possibile sulle :ref:`Rotta in Uscita <rotte_in_uscita_ref_label>`.

*  Anteponi: inserire le cifre che il |product| aggiungerà al numero chiamato prima di effettuare la chiamata. Non è possibile per ovvie ragioni usare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.
*  Prefisso: inserire le cifre che devono essere tolte dal |product| a partire dall'inizio del numero chiamato prima di effettuare la chiamata. Non è possibile per ovvie ragioni usare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.
*  Modello Corrispondente: inserire il modello di chiamata in uscita che la Rotta in Uscita deve considerare. E' possibile utilizzare i :ref:`pattern di Asterisk <pattern_ref_label>` in questo campo.

Wizard Regole di Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~

Con il menù del Wizard Modelli di chiamata è possibile caricare uno tra i tipi di chiamata che si trovano in elenco, con o senza prefisso d'uscita.

Prefisso Chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire qui un prefisso da aggiungere a tutte le chiamate in uscita.

Impostazioni in Uscita
----------------------

DAHDI Trunks
~~~~~~~~~~~~

Canale e Gruppo DAHDI disponibili da collegare al Fascio, indicare la porta e se iniziare dal primo canale o dall'ultimo del gruppo.

.. _configurazione_provider_voip_ref_label:

Configurazione Provider Voip
============================

Descrizione
-----------

Il wizard per la configurazione di provider voip ha lo scopo di semplificare la creazione di un :ref:`Fascio Sip <fasci_sip_ref_label>` che collegherà il |product| con il provider.

I provider al momento supportati sono **Eutelia**, **Messagenet**, **Squillo**, **VoipVoice**, **Enjoip** e **Cheapnet**, stiamo lavorando per estendere questo elenco il più possibile.

Inoltre è possibile collegare un account **Skype** tramite la modalità **Skype Connect**, con un account **Skype** business dove è stata abilitata, rende possibile utilizzare le tariffe di **Skype** per effettuare delle chiamate esterne. Stiamo lavorando per estendere l'integrazione con **Skype** alla possibilità di ricevere chiamate dagli account **Skype** oltre ad integrare la rubrica dell'account **Skype** nel |product|.

Se si vuole configurare un provider non presente in elenco, il consiglio è partire dalla configurazione di Eutelia ed adattarla secondo le esigenze.

Nota per la Ricezione delle chiamate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In situazioni particolari è necessario per registrare il fascio sip sul provider dichiarare il proprio ip pubblico. Se la registrazione del fascio va in errore, per controllarne lo stato vedi :ref:`qui <cli_ref_label>`, si può provare a configurare nelle :ref:`Impostazioni SIP <impostazioni_sip_ref_label>` l'ip pubblico e le reti locali del |product|.

Configurazione
--------------

Provider
~~~~~~~~

Scegliere il Provider Voip che si vuole configurare.

Nome Fascio
~~~~~~~~~~~

Nome del fascio SIP che si andrà a creare.

Username
~~~~~~~~

Username per il collegamento con il Provider Voip, deve essere fornito dal Provider, spesso coincide con il numero di telefono.

Password
~~~~~~~~

Password fornita dal Provider Voip per il collegamento.

.. warning:: Per problemi di compatibilità con la stringa di registrazione, la password del fascio non può contenere il carattere /, se così fosse chiedere al Provider di rinnovarla

Numero Telefono
~~~~~~~~~~~~~~~

Numero di telefono fornito dal Provider Voip. Ricordarsi di creare una :ref:`Rotta in Entrata <rotte_in_entrata_ref_label>` se si vogliono ricevere chiamate.

Codec consentiti
~~~~~~~~~~~~~~~~

Codec utilizzabili con il Provider Voip, è possibile inserirne più di uno separandoli con una virgola.

Forza codec
~~~~~~~~~~~

Se spuntato solo i codec consentiti saranno abilitati, proibendo l'uso di altri codec.

