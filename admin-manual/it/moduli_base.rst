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

Password per questo interno. Può essere alfanumerica.

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

Asteirsk: ccbs\_available\_timer. Quanto tempo una richiesta di Richiama su Occupato deve rimane attiva, in secondi, prima di scadere se l'estensione chiamata era occupata al primo tentativo.

Timeout Richiama su Non Risposta
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Asteirsk: ccnr\_available\_timer. Quanto tempo una richiesta di Richiamata su Non Risposta deve rimanere attiva, in secondi, prima di scadere se l'estensione chiamata non ha risposto al primo tentativo.

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

Una suoneria particolare può essere utilizata per il Richiama su Occupato. Solo se l'interno è in modalità *generic* e la modalità di richiamata è Richiamata Diretta.

Prefisso ID Chiamante
~~~~~~~~~~~~~~~~~~~~~

Un prefisso ID chiamante opzionale può essere utilizzato per la richiamata. Funziona solo se la modalità dell'interno è *generic*.

Alert-Info per il chiamato
~~~~~~~~~~~~~~~~~~~~~~~~~~

Una suoneria differenziata configurata per essere mandata all'estensione da richiamare.

Perfisso ID Chiamante per il chiamato
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

.. warning::  L'indirizzo mittente della mail sarà @dominio del |product|, nel caso la posta non sia gestita direttamente dal |product| un dominio fittizio potrebbe portare problemi sull'invio della mail, vedi la documentazione di |service_product|.

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

.. _interni_sip_ref_label:

Interni SIP
===========

.. _interni_sip_callgroup_ref_label:

.. _interni_sip_pickupgroup_ref_label:

.. _interni_sip_voicemail_ref_label:

.. _interni_dahdi_ref_label:

Interni DAHDI
=============


.. _musiche_di_attesa_ref_label:

Musica di Attesa
================


Configurazione Patton
=====================
 :ref:`Configurazione Patton <configurazione_patton_ref_label>`


.. _wizard_provisioning_ref_label:

Wizard Provisioning
===================


.. _registrazioni_di_sistema_ref_label:

Registrazioni Sistema
=====================


.. _fasci_sip_ref_label:

Fasci SIP
=========


.. _fasci_iax_ref_label:

Fasci IAX
=========


.. _fasci_dahdi_ref_label:

Fasci DAHDI
===========


.. _configurazione_provider_voip_ref_label:

Configurazione Provider Voip
============================


