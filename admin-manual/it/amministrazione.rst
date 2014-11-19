===============
Amministrazione
===============

.. _amministratori_ref_label:

Amministratori
==============

Descrizione
-----------

|product|, di default, permette l'accesso all'interfaccia web al solo utente admin.

Nel caso si voglia consentire l'accesso ad un'utente diverso, deve essere prima creato sul |product_service| sottostante, accedendo alla pagina

::

  http://nome_server:980

sezione Collaborazione -> Utenti.

Questo nuovo utente deve, poi, diventare membro del gruppo **voicemanager**, operazione da effettuare nella sezione Gestione -> Gruppi.

Dopo aver eseguito queste operazioni, si deve accedere al modulo Amministratori e replicare l'utente appena creato sul |product_service| anche qui.

Creando un nuovo utente per interfaccia web del |product| è anche possibile limitarne l'accesso ad alcuni moduli e/o solo ad un intervallo di interni, code e gruppi di chiamata.

Configurazione
--------------

Nome utente
~~~~~~~~~~~

Indicare il nome utente, l'utente deve essere già stato creato sul |product_service|.

Restrizioni d'accesso
---------------------

Nome Dipartimento
~~~~~~~~~~~~~~~~~

Restringe la visualizzazione per questo utente a IVR e Registrazioni di Sistema che appartengono a questo dipartimento.

Intervallo Interni
~~~~~~~~~~~~~~~~~~

Possibilità di restringere l'accesso per l'utente ad un intervallo di numerazioni, comprende Interni, Gruppi di Chiamata e Code.

Accesso Amministratore
~~~~~~~~~~~~~~~~~~~~~~

Selezionare i moduli di |product| a cui consentire l'accesso all'utente.

.. _api_asterisk_ref_label:

Api Asterisk
============

Descrizione
-----------

|product| permette ad un programma client di connettersi ad una istanza Asterisk ed impartire comandi o rilevare eventi del |product| su una connessione TCP/IP tramite l'interfaccia **Asterisk Manager Interface** (AMI).

Molti programmi si basano su questo collegamento, anche il |product_cti| ad esempio, per collegarsi a centralini basati su Asterisk ed effettuare operazioni.

|product| rende disponibile questo collegamento sulla porta TCP 5038.

La comunicazione tra client e Asterisk server attraverso l'interfaccia manager avviene tramite un semplice protocollo testuale di tipo request/response basato su linee strutturate come "chiave: valore".

Il modulo Api Asterisk aiuta nella creazione di un'utente per collegarsi all'interfaccia AMI e nella definizione dei permessi e delle restrizioni al suo accesso.

Configurazione
--------------

Nome Manager
~~~~~~~~~~~~

Nome utente, inserire senza spazi ed evitando caratteri speciali.

Password Manager
~~~~~~~~~~~~~~~~

Password utente, inserire senza spazi.

Nega
~~~~

Reti ip dalle quali non consentire l'accesso all'utente, utilizzare il carattere & come separatore tra le reti.

Permetti
~~~~~~~~

Reti ip dalle quali consentire l'accesso all'utente, utilizzare il carattere & come separatore tra le reti.

Permessi
~~~~~~~~

Elenco delle varie azioni possibili per l'utente. Per maggiori informazioni riferirsi alla documentazione di Asterisk.

Spuntando il campo ALL si abilitano tutte le azioni disponibili.

.. _impostazioni_iax_ref_label:
   
Impostazioni IAX
================

Descrizione
-----------

Impostazioni per la gestione del protocollo IAX.

Codec audio
-----------

Codec
~~~~~

Codec abilitati e priorità per l'utilizzo su |product|, gli altri saranno disabilitati a meno che non indicati su :ref:`Fasci <fasci_sip_ref_label>` o :ref:`Interni <interni_sip_ref_label>`.

Priorità Codec
~~~~~~~~~~~~~~

Gestisce la negoziazione del codec durante le chiamate ricevute in IAX.
Questa opzione è ereditata da tutti gli apparati e utenti a meno che non venga specificata diversamente.

Occupazione Banda
~~~~~~~~~~~~~~~~~

Controllo sull'occupazione della banda.

Codec Video
-----------

Supporto Video
~~~~~~~~~~~~~~

Abilitazioni/Disabilitazione della Video Chiamata.

Impostazioni di Registrazione
-----------------------------

Tempi di Registrazione
~~~~~~~~~~~~~~~~~~~~~~

Durata minima e massima di una registrazione per interni IAX.

Impostazioni Buffer Jitter
--------------------------

Buffer Jitter
~~~~~~~~~~~~~

Abilita l'uso del Buffer Jitter.

Impostazioni Avanzate
---------------------

Lingua
~~~~~~

Lingua.

Indirizzo Utilizzato
~~~~~~~~~~~~~~~~~~~~

Ip dove è in ascolto Asterisk. Inserire 0.0.0.0 per tutti gli ip del |product|.

Porta Utilizzata
~~~~~~~~~~~~~~~~

Porta UDP utilizzata da Asterisk per il IAX.

Ritardo autenticazione rifiutata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitare il ritardo di autenticazione rifiutata per introdurre un timeout per accettare una connessione dopo un rifiuto.

Altre Impostazioni IAX
~~~~~~~~~~~~~~~~~~~~~~

E' possibile aggiungere altre impostazioni IAX.

.. _impostazioni_sip_ref_label:

Impostazioni SIP
================

Descrizione
-----------

Impostazioni per la gestione del protocollo SIP.

Impostazioni NAT
----------------

NAT
~~~

Impostazioni NAT Asterisk:
*  **force\_rport**: forza RFC 3581 e disabilita il supporto RTP simmetrico.
*  **comedia**: consente RFC 3581 se richiesto da remoto e consente il supporto RTP simmetrico.
*  **force\_rport,comedia**: Entrambi i comportamenti.

Configurazione IP
~~~~~~~~~~~~~~~~~

Configurazione dell'IP del |product|, se pubblico, dinamico o statico.

IP Esterno
~~~~~~~~~~

Ip con il quale il |product| si presenta su internet, è possibile calcolarlo con Configura Automaticamente.

Reti Locali
~~~~~~~~~~~

Rete locale del |product| dalla quale accettare connessioni e l'uso dei servizi, è possibile calcolarla con Configura Automaticamente e aggiungerne una tramite Aggiungi Campo Rete Locale.

Codec Audio
-----------

Codec
~~~~~

Codec abilitati e priorità per l'utilizzo su |product|, gli altri saranno disabilitati a meno che non indicati su :ref:`Fasci <fasci_sip_ref_label>` o :ref:`Interni <interni_sip_ref_label>`.

Non-Standard g726
~~~~~~~~~~~~~~~~~

Comportamento del |product| con il codec g726 non standard.

T38 Pass-Through
~~~~~~~~~~~~~~~~

Attivazione/Disattivazione del protocollo T38.

Codec Video
-----------

Supporto Video
~~~~~~~~~~~~~~

Abilitazioni/Disabilitazione della Video Chiamata e codec abilitati e priorità.

Massima Frequenza Bit
~~~~~~~~~~~~~~~~~~~~~

Banda massima per le Video Chiamate.

Impostazioni MEDIA e RTP
------------------------

Comportamento Reinvite
~~~~~~~~~~~~~~~~~~~~~~

Comportamento del |product| per il Reinvite, si, no, solo se non dietro a nat e UPDATE al posto di INVITE.

Timer RTP
~~~~~~~~~

Timeout per chiusura della chiamata dopo inattività su RTP o RTCP, timeout per terminare la chiamata in attesa se non si ha attività RTP o RTCP, invia keepalives net canale RTP per tenere il NAT aperto durante i momenti senza streming RTP.

Notifiche e WMI
---------------

Frequenza Verifica MWI
~~~~~~~~~~~~~~~~~~~~~~

Frequenza in secondi con cui controllare lo stato MWI.

Notifica Ringing
~~~~~~~~~~~~~~~~

Controlla se sottoscrizioni occupati ottengono il segnale di ringing, utile per i BLF.

Notifica Attesa
~~~~~~~~~~~~~~~

Controlla se sottoscrizioni occupati ottengono il segnale di attesa, utile per i BLF.

Impostazioni di Registrazione
-----------------------------

Registrazioni
~~~~~~~~~~~~~

Numero di secondi ogni quale ritentare una registrazione finché non si ha successo e numero massimo di tentativi, zero per illimitato.

Tempi di Registrazione
~~~~~~~~~~~~~~~~~~~~~~

Durata minima e massima di una registrazione e durata standard.

Impostazioni Buffer Jitter
--------------------------

Buffer Jitter
~~~~~~~~~~~~~

Abilita l'uso del Buffer Jitter.

Impostazioni Avanzate
---------------------

Lingua
~~~~~~

Lingua.

Contesto Default
~~~~~~~~~~~~~~~~

Contesto Asterisk di default per le chiamate ricevute dove non specificato.

Indirizzo Utilizzato
~~~~~~~~~~~~~~~~~~~~

Ip dove è in ascolto Asterisk. Inserire 0.0.0.0 per tutti gli ip del |product|.

Porta Utilizzata
~~~~~~~~~~~~~~~~

Porta UDP utilizzata da Asterisk per il SIP.

Permetti SIP non Autenticati
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se abilitato permette chiamate SIP non autenticate.

Risoluzione Server
~~~~~~~~~~~~~~~~~~

Abilita Asterisk srvlookup.

Eventi su Chiamata
~~~~~~~~~~~~~~~~~~

Genera Eventi nel Manager quando un useragent SIP genera Eventi.

Impostazioni SIP
~~~~~~~~~~~~~~~~

E' possibile aggiungere altre impostazioni SIP.

.. _call_debugger_ref_label:

Call Debugger
=============

Descrizione
-----------

Il modulo Call Debugger aiuta a raccogliere dai log di |product| tutte le informazioni riguardanti una chiamata e a raggrupparle per controllare passo dopo passo cosa è successo nella chiamata selezionata.

Selezionando una chiamata, quindi, verrà raggruppato tutto il log che la riguarda e proposto per valutare eventuali problemi o comportamenti strani.

Il modulo non nasce per effettuare una consultazione di dati a ritroso nel tempo ma per avere il log di una chiamata molto recente, praticamente appena effettuata, fatta per riprodurre un comportamento sbagliato o un errore.

Configurazione
--------------

Selezionare il numero di ultime chiamate da visualizzare e il |product| le elencherà indicando data, ora e chiamante.
Cliccando sulla chiamata da visualizzare si apriranno tutte le chiamate generate, possono essere da una tante come ad esempio se si tratta di una chiamata destinata ad una :ref:`Coda <code_ref_label>` o ad un :ref:`Gruppo di Chiamata <gruppi_di_chiamata_ref_label>`.

Cliccando sulle varie chiamate si aprirà tutto il log correlato pronto per essere analizzato.

.. _contesti_personalizzati_ref_label:

Contesti Personalizzati
=======================

Descrizione
-----------

I Contesti Personalizzati, o classi di servizio, consentono di differenziare i vari `interni <Interni_|product|>`__ di |product| per limitarne le funzionalità.

Un :ref:`interno <interni_ref_label>` appena creato appartiene di default al contesto *from-internal* che consente ai suoi appartenenti di utilizzare tutte le funzionalità di |product| e tutte le :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` configurate.

Tramite questo modulo viene creato un contesto personalizzato equiparabile al contesto *from-internal* dove però c'è la possibilità di limitare funzionalità e risorse utilizzabili.

Una volta creato il contesto personalizzato è possibile associarci gli `interni <Interni_|product|>`__ tramite l'apposita opzione, vedi :ref:`qui <interni_sip_ref_label>`.

Configurazione
--------------

Dopo aver creato il contesto personalizzato inserendo Nome e Descrizione, si accede all'interfaccia per amministrarne i vari permessi.

Le scelte proposte sono:
*  **Permetti** (Allow)
*  **Nega** (Deny)
*  **Permetti Regole** (Allow Rules): per permettere solo se il numero chiamato corrisponde alle Regole di Chiamata indicate.
*  **Nega Regole** (Deny Rules): per negare solo se il numero chiamato corrisponde alle Regole di Chiamata indicate.
*  tutti i :ref:`Gruppi Temporali <gruppi_temporali_ref_label>` configurati per permettere la funzionalità solo negli orari indicati.

Il campo **Priorità** (Priority) serve ad avere un ordine delle varie regole in caso di conflitti, chiamata che interessa più regole.

**Priorità** numericamente più basse vengono controllate prima e quindi hanno una priorità più alta.

Contesto
~~~~~~~~

*  **Contesto**: nome del contesto personalizzato.
*  **Descrizione**: descrizione del contesto personalizzato.
*  **Regole di Chiamata**: indicando qui delle regole di chiamata, con la possibilità di utilizzare i :ref:`pattern <pattern_ref_label>` di Asterisk, tutti i componenti configurati con *Permetti Regole* saranno disponibili se il modello di chiamata corrisponde con quanto inserito, mentre tutti i componenti configurati a *Nega Regole* saranno disponibili se il modello di chiamata non corrisponde con quanto inserito.

Imposta Tutto a
~~~~~~~~~~~~~~~

*  **Imposta Tutto A**: possibilità di configurare tutti i componenti al valore scelto qui automaticamente, per velocizzare la configurazione.

Contesto Interno Standard
~~~~~~~~~~~~~~~~~~~~~~~~~

*  **Dialplan Interno Personalizzato**: accesso al contesto *from-internal-custom*.
*  **Parcheggio Chiamate**: accesso al contesto di parcheggio, vedi :ref:`qui <parcheggi_ref_label>`.
*  **TUTTO il Dialplan Interno**: accesso a tutto il dialplan di |product|, in pratica tutto quello elencato sotto, interni, funzionalità e :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

Dialplan Interno
~~~~~~~~~~~~~~~~

*  **Gruppi di Chiamata**: accesso ai :ref:`Gruppi di chiamata <gruppi_di_chiamata_ref_label>`.
*  **Gruppi di Chiamata**: accesso ai :ref:`Gruppi di chiamata <gruppi_di_chiamata_ref_label>`.
*  **Disattiva Trasferimento di Chiamata su Occupato**: accesso al codice per disattivare il :ref:`Trasferimento su Occupato <trasferimento_chiamata_ref_label>`.
*  **Disattiva Trasferimento di Chiamata su Occupato (chiede dettagli)**: accesso al codice per disattivare il :ref:`Trasferimento su Occupato <trasferimento_chiamata_ref_label>` chiedendo dettagli.
*  **Attiva Trasferimento di Chiamata su Occupato**: accesso al codice per attivare il :ref:`Trasferimento su Occupato <trasferimento_chiamata_ref_label>`.
*  **Disattiva Trasferimento di Chiamata Incondizionato**: accesso al codice per disattivare il :ref:`Trasferimento Incondizionato <trasferimento_chiamata_ref_label>`.
*  **Disattiva Trasferimento di Chiamata Incondizionato (chiede dettagli)**: accesso al codice per disattivare il :ref:`Trasferimento Incondizionato <trasferimento_chiamata_ref_label>` chiedendo dettagli.
*  **Attiva Trasferimento di Chiamata Incondizionato**: accesso al codice per attivare il :ref:`Trasferimento Incondizionato <trasferimento_chiamata_ref_label>`.
*  **Disattiva Trasferimento su Nessuna Risposta/Non disponibile**: accesso al codice per disattivare il :ref:`Trasferimento su Nessuna Risposta <trasferimento_chiamata_ref_label>`.
*  **Attiva Trasferimento su Nessuna Risposta/Non disponibile**: accesso al codice per attivare il :ref:`Trasferimento su Nessuna Risposta <trasferimento_chiamata_ref_label>`.
*  **Abilita/Disabilita Inoltro Chiamata**: accesso al codice per abilitare/disabilitare l':ref:`Inoltro di Chiamata <trasferimento_chiamata_ref_label>`.
*  **Abilita/Disabilita Inoltro Chiamata**: accesso al codice per abilitare/disabilitare l':ref:`Inoltro di Chiamata <trasferimento_chiamata_ref_label>`.
*  **Paging & Intercom**: accesso ai gruppi di :ref:`Paging <paging_e_intercom_ref_label>`.
*  **Disattiva Avviso di Chiamata**: accesso al codice per disattivare l':ref:`Avviso di Chiamata <avviso_chiamata_ref_label>`.
*  **Attiva Avviso di Chiamata**: accesso al codice per attivare l':ref:`Avviso di Chiamata <avviso_chiamata_ref_label>`.
*  **Attiva/Disattiva Seguimi**: accesso al codice per attivare/disattivare il :ref:`Seguimi <gestione_seguimi_ref_label>`.
*  **Seguimi**: accesso al :ref:`Seguimi <seguimi_ref_label>`.
*  **Seguimi**: accesso al :ref:`Seguimi <seguimi_ref_label>`.
*  **Registrazione Chiamate**: accesso al codice per la :ref:`Registrazione durante la Chiamata <codice_registrazione_ref_label>`.
*  **Ultima Chiamata**: accesso al codice per avere informazioni sull':ref:`Ultima Chiamata <ultima_chiamata_ref_label>`.
*  **Test Eco**: accesso al codice per effettuare un :ref:`Test Eco <test_eco_ref_label>`.
*  **Riproduce il Numero Interno**: accesso al codice per riprodurre il proprio :ref:`Interno <riproduce_ref_label>`.
*  **Data e Ora**: accesso al codice per avere riprodotti :ref:`Data e Orario <dataora_ref_label>`.
*  **Conferenze**: accesso alle :ref:`Conferenze <conferenze_ref_label>`.
*  **Esegui Dettatura**: accesso al codice per eseguire una :ref:`Dettatura <dettatura_ref_label>`.
*  **Invia Dettatura**: accesso al codice per effettuare una :ref:`Dettatura via email <dettatura_ref_label>`.
*  **Applicazioni Varie**: accesso ai codici creati per il modulo :ref:`Applicazioni Varie <applicazioni_varie_ref_label>`.
*  **Blocco Interni**: accesso ai codici del modulo :ref:`Blocco Interni <blocco_interni_ref_label>`.
*  **Casella Vocale**: accesso al codice per la :ref:`Casella Vocale <casella_vocale_ref_label>`.
*  **Casella Vocale Personale**: accesso al codice per la :ref:`Casella Vocale Personale <casella_vocale_ref_label>`.
*  **Controllo Flusso Chiamata**: accesso ai codici del modulo :ref:`Controllo Flusso Chiamata <controllo_flusso_chiamata_ref_label>`.
*  **Elenco Telefonico**: accesso al codice per l':ref:`Elenco Telefonico <elenco_ref_label>`.
*  **Gruppo di Caselle Vocali**: accesso ai `Gruppi di Caselle Vocali <gruppi_caselle_vocali_ref_label>`.
*  **Numeri Brevi**: accesso al codice per utilizzare i :ref:`Numeri Brevi <gestione_numeri_brevi_ref_label>`.
*  **Imposta CallerID**: accesso al modulo :ref:`Imposta CallerID <imposta_callerid_ref_label>`.
*  **Ripresa Chiamate Parcheggiate**: accesso alle chiamate parcheggiate del modulo :ref:`Parcheggi <parcheggi_ref_label>`.
*  **Richiama su Occupato Annullata**: accesso al codice per l'annullamento della funzionalità :ref:`Richiama su Occupato <campon_ref_label>`.
*  **Richiesta di Richiama su Occupato**: accesso al codice per la richiesta di :ref:`Richiamata su Occupato <campon_ref_label>`.
*  **Richiedi/Annulla Richiama su Occupato**: accesso al codice per richiedere/annullare :ref:`Richiamata su Occupato <campon_ref_label>`.
*  **Blacklist**: accesso ai codici utilizzati dal modulo :ref:`Blacklist <blackList_ref_label>`.
*  **Code**: accesso alle :ref:`Code <code_ref_label>`.
*  **Login/Logout Coda**: accesso al codice per il login/logout dalle :ref:`Code <gestione_code_ref_label>` come agente dinamico.
*  **Servizio Notte**: accesso ai codici del modulo :ref:`Servizio Notte <servizio_notte_ref_label>`.
*  **Direttore Segretaria**: accesso ai codici del modulo :ref:`Direttore Segretaria <direttore_segretaria_ref_label>`.
*  **Disattiva Non-Disturbare (DND)**: accesso al codice per la disattivazione del :ref:`Non Disturbare <dnd_ref_label>`.
*  **Attiva Non-Disturbare (DND)**: accesso al codice per l'attivazione del :ref:`Non Disturbare <dnd_ref_label>`.
*  **Attiva/Disattiva DND**: accesso al codice per attivare/disattivare il :ref:`Non Disturbare <dnd_ref_label>`.
*  **Attiva/Disattiva DND**: accesso al codice per attivare/disattivare il :ref:`Non Disturbare <dnd_ref_label>`.
*  **Connessione/Disconnessione Utente**: accesso al codice per la connessione/disconnessione :ref:`Utente <disconnessione_utente_ref_label>`.
*  **Conferma Chiamata**: accesso alla funzionalità di conferma chiamata, tipica di :ref:`Gruppi di Chiamata <gruppi_di_chiamata_ref_label>`, :ref:`Seguimi <seguimi_ref_label>`, :ref:`Code <code_ref_label>`.
*  **Seguimi Squillo Interno Primario**: accesso alla funzionalità del :ref:`Seguimi <seguimi_ref_label>` per lo squillo dell'interno principale.
*  **Call Pickup Diretto**: accesso al codice per il :ref:`Pickup Diretto <pickup_diretto_ref_label>`.
*  **ZapBarge**: accesso al codice per il :ref:`ZapBarge <zapbarge_ref_label>`.
*  **ChanSpy**: accesso al codice per il :ref:`ChanSpy <spy_ref_label>`.
*  **Simulazione Chiamata in Entrata**: accesso al codice per la :ref:`Simulazione Chiamata in Entrata <simulazione_chiamata_ref_label>`.
*  **Chiamate Interne**: permesso per chiamare gli interni del |product|.
*  **TUTTE LE ROTTE IN USCITA**: permesso per utilizzare tutte le :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` configurate su |product|.

Rotte in Uscita
~~~~~~~~~~~~~~~

In questa sezione vengono elencate tutte le :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` configurate su |product| in modo da singolarmente rotta per rotta permettere o negare l'accesso agli interni di questo contesto personalizzato.

Le :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` vengono elencate con il nome scelto in fase di configurazione.

Se in una :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` è stato configurato un Gruppo Temporale per limitare l'utilizzo della Rotta in fasce orarie, la :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>` verrà proposta una volta per ogni fascia oraria configurata, andare con il mouse sul punto interrogativo per capire di che fascia di tempo si tratta.

Destinazione di Failover
~~~~~~~~~~~~~~~~~~~~~~~~

Quando un interno di questo contesto prova a utilizzare o contattare una parte del dialplan che gli è stata vietata è necessario definire come il |product| debba gestire la chiamata, in pratica dove destinare la chiamata al posto della destinazione voluta.

Destinazione su Fallimento
^^^^^^^^^^^^^^^^^^^^^^^^^^

*  **PIN**: inserire un codice numerico per richiedere un'autenticazione prima di procedere alla destinazione selezionato sotto.
*  **Destinazione su Fallimento**: inserire la destinazione della chiamata fatta a una parte del dialplan vietato.

Destinazione su Fallimento Codici Servizi
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*  **PIN**: inserire un codice numerico per richiedere un'autenticazione prima di procedere alla destinazione selezionato sotto.
*  **Destinazione su Fallimento**: inserire la destinazione della chiamata verso un Codice Servizio vietato.

.. _amministrazione_contesti_personalizzati_ref_label:

Amministrazione Contesti Personalizzati
=======================================

Descrizione
-----------

Il modulo Amministrazione Contesti Personalizzati permette di apportare modificare al contesto *from-internal*, contesto base di |product|; quello a cui, ad esempio, appartengono di default tutti gli :ref:`interni <interni_ref_label>` appena creati e che di default consente l'accesso a tutte le funzionalità, applicazioni e risorse di |product|.

E' possibile, quindi, modificare il contesto *from-internal* aggiungendo dei sotto contesti, che poi possono essere usati in varie modalità anche da altri moduli di |product|, o cancellando quelli esistenti.

Il modulo offre anche la possibilità di modificare la descrizione dei componenti del contesto *from-internal*, di tutti gli eventuali sotto contesti, di tutte le funzionalità e applicazioni incluse.

Queste descrizioni poi verranno riportate anche in ogni :ref:`Contesto Personalizzato <contesti_personalizzati_ref_label>` creato tramite l'apposito modulo, vedi :ref:`qui <contesti_personalizzati_ref_label>` e quindi sono di aiuto per individuare velocemente le parti da modificare.

.. _codici_servizi_ref_label:

Codici Servizi
==============

Descrizione
-----------

Il modulo Codici Servizi elenca tutti i comandi del |product| utilizzabili da un qualsiasi apparecchio registrato.

Per utilizzare uno di questi codici basta semplicemente fare una telefona utilizzando il codice come numero da chiamare.

Ogni codice ha un valore di default, ripristinabile cliccando su Utilizzare Predefinito.

E' possibile personalizzare ogni codice variandolo dal default, raccomandiamo di agire però con molta prudenza per con creare conflitti tra codici e anche con gli altri moduli del |product|, interni, gruppi di chiamata, code etc.

Tutti i codici possono essere disattivati.

Configurazione
--------------

Blacklist
---------

Vedi modulo :ref:`Blacklist <blackList_ref_label>`.

Direttore Segretaria
--------------------

Vedi modulo :ref:`Direttore Segretaria <direttore_segretaria_ref_label>`.

.. _trasferimento_chiamata_ref_label:

Trasferimento di Chiamata
-------------------------

Attiva Trasferimento di Chiamata Incondizionato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attivazione del trasferimento di chiamata incondizionato.

Digitando solo il codice verrà chiesto prima su quale interno attivarlo e poi verso quale numero.

Digitando il codice seguito dal numero al quale trasferire le chiamate il |product| darà per scontato che l'interno su cui attivare il trasferimento è quello da cui si sta chiamando.

Disattiva Trasferimento di Chiamata Incondizionato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disattivazione del trasferimento di chiamata incondizionato per l'interno dal quale si è digitato il codice.

Disattiva Trasferimento di Chiamata Incondizionato (chiede dettagli)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disattivazione del trasferimento di chiamata incondizionato, verrà chiesto per quale interno effettuarlo.

Attiva Trasferimento di Chiamata su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attivazione del trasferimento di chiamata su occupato.

Digitando solo il codice verrà chiesto prima su quale interno attivarlo e poi verso quale numero.

Digitando il codice seguito dal numero al quale trasferire le chiamate il |product| darà per scontato che l'interno su cui attivare il trasferimento è quello da cui si sta chiamando.

Disattiva Trasferimento di Chiamata su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disattivazione del trasferimento di chiamata su occupato per l'interno dal quale si è digitato il codice.

Disattiva Trasferimento di Chiamata su Occupato (chiede dettagli)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disattivazione del trasferimento di chiamata su occupato, verrà chiesto per quale interno effettuarlo.

Attiva Trasferimento su Nessuna Risposta/Non disponibile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attivazione del trasferimento di chiamata su nessuna risposta/non disponibile.

Digitando solo il codice verrà chiesto prima su quale interno attivarlo e poi verso quale numero.

Digitando il codice seguito dal numero al quale trasferire le chiamate il |product| darà per scontato che l'interno su cui attivare il trasferimento è quello da cui si sta chiamando.

Disattiva Trasferimento su Nessuna Risposta/Non disponibile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disattivazione del trasferimento di chiamata su nessuna risposta/non disponibile per l'interno dal quale si è digitato il codice.

Abilita/Disabilita Inoltro Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitazione e disattivazione inoltro di chiamata generale con codice unico, utile se si vuole mappare la funzionalità su un tasto BLF di un telefono, verrà chiesto di inserire il numero di destinazione dando per scontato che si vuole attivare l'inoltro dall'interno da cui si sta chiamando.

.. _avviso_chiamata_ref_label:

Avviso di Chiamata
------------------

Attiva Avviso di Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per attivare l'avviso di chiamata sull'interno da cui è stato digitato, cioè non essere considerato occupato dal |product| se impegnati in una conversazione. Da attivare se gli apparecchi telefonici sono in grado di gestire più chiamate contemporaneamente.

Disattiva Avviso di Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disattivazione dell'avviso di chiamata per l'interno da cui si sta chiamando.

.. _campon_ref_label:

Richiama su Occupato
--------------------

Richiama su Occupato Annullata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se è stata fatta una richiesta di richiamata su occupato, chiamando questo codice viene annullata. Vedi :ref:`qui <funzionalita_base_ref_label>`.

Richiesta di Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dopo una chiamata che ha dato occupato, chiamando questo codice viene attivato il servizio di Richiamata, il |product| proverà a ricontattare il numero e in caso di esito positivo metterà in comunicazione il chiamato con l'interno. Vedi :ref:`qui <funzionalita_base_ref_label>`.

Richiedi/Annulla Richiama su Occupato
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per attivare/disattivare la richiesta di richiama su occupato, utile per essere utilizzato su un tasto funzione di un apparecchio telefonico. Vedi :ref:`qui <funzionalita_base_ref_label>`.

Sistema
-------

.. _pickup_generale_ref_label:

Call Pickup Generale di Asterisk
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vedi :ref:`qui <funzionalita_base_ref_label>`.

.. _spy_ref_label:

ChanSpy
~~~~~~~

Codice per intromettersi in una chiamata in corso sul |product| in modalità spia, solo in ascolto.

.. _pickup_diretto_ref_label:

Call Pickup Diretto
~~~~~~~~~~~~~~~~~~~

Vedi :ref:`qui <funzionalita_base_ref_label>`.

.. _trasferimento_assistito_ref_label:

Trasferimento di chiamata assistito
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vedi :ref:`qui <funzionalita_base_ref_label>`.

.. _trasferimento_diretto_ref_label:

Trasferimento di chiamata diretto
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vedi :ref:`qui <funzionalita_base_ref_label>`.

.. _riaggancio_chiamata_ref_label:

Riaggancio chiamata
~~~~~~~~~~~~~~~~~~~

Codice per riagganciare una chiamata in corso.

In-Call Asterisk Timeout in millisecondi nella digitazione di una di queste funzioni
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Timeout in millesecondi che il |product| aspetta una volta digitato un tasto di un Codice Servizio la digitazione del successivo. Non abbassarlo sotto i 1000 millesecondi per non avere problemi nell'usare i Codici Servizi.

In-Call Asterisk Timeout in secondi nel trasferimento consultativo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Timeout in secondi che il |product| aspetta dopo la digitazione del comando di trasferimento consultativo, la digitazione dell'interno a cui trasferire. Alzarlo di molto per usare il codice di trasferimento consultativo come una attesa per i telefoni che non hanno questa funzionalità.

In-Call Asterisk Timeout in secondi nella digitazione del trasferimento di chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Timeout in secondi che il |product| aspetta dopo la digitazione del comando di trasferimento di chiamata.

In-Call Asterisk Timeout su nessuna risposta trasferimento consultativo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Timeout in secondi in cui il |product| contatta la destinazione del trasferimento prima di dichiararla non disponibile.

.. _codice_registrazione_ref_label:

Registrazione durante la chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per la registrazione su richiesta di una telefonata in corso.

.. _simulazione_chiamata_ref_label:

Simulazione Chiamata in Entrata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per simulare una chiamata in entrata, serve a verificare la corretta configurazione del |product|.

.. _disconnessione_utente_ref_label:

Disconnessione Utente
~~~~~~~~~~~~~~~~~~~~~

Codice disconnessione utente.

.. _connessione_utente_ref_label:

Connessione Utente
~~~~~~~~~~~~~~~~~~

Codice connessione utente.

.. _zapbarge_ref_label:

ZapBarge
~~~~~~~~

Codice di intromissione per chiamate fatte su tecnologia DAHDI.

Controllo Flusso di Chiamata
----------------------------

Codici per l'amministrazione dei :ref:`Controllo Flusso Chiamata <controllo_flusso_chiamata_ref_label>` configurati.

.. _dettatura_ref_label:

Dettatura
---------

Email dettatura completata
~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per effettuare una dettatura e inviarla via email.

Esegui dettatura
~~~~~~~~~~~~~~~~

Codice per eseguire una dettatura.

.. _dnd_ref_label:

Non-Disturbare (DND)
--------------------

Attiva Non-Disturbare (DND)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attiva il non disturbare.

Disattiva Non-Disturbare (DND)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disattiva il non disturbare.

Attiva/Disattiva DND
~~~~~~~~~~~~~~~~~~~~

Codice univoco per attivare/disattivare il non disturbare, utile per mapparlo su un tasto funzione di un apparecchio telefonico.

.. _gestione_seguimi_ref_label:

Seguimi
-------

Attiva/Disattiva Seguimi
~~~~~~~~~~~~~~~~~~~~~~~~

Attiva/disattiva il `Seguimi <Seguimi_|product|>`__ dell'interno da cui è stata effettuata la chiamata.

Servizi Aggiuntivi
------------------

.. _ultima_chiamata_ref_label:

Ultima Chiamata
~~~~~~~~~~~~~~~

Codice per avere dal |product| informazioni sull'ultima chiamata ricevuta.

.. _test_eco_ref_label:

Test Eco
~~~~~~~~

Codice per attivare il test dell'eco. Ogni cosa che viene detta dal microfono dell'apparecchio telefonico verrà ripetuta dal |product|.

Il test ha lo scopo per rendersi conto della latenza tra apparecchio telefonico e |product|.

.. _riproduce_ref_label:

Riproduce il Numero d'Interno
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per avere riprodotto dal |product| il numero dell'interno dal quale si sta chiamando.

.. _dataora_ref_label:

Data e Ora
~~~~~~~~~~

Codice per avere riprodotto dal |product| ora e data corrente.

Blocco Interni
--------------

Vedi modulo :ref:`Blocco Interni <blocco_interni_ref_label>`.

Applicazioni Varie
------------------

Codici per le :ref:`Applicazioni Varie <applicazioni_varie_ref_label>` create.

Gestione Camere
---------------

Codici del modulo :doc:`|product_hotel| <hotel>`.

Assegna un extra ad una camera.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per assegnare un extra ad una camera. La sintassi è codice (il default è \*33), numero camera, cancelletto (#), id extra su due cifre, cancelletto (#). quantità su due cifre.

Configura la sveglia da una camera.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per configurare la sveglia della camera.

Configura la sveglia di una camera.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per configurare la sveglia di una camera qualsiasi, di solito lo usa la receptionist.

Effettua il check-in/check-out di una camera.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per effettuare il checkin/checkout di una camere, la sintassi è codice (il default è 967) seguito dal numero della camera.

Pulizia camera
~~~~~~~~~~~~~~

Codice per marcare pulita la camera dal quale si chiama.

.. _gestione_numeri_brevi_ref_label:

Numeri Brevi
------------

Accesso Numeri Brevi
~~~~~~~~~~~~~~~~~~~~

Vedi :ref:`qui <numeri_brevi_ref_label>`.

Paging e Intercom
-----------------

Prefisso Intercom
~~~~~~~~~~~~~~~~~

Codice per effettuare una chiamata intercom.

Permette Intercom
~~~~~~~~~~~~~~~~~

Codice per consentire l'intercom.

Non permette Intercom
~~~~~~~~~~~~~~~~~~~~~

Codice per vietare l'intercom.

.. _gestione_parcheggi_ref_label:

Parcheggi
---------

Intercetta qualsiasi chiamata Parcheggiata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per intercettare una qualsiasi chiamata parcheggiata, vedi anche :ref:`qui <parcheggi_ref_label>`.

.. _elenco_ref_label:

Elenco Telefonico (Directory)
-----------------------------

Elenco Telefonico chiama-per-nome
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Codice per fare una ricerca alfabetica sul |product| tra gli interni.

.. _gestione_code_ref_label:

Code
----

Login/Logout Coda
~~~~~~~~~~~~~~~~~

Codice per loggarsi/sloggarsi dalle :ref:`Code <code_ref_label>` dove si è registrati come Agente Dinamico.

.. _gestione_registrazioni_ref_label:

Registrazioni
-------------

Controllo Registrazione
~~~~~~~~~~~~~~~~~~~~~~~

Codice per controllare una registrazione appena fatta dall'interno.

Salva Registrazione
~~~~~~~~~~~~~~~~~~~

Codice per effettuare una registrazione dall'apparecchio telefonico da cui si sta chiamando, vedi anche :ref:`qui <registrazioni_di_sistema_ref_label>`.

Condizioni Temporali
--------------------

Codice per interagire con le :ref:`Condizioni Temporali <condizioni_temporali_ref_label>` configurate.

Casella Vocale
--------------

Casella Vocale
~~~~~~~~~~~~~~

Codice per interagire con una :ref:`Casella Vocale <casella_vocale_ref_label>` di un qualunque interno. E' possibile accodare l'interno per evitare la richiesta.

Casella Vocale Personale
~~~~~~~~~~~~~~~~~~~~~~~~

Codice per interagire con la :ref:`Casella Vocale <casella_vocale_ref_label>` dell'interno dal quale si effettua la chiamata.

.. _impostazioni_generali_ref_label:

Impostazioni Generali
=====================

Descrizione
-----------

Nel Modulo Impostazioni Generali vengono raccolti dei parametri globali per configurare il |product|.

Procedere con molta cautela modificando solo valori di cui si è a conoscenza del significato.

Configurazione
--------------

Opzioni di Chiamata
-------------------

Opzioni Asterisk per le chiamate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opzioni per le chiamate entranti:

*  **t**: permette al chiamato di trasferire le chiamate digitando il :ref:`Codice Servizio <trasferimento_diretto_ref_label>` di |product|.
*  **T**: permette al chiamante di trasferire le chiamate digitando il :ref:`Codice Servizio <trasferimento_diretto_ref_label>` di |product|.
*  **r**: genera un o squillo al chiamante.
*  **x o w**: consente al chiamato di far partire la registrazione usando il :ref:`Codice di Registrazione Chiamata <codice_registrazione_ref_label>` ( x per Automixmon w per Automon come configurato in :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>` ).
*  **X o X**: consente al chiamante di far partire la registrazione usando il :ref:`Codice di Registrazione Chiamata <codice_registrazione_ref_label>` ( X per Automixmon W per Automon come configurato in :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>`).

Opzioni Asterisk per le chiamate in uscita
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opzioni per le chiamate uscenti:

-  **t**: permette al chiamato di trasferire le chiamate digitando il :ref:`Codice Servizio <trasferimento_diretto_ref_label>` di |product|.
-  **T**: permette al chiamante di trasferire le chiamate digitando il :ref:`Codice Servizio <trasferimento_diretto_ref_label>` di |product|.
-  **r**: genera un o squillo al chiamante, non è consigliabile per le chiamate in uscita.
-  **x o w**: consente al chiamato di far partire la registrazione usando il :ref:`Codice di Registrazione Chiamata <codice_registrazione_ref_label>` ( x per Automixmon w per Automon come configurato in :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>` ).
-  **X o X**: consente al chiamante di far partire la registrazione usando il :ref:`Codice di Registrazione Chiamata <codice_registrazione_ref_label>` ( X per Automixmon W per Automon come configurato in :ref:`Impostazioni Avanzate <impostazioni_avanzate_ref_label>` ).

Registrazione Chiamate
----------------------

Impostazione Globale Registrazione chiamate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abilitazione generale per la registrazione delle chiamate configurabili dagli interni, vedi :ref:`qui <interni_sip_ref_label>`.

Se disabilitato ogni opzione *Registra Subito* configurata sugli Interni sarà ignorata non registrando nessuna chiamata.

Questa opzione non ha effetti sulla registrazione su richiesta, configurabile in :ref:`Opzioni Chiamata <impostazioni_generali_ref_label>`, ne sulle registrazioni di :ref:`Code <code_ref_label>` e :ref:`Conferenze <conferenze_ref_label>`.

Disabilitare questa opzione se non si utilizzano le registrazioni, velocizzando il processo delle chiamate da parte del |product|.

Formato registrazione chiamate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Selezionare il formato delle registrazioni delle chiamate.

Casella Vocale
--------------

Tempo predefinito di squillo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il numero di secondi di squillo di un interno prima di inviare i chiamanti alla :ref:`Casella Vocale <casella_vocale_ref_label>`. Questa opzione può essere impostata singolarmente per ogni interno :ref:`qui <interni_sip_ref_label>` e non ha effetti per interni senza :ref:`Casella Vocale <casella_vocale_ref_label>`.

Prefisso chiamata diretta Casella Vocale
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il prefisso per contattare direttamente la :ref:`Casella Vocale <casella_vocale_ref_label>` di un interno, modificare con cautela per non creare dei conflitti con codici già esistenti.

Tipo messaggio per la chiamata diretta alla Casella Vocale
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il messaggio predefinito da utilizzare quando si chiama direttamente la :ref:`Casella Vocale <casella_vocale_ref_label>` di un interno.

Guadagno opzionale messaggi vocali
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Guadagno utilizzato durante la registrazione dei messaggi vocali.
L'unità di misura è in decibel.

Non riprodurre "prego lasciare un messaggio dopo il segnale acustico" al chiamante
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Selezionare l'opzione per non riprodurre il messaggio predefinito "Prego lasciare un messaggio dopo il segnale acustico. Quando terminato riagganciare o premere cancelletto." dopo il messaggio di benvenuto della :ref:`Casella Vocale <casella_vocale_ref_label>`. Questa opzione è globale.

Interno Operatore
~~~~~~~~~~~~~~~~~

Numero di default che il |product| deve comporre quando il chiamante preme '0' dalla :ref:`Casella Vocale <casella_vocale_ref_label>` o dalla directory dell':ref:`IVR <ivr_ref_label>`. Non deve essere un interno per forza, può essere ad esempio un :ref:`Gruppo di Chiamata <gruppi_di_chiamata_ref_label>` o un numero esterno.

VmX Locator Casella Vocale
--------------------------

Messaggio dopo il Timeout
~~~~~~~~~~~~~~~~~~~~~~~~~

Se questa destinazione è la Casella Vocale scegliere se riprodurre le istruzioni standard o un semplice segnale acustico.

Messaggio a Fine Ripetizioni
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se questa destinazione è la Casella Vocale scegliere se riprodurre le istruzioni standard o un semplice segnale acustico.

Opzione Chiamata Diretta
~~~~~~~~~~~~~~~~~~~~~~~~

Se sull':ref:`Interno <interni_sip_ref_label>` è stata definita l'opzione per chiamare direttamente la Casella Vocale, questa sarà l'opzione predefinita se non diversamente specificato sull'Interno.

Timeout Messaggio
~~~~~~~~~~~~~~~~~

Il tempo in secondi dopo la riproduzione del messaggio per andare in timeout e/o ripetere il messaggio se non è stata fatta nessuna scelta.

Riproduci il Messaggio
~~~~~~~~~~~~~~~~~~~~~~

Numero di volte che il messaggio viene riprodotto se il chiamante non fa nessuna scelta prima di andare all'opzione di timeout.

Numero di Ripetizioni in caso di Errore
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Numero di volte che il messaggio viene riprodotto se il chiamante non fa una scelta errata prima di andare all'opzione di opzione non valida.

Impostazioni Internazionali
---------------------------

Indicazioni Paese
~~~~~~~~~~~~~~~~~

Selezionare lo stato.

Formato orario 24 ore
~~~~~~~~~~~~~~~~~~~~~

Selezionare Si per il formato 24 0re, No per utilizzare quello a 12 ore (am/pm).

Impostazioni di Sicurezza
-------------------------

Permetti chiamate anonime SIP in ingresso
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Impostando Si, tutti avranno la possibilità di chiamare il |product| tramite il protocollo SIP ricevendo così anche chiamate anonime.

.. _amministrazione_moduli_ref_label:

Amministrazione Moduli
======================

Descrizione
-----------

Tramite l'Amministrazione moduli vengono gestiti tutti i componenti del |product|.

Nella pagina sono elencati, divisi per tipologia, tutti i moduli installati e/o installabili su |product|.

C'è la possibilità cliccando sul nome del modulo di gestire le azioni che lo riguardano, a seconda del suo stato sarà possibile installarlo, aggiornarlo, disinstallarlo, attivarlo o disattivarlo.

I moduli vengono aggiornati tramite aggiornamenti automatici e/o manuali, il tipo di aggiornamento dipende dal modulo e ovviamente dai cambiamenti da apportare.

.. _messaggio_rotta_congestionata_ref_label:

Messaggio Rotta Congestionata
=============================

Descrizione
-----------

In questo modulo è possibile personalizzare i messaggi di errore o di impossibilità delle chiamate effettuate.

I messaggi vengono presi dalle :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` già caricate.

Configurazione
--------------

Rotte Standard
~~~~~~~~~~~~~~

Messaggio o tono da riprodurre in caso di indisponibilità di Fasci per chiamare.

Rotte Intra-Aziendali
~~~~~~~~~~~~~~~~~~~~~

Messaggio o tono da riprodurre in caso di indisponibilità di Fasci per le rotte Intra-Aziendali.

Rotte di Emergenza
~~~~~~~~~~~~~~~~~~

Messaggio o tono da riprodurre in caso di indisponibilità di Fasci per le rotte di emergenza.

Nessuna Risposta
~~~~~~~~~~~~~~~~

Messaggio o tono da riprodurre in caso di nessuna risposta per la chiamata. Il messaggio di default è: "Il numero chiamato non ha risposto."

Numero Incompleto
~~~~~~~~~~~~~~~~~

Messaggio o tono da riprodurre se il Fascio riporta Numero Errato o Incompleto. Il messaggio di default è: "Il numero chiamato non è attivo, verificare il numero è riprovare."

.. _amministrazione_caselle_vocali_ref_label:

Amministrazione Caselle Vocali
==============================

Descrizione
-----------

Il modulo Amministrazione Caselle Vocali consente di gestire tutte le :ref:`Caselle Vocali <casella_vocale_ref_label>` configurate su |product|.

Il modulo si divide in varie parti, sia generali che per le singole caselle.

Sulla destra, innanzitutto, c'è l'elenco degli :ref:`interni <interni_ref_label>` configurati sul |product|, con sfondo verde quelli con la :ref:`Casella Vocale <casella_vocale_ref_label>` configurata, in giallo quelli con la :ref:`Casella Vocale <casella_vocale_ref_label>` non attiva.

E' possibile cliccando sui vari :ref:`interni <interni_ref_label>` con :ref:`Casella Vocale <casella_vocale_ref_label>` attiva entrare nella configurazione specifica, altrimenti negli :ref:`interni <interni_ref_label>` non attivi si viene dirottati al modulo per attivarla.

Il modulo ha poi tre sezioni *Impostazioni*, *Utilizzo* e *Definizione Timezone* per la configurazione generale.

La parte di *Definizione Timezone* non è al momento supportata.

Configurazione
--------------

Impostazioni
~~~~~~~~~~~~

Nelle immagini i valori di default.

*  **adsifdn**: numero descrittore della applicazione ADSI per scaricare a.
*  **adsisec**: codice di sicurezza applicazione ADSI.
*  **adsiver**: numero versione applicazione ADSI.
*  **attach**: attivazione/disattivazione opzione per allegare il messaggio audio alla email.
*  **authpassword**: password per l'utente amministrativo IMAP server, se usato.
*  **authuser**: l'utente amministratore per la connessione al server IMAP.
*  **backupdeleted**: numero massimo di messaggi ammessi nella cartella *Deleted*. Se configurato a 0 o a no nessun messaggio cancellato sarà spostato, se impostato ad un numero da 1 a 9999 al massimo, questo numero di messaggi sarà allocato nella cartella *Deleted*. Il default è off.
*  **callback**: contesto dal quale farsi richiamare, se non inserito la richiamata sarà disabilitata.
*  **charset**: il carattere per il messaggio della Casella Vocale.
*  **cidinternalcontexts**: il contesto interno per il playback del nome invece del numero quando viene comunicato il chiamate.
*  **dialout**: contesto per le chiamate in uscita da (opzione 4 del menù avanzato), se non inserito le chiamate in uscita non saranno permesse.
*  **emailbody**: corpo della email di notifica della Casella Vocale.
*  **emaildateformat**: formato data per l'email della Casella Vocale.
*  **emailsubject**: oggetto della email di notifica Casella Vocale.
*  **envelope**: attivazione/disattivazione della riproduzione della busta prima del messaggio.
*  **exitcontext**: contesto di uscita per gli utenti che digitano 0 o \* ad esempio.
*  **expungeonhangup**: elimina in uscita.
*  **externnotify**: applicazione esterna per la notifica della Casella Vocale
*  **externpass**: comando per cambiare la password per l'applicazione esterna, sovrascrive externnotify.
*  **externpassnotify**: comando da eseguire dopo il cambio di password dall'applicazione esterna.
*  **forcegreetings**: forza un utente di un Casella Vocale appena configurata a registrare il messaggio di benvenuto.
*  **forcename**: forza un utente di un Casella Vocale appena configurata a registrare il proprio nome.
*  **format**: formato del file audio della Casella Vocale. Inserire solo formati supportati da **Asterisk**.
*  **fromstring**: nome mittente della email.
*  **greetingsfolder**: cartella dove conservare i benvenuti se imapgreetings=yes, se non specificato è INBOX.
*  **imapclosetimeout**: timeout per server IMAP.
*  **imapflags**: protocollo opzionale per il server IMAP, per esempio ssl per i server che supportano OpenSSL.
*  **imapfolder**: la cartella dove conservare i messaggi email della Casella Vocale.
*  **imapgreetings**: attivazione archiviazione messaggi di benvenuto.
*  **imapopentimeout**: timeout per server IMAP.
*  **imapparentfolder**: cartella radice per il server IMAP.
*  **imapport**: porta per il server IMAP.
*  **imapreadtimeout**: timeout per server IMAP.
*  **imapserver**: indirizzo del server IMAP.
*  **imapwritetimeout**: timeout per server IMAP.
*  **listen-control-forward-key**: tasto personalizzato per scorre in avanti i messaggi.
*  **listen-control-pause-key**: tasto personalizzato per la pausa dei messaggi.
*  **listen-control-restart-key**: tasto personalizzato per il riavvio dei messaggi.
*  **listen-control-reverse-key**: tasto personalizzato per scorre indietro i messaggi.
*  **listen-control-stop-key**: tasto personalizzato per fermare i messaggi.
*  **mailcmd**: comando per inviare email.
*  **maxgreet**: massima durata del benvenuto.
*  **maxlogins**: numero massimo di tentativi di accesso.
*  **maxmessage**: lunghezza massima messaggio, dimensione.
*  **maxmsg**: numero massimo messaggi della Casella Vocale.
*  **maxsecs**: numero massimo di secondi di durata di un messaggio.
*  **maxsilence**: numero di secondi di silenzio dopo il quale il |product| chiuderà la registrazione della Casella Vocale.
*  **minsecs**: numero di secondi minimo per considerare un messaggio valido. Deve essere superiore a maxsilence altrimenti ci possono essere dei messaggi vuoti.
*  **moveheard**: sposta i messaggi ascoltati nella cartella *Old*.
*  **nextaftercmd**: salta al prossimo messaggio dopo aver premuto 7 o 9 per cancellare/salvare il messaggio corrente.
*  **odbcstorage**: la connessione odbc configurata nel file /etc/asterisk/res\_odbc.conf per il salvataggio delle Caselle Vocali.
*  **odbctable**: tabella odbc dove registrare i messaggi delle Caselle Vocali.
*  **operator**: se attivato abilita premendo 0 prima/durante/dopo un messaggio di contattare un operatore.
*  **pagerbody**: corpo del messaggio inviato al sistema di inoltro se abilitato.
*  **pagerfromstring**: mittente del messaggio inviato al sistema di inoltro se abilitato.
*  **pagersubject**: oggetto del messaggio inviato al sistema di inoltro se abilitato.
*  **pbxskip**: salta la stringa [PBX] dal titolo del messaggio.
*  **pollfreq**: frequenza di polling se pollmailboxes è attivato.
*  **pollmailboxes**: se le caselle postali vengono cambiate al di fuori del modulo Caselle Vocali questa opzione deve essere attivata.
*  **review**: abilita il mittente a risentire/registrare di nuovo il messaggio appena lasciato.
*  **saycid**: comunica le informazioni del chiamante prima del messaggio.
*  **sayduration**: comunica le informazioni sulla durata prima del messaggio.
*  **saydurationm**: specificare la durata minima da comunicare.
*  **searchcontexts**: cerca la Casella Vocale in tutti i contesti oltre al corrente.
*  **sendvoicemail**: abilita l'invio alla Casella Vocale.
*  **serveremail**: indirizzo mittente della mail di notifica della Casella Vocale.
*  **silencethreshold**: che valore di rumore considerare silenzio.
*  **skipms**: quanti millesecondi per spostarsi avanti/indietro quando si effettua lo scorrimento avanti/indietro nel messaggio.
*  **smdienable**: abilita interfaccia SMDI.
*  **smdiport**: porta valida come specificato in /etc/asterisk/smdi.conf per l'utilizzo di SMDI.
*  **tempgreetwarn**: ricorda all'utente che ha attivato un messaggio di benvenuto temporaneo.
*  **usedirectory**: permesso di trovare le voci per avanti/indietro nella directory.
*  **userscontext**: contesto utente quando le voci di /etc/asterisk/users.conf sono registrate.
*  **vm-mismatch**: personalizzare il file audio al posto di quello di default che dice "La password inserita e re-inserita non coincidono.  Riprova."
*  **vm-newpassword**: personalizzare il file audio che viene utilizzato al posto del prompt di default che dice: "Inserisci la tua nuova password seguita dal tasto cancelletto."
*  **vm-passchanged**: Personalizzare il file audio che viene utilizzato al posto del prompt di default che dice: "La tua password è stata cambiata."
*  **vm-password**: Personalizzare il file audio che viene utilizzato al posto del prompt di default che dice: "password".
*  **vm-reenterpassword**: Personalizzare il file audio che viene utilizzato al posto del prompt di default che dice: "Si prega di inserire nuovamente la password seguita dal tasto cancelletto".
*  **volgain**: l'allegato alla mail della Casella Vocale può arrivare in un volume troppo basso per essere ascoltato. Questo parametro consente di specificare la quantità di guadagno da aggiungere al messaggio durante l'invio di un messaggio vocale. NOTA: sox deve essere installato per far funzionare questa opzione.

Utilizzo
~~~~~~~~

La sezione Utilizzo offre una visione di insieme dello stato delle Caselle Vocali su |product|, fornendo il totale delle Caselle Vocali configurate, dei messaggi presenti, dello spazio disco occupato etc.

*  **Numero di Account**: numero di account attivati/non attivati/disabilitati.
*  **Numero messaggi**: numero messaggi cartella INBOX/altre cartelle.
*  **Nomi Registrati**: numero di messaggi nome registrati.
*  **Messaggi di benvenuto su non disponibile**: numero di messaggi di benvenuto su non disponibile registrati.
*  **Messaggi di benvenuto su occupato**: numero di messaggi di benvenuto su occupato registrati.
*  **Messaggi di benvenuto temporanei**: numero di messaggi di benvenuto temporanei registrati.
*  **Messaggi di benvenuto abbandonati**: numero di messaggi di benvenuto abbandonati registrati.
*  **Disco Usato**: spazio di disco usato al momento dai dati dalle Caselle Vocali in megabytes.

Amministrazione Singole Caselle Vocali
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cliccando su uno degli interni nella parte destra si entra nell'amministrazione della singola Casella Vocale.

Impostazioni
^^^^^^^^^^^^

Nelle Impostazioni si ottiene l'accesso alla parte della configurazione dell'interno che riguarda la Casella Vocale, per maggiori dettagli vedi :ref:`qui <casella_vocale_ref_label>`.

Utilizzo
^^^^^^^^

Nella sezione Utilizzo viene mostrato lo stato della Casella Vocale.

*  **Numero messaggi**: numero messaggi cartella INBOX/altre cartelle.
*  **Nome Registrato**: presenza o meno della registrazione del messaggio nome.
*  **Messaggio di benvenuto su non disponibile**: presenza o meno della registrazione messaggio di benvenuto su non disponibile.
*  **Messaggio di benvenuto su occupato**: presenza o meno della registrazione messaggio di benvenuto su occupato.
*  **Messaggio di benvenuto temporanei**: presenza o meno della registrazione messaggio di benvenuto temporanei.
*  **Messaggio di benvenuto abbandonati**: presenza o meno della registrazione messaggio di benvenuto abbandonati.
*  **Disco Usato**: spazio di disco usato al momento dai dati dalla Casella Vocale in megabytes.

Impostazioni Avanzate
^^^^^^^^^^^^^^^^^^^^^

Nella sezione Impostazioni Avanzate è possibile personalizzare le opzioni della Casella Vocale rispetto allo standard generale.
