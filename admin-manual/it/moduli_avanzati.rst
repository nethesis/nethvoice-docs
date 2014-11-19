===============
Moduli Avanzati
===============

.. _impostazioni_avanzate_ref_label:

Impostazioni Avanzate
=====================

Il Modulo Impostazioni Avanzate consente di andare nel dettaglio dei servizi di |product| configurando nei minimi particolari ogni funzionalità.

**Alcune di queste impostazioni possono rendere il sistema inutilizzabile**.

Fare un backup prima di apportare modifiche.

Le impostazioni read-only sono in genere più variabili. Possono essere modificate impostando "true" l'opzione "Override delle impostazioni in sola lettura". Dopo averle modificate,, si devono salvare le impostazioni abilitando il check nella check box verde che apparirà. Si possono reimpostare le impostazioni di default cliccando nell'icona a destra del valore.

.. warning:: Fare delle modifiche solo se si è certi di quello che si sta facendo e si è a conoscenza delle possibili problematiche create

.. _cli_ref_label:

CLI Asterisk
============

Permette di eseguire comandi tramite la console CLI (Command Line Interface) di Asterisk, visualizzando via web la risposta.

I comandi che possono essere eseguiti sono tutti quelli della console, ovviamente non è possibile usarlo per vedere in tempo reale scorrere le chiamate, come si può fare collegandosi in ssh a nethservice e digitando il comando ::

  asterisk -r

Esempi di Comandi
-----------------

*  **sip show peers**: Elenca tutti gli interni SIP con il relativo stato di registrazione sul server, e l'ip da cui si collegano
*  **iax2 show peers** Come il precedente ma per gli interni IAX
*  **sip show peer EXTEN** Visualizza i dettagli di configurazione dell'interno EXTEN
*  **iax2 show peer EXTEN** Come il precedente ma per gli interni IAX
*  **core show channels verbose** visualizza l'elenco dei canali attivi in questo momento
*  **sip show registry** visualizza lo stato della registrazione dei fasci sip che la prevedono(ad esempio fasci voip)
*  **hangup request CANALE** chiude un canale aperto (premere due volte tab per visualizzare i canali aperti)

.. _blacklist_ref_label:

Blacklist
=========

Descrizione
-----------

Il modulo Blacklist di |product| consente di bloccare in ingresso le chiamate che provengono da determinati numeri telefonici.

La chiamata da un chiamante bloccato invece di entrare nel normale flusso di chiamata verrà rifiutata con un messaggio che dice che il numero chiamato non è più valido.

Il modulo offre anche la possibilità di bloccare le chiamate anonime.

Non è ammesso l'utilizzo dei :ref:`pattern di Asterisk <pattern_ref_label>`, se è necessario utilizzarli si possono bloccare le chiamate tramite le :ref:`Rotte in entrata <rotte_in_entrata_ref_label>` destinandole ad un :ref:`Annuncio <annunci_ref_label>` o chiudendo subito la chiamata ad esempio.

Configurazione
--------------

Numero/ID Chiamante
~~~~~~~~~~~~~~~~~~~

Inserire il numero o il nome in caso sia risolto dalla rubrica del |product| che si vuole inserire in Blacklist.

Descrizione
~~~~~~~~~~~

Inserire una descrizione per il numero da inserire in Blacklist.

Blocca ID Chiamanti Anonimi
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Spuntando l'opzione vengono bloccate tutte le chiamate anonime.

Codici Attivazione
~~~~~~~~~~~~~~~~~~

I seguenti Codici, modificabili tramite il modulo :ref:`Codici Servizi <codici_servizi_ref_label>` consentono l'utilizzo del modulo Blacklist direttamente da un interno.

Servono ad aggiungere, rimuovere un numero dalla Blacklist, vanno ovviamente seguiti dal numero in questione.

Con un codice, invece, è possibile aggiungere alla Blacklist il numero dell'ultimo chiamante.

.. _blocco_interni_ref_label:

Blocco Interni
==============

Descrizione
-----------

Il modulo Blocco Interni permette di impedire a degli interni del |product| dei modelli di chiamate in uscita, modello che viene stabilito secondo dei :ref:`Pattern <pattern_ref_label>` inseriti nel Modello di Chiamata, uno per linea.

Il Blocco viene attivato digitando un codice sull'interno da bloccare e con un altro codice può essere revocato, attivazione e disattivazione del blocco possono essere regolate tramite la richiesta di una password.

Prestare molta attenzione nell'inserimento dei modelli di chiamata da bloccare, in quanto con dei modelli invasivi si può ottenere un comportamento molto drastico non voluto.

Configurazione
--------------

Modelli di Chiamata
~~~~~~~~~~~~~~~~~~~

Inserire qui i modelli di chiamata, uno per linea, usando i :ref:`Pattern <pattern_ref_label>` di **Asterisk**.

Codici da telefono
~~~~~~~~~~~~~~~~~~

I seguenti Codici, modificabili tramite il modulo :ref:`Codici Servizi <codici_servizi_ref_label>` consentono l'utilizzo del modulo Blocco Interni direttamente da un interno.

Servono a bloccare, sbloccare e cambiare la password di controllo delle funzionalità.

.. _modulo_registrazione_chiamate_ref_label:

Modulo Registrazione Chiamate
=============================

Descrizione
-----------

Il modulo Registrazione Chiamate permette di forzare o meno la registrazione all'interno dell flusso della chiamata ignorando le configurazioni in essere.

Se una chiamata è da registrare, è possibile registrarla immediatamente incorporando eventuali annunci, musica di attesa, ecc prima di ricevere risposta, oppure la registrazione può iniziare al momento in cui chiamata è risposta.

Configurazione
--------------

Descrizione
~~~~~~~~~~~

Il nome di questa istanza di registrazione chiamate.

Modalità Registrazione Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Comportamento del |product| riguardo alla registrazione:

*  **Permetti**: manterrà le impostazioni di registrazione normali del flusso di chiamata.
*  **Registra alla Risposta**: inizia la registrazione quando la chiamata dovrebbe essere registrata ignorando tutte le impostazioni che dicono il contrario.
*  **Registra Subito**: avvia la registrazione subito catturando annunci, musica di attesa ecc.
*  **Mai**: non consentirà la registrazione a prescindere dalle impostazioni nel flusso di chiamata.

Destinazione
~~~~~~~~~~~~

Destinazione della chiamata successiva al passaggio sul modulo.

.. _destinazioni_personalizzate_ref_label:

Destinazioni Personalizzate
===========================

Descrizione
-----------

Il modulo Destinazioni Personalizzate permette di registrare e aggiungere destinazioni che puntano ad un piano di chiamata personalizzato e pubblica queste destinazioni come disponibili in altri moduli.

Questa è una funzione avanzata ed andrebbe usata solo da utenti che conosco bene i comandi.

Configurazione
--------------

Destinazione Personalizzata
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Questa è la Destinazione Personalizzata che sarà pubblicata.

Deve essere formattata come se fosse inserita nel codice di Asterisk, dopo il comando goto, con contesto, estensione, priorità.

Ad esempio app-prova,s,1

Selezione Rapida Destinazione
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Selezione rapida tra le destinazioni già caricate.

Descrizione
~~~~~~~~~~~

Breve descrizione per individuare da altri Moduli questa Destinazione Personalizzata.

Note
~~~~

Ulteriori note descrittive per documentare il funzionamento della Destinazione.

.. _interni_personalizzati_ref_label:

Interni Personalizzati
======================

Descrizione
-----------

Il modulo Interni Personalizzati permette facilmente di registrare un interno (extension) personalizzato o codice di servizio precedentemente creato in un file custom.

Questo permette a |product| di conoscerne l'esistenza.

Il Registro Interni mette da parte questa numerazione in modo da rilevare eventuali conflitti e riportarli in caso di errori negli altri moduli. Qui non si dovrebbero inserire interni che sono stati creati con il modulo :ref:`Applicazioni Varie <applicazioni_varie_ref_label>` perché questi non sono interni (extension) personalizzati.

Configurazione
--------------

Interno Personalizzato
~~~~~~~~~~~~~~~~~~~~~~

Inserire qui l'Interno o il Codice di Servizio che sta utilizzando nel piano di chiamata e che si vuole inserire nel Registro Interni di |product|.

Descrizione
~~~~~~~~~~~

Breve descrizione per questo Interno Personalizzato che sarà pubblicata nel Registro Interni di |product|.

Note
~~~~

Ulteriori note descrittive per documentare il funzionamento della Destinazione.

.. _direttore_segretaria_ref_label:

Direttore Segretaria
====================

Descrizione
-----------

Il modulo Direttore Segretaria serve a dare dei ruoli agli interni del |product| per variare le politiche di squillo degli interni.

Creando un gruppo, a cui bisogna dare un nome, si ha la possibilità di istituire tre ruoli, Direttore, Segretaria e Amministratore.

Quando verrà chiamato l'interno di un Direttore, il suo interno non suonerà ma la chiamata verrà girata agli interni classificati come Segretarie.

Solo gli interni Amministratori riusciranno a contattare direttamente gli interni Direttori senza passare per gli interni Segretarie.

Configurazione
--------------

Ricerca Gruppo
~~~~~~~~~~~~~~

Ricerca di un interno per controllare se ed eventualmente in che gruppo è stato utilizzato.

Nome Gruppo
~~~~~~~~~~~

Nome del gruppo puramente descrittivo per favorirne il riconoscimento.

Direttori
~~~~~~~~~

Inserire gli gli interni da categorizzare come Direttori, uno per riga.

Segretarie
~~~~~~~~~~

Inserire gli gli interni da categorizzare come Segretarie, uno per riga.

Amministratori
~~~~~~~~~~~~~~

Inserire gli gli interni da categorizzare come Amministratori, uno per riga.

Pulisci e Rimuovi Duplicati
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Non ci possono essere interni duplicati sia nello stesso ruolo che in ruoli diversi, cliccando in questo tasto si eliminano eventuali sviste.

Codici da Telefono
~~~~~~~~~~~~~~~~~~

I seguenti Codici, modificabili tramite il modulo :ref:`Codici Servizi <codici_servizi_ref_label>` consentono l'attivazione del modulo Direttore Segretaria direttamente da un interno.

.. _cli_import_interni_ref_label:

Import Interni
==============

Descrizione
-----------

Il modulo Import Interni ha la funzione di importare la lista degli :ref:`Interni <interni_ref_label>` direttamente da un file csv.

Questo dovrebbe agevolare il compito in presenza di installazioni di |product| con un numero di :ref:`Interni <interni_ref_label>` elevato.

La giusta formattazione del file csv si ottiene scaricando il file Template CSV o cliccando nel pulsante ESPORTAZIONE INTERNI nel caso esistano già degli :ref:`Interni <interni_ref_label>` configurati nel |product|.

Il file deve contenere un :ref:`Interno <interni_ref_label>` per riga con tutti i campi separati da virgola.

L'elenco dei campi si trova direttamente nel modulo.

.. _import_rotte_in_entrata_ref_label:

Import Rotte in Entrata
=======================

Descrizione
-----------

Il modulo Import Rotte in entrata ha la funzione di importare le :ref:`Rotte in Entrata <rotte_in_entrata_ref_label>` direttamente da un file csv.

Questo dovrebbe agevolare il compito in presenza di installazioni di |product| con configurazioni per le chiamate in entrata numerose.

La giusta formattazione del file csv si ottiene scaricando il file Template CSV o cliccando nel pulsante ESPORTA nel caso esistano già delle :ref:`Rotte in Entrata <rotte_in_entrata_ref_label>` configurate nel |product|.

Il file deve contenere una :ref:`Rotte in Entrata <rotte_in_entrata_ref_label>` per riga con tutti i campi separati da virgola.

L'elenco dei campi si trova direttamente nel modulo.

.. _lingue_ref_label:

Lingue
======

Descrizione
-----------

Il modulo Lingue permette di cambiare la lingua durante il flusso di una chiamata semplicemente direzionando la chiamata al modulo per poi farla continuare verso la destinazione desiderata.

Il cambiamento di lingua si traduce in pratica nel fatto che il |product| da quel momento utilizzerà i messaggi di sistema nella lingua prescelta.

Di default su |product| sono caricati solo i messaggi in italiano ed in inglese.

Per aggiungere i files audio di una lingua, scaricare i suoni per Asterisk e caricarli :ref:`qui <struttura_filesystem_ref_label>`.

Configurazione
--------------

Descrizione
~~~~~~~~~~~

Descrizione per il modulo.

Codice Lingua
~~~~~~~~~~~~~

Codice lingua di Asterisk, per esempio it per italiano, fr per francese, de per tedesco...

.. _applicazioni_varie_ref_label:

Applicazioni Varie
==================

Descrizione
-----------

Le Applicazioni Varie possono essere utilizzate per impostare dei servizi consultabili direttamente dai telefoni scegliendo una delle varie destinazioni disponibili in |product|.

Non è la stessa cosa del modulo :ref:`Destinazioni Varie <destinazioni_varie_ref_label>`, che serve a creare destinazioni da poter essere utilizzate da altri moduli di |product|, per chiamare per esempio numeri interni o altri servizi.

Configurazione
--------------

Descrizione
~~~~~~~~~~~

Nome descrittivo per individuare l'Applicazione creata.

Codice Servizio
~~~~~~~~~~~~~~~

Il codice/interno che gli utenti dovranno digitare per accedere a questa Applicazione. Una volta creata l'Applicazione può essere modificato dalla pagina :ref:`Codici Servizi <codici_servizi_ref_label>`.

Stato Servizio
~~~~~~~~~~~~~~

Stato dell'Applicazione, se attiva o no.

Destinazione
~~~~~~~~~~~~

Destinazione della chiamata dopo aver digitato il Codice Servizio.

.. _gruppi_pin_ref_label:

Gruppi Pin
==========

Descrizione
-----------

Il modulo Gruppi PIN di |product| ha la funzione di raggruppare dei codici pin ed utilizzarli nei moduli che possono richiedere una autorizzazione tramite PIN come ad esempio le :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

La richiesta di un PIN può anche essere automatizzata inserendo il valore del campo accountcode configurato nell':ref:`interno <interni_sip_ref_label>` nella lista dei PIN.

Configurazione
--------------

Descrizione Gruppo PIN
~~~~~~~~~~~~~~~~~~~~~~

Descrizione per individuare il Gruppo PIN.

Registra nel CDR
~~~~~~~~~~~~~~~~

Spuntare questa opzione per registrare nei :ref:`Report <report_cdr_ref_label>` del |product| l'immissione del PIN.

Lista PIN
~~~~~~~~~

Inserire uno o più PIN, uno per riga. Ovviamente si tratta di valori numerici.

.. _priorita_code_ref_label:

Priorita Code
=============

Descrizione
-----------

Il modulo Priorità Coda permette di impostare al chiamante una priorità nella coda.

Normalmente un chiamante ha priorità 0. Impostando una priorità alta il chiamante verrà risposto prima degli altri presenti già in :ref:`Coda <code_ref_label>`.

La priorità è applicata a tutte le `Code <Code_|product|>`__ dove il chiamante eventualmente è diretto. Di solito come destinazione viene imposta una :ref:`Coda <code_ref_label>`, ma questo non è obbligatorio.

Per esempio si potrebbe impostare come destinazione un unico :ref:`IVR <ivr_ref_label>` ma proveniente da due diverse :ref:`Rotte in Entrata <rotte_in_entrata_ref_label>`, e di conseguenza le chiamate che andranno dall':ref:`IVR <ivr_ref_label>` nelle successive :ref:`Code <code_ref_label>` seguiranno la priorità qui impostata.

Configurazione
--------------

Descrizione
~~~~~~~~~~~

Nome descrittivo per questa Priorità Code.

Priorità
~~~~~~~~

Priorità per la chiamata che transita attraverso questa Priorità Coda.
La priorità 0 è quella di default ed anche quella più bassa all'interno di una :ref:`Coda <code_ref_label>`.

Destinazione
~~~~~~~~~~~~

Destinazione della chiamata dopo che le è stata modificata la Priorità Coda.

.. _richiamata_ref_label:

Richiamata
==========

Descrizione
-----------

Il modulo Richiamata consente di essere richiamati in modo automatico.

Se una chiamata arriva al modulo Richiamata, il |product| riaggancerà subito la chiamata e richiamerà il chiamante subito dopo indirizzando la chiamata al modulo selezionato.

Questo modulo ha di solito lo scopo di ridurre i costi per chiamate particolari, tipo internazionali o cellulari.

Le chiamate effettuate dal modulo Richiamata verranno processate normalmente secondo le politiche decise nelle :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

Configurazione
--------------

Descrizione Richiamata
~~~~~~~~~~~~~~~~~~~~~~

Inserire una descrizione per questa Richiamata.

Numero Richiamata
~~~~~~~~~~~~~~~~~

Inserire in numero da richiamare. Se lasciato vuoto verrà richiamato l'ID Chiamante.

Ritardo prima della Richiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire il numero di secondi prima di effettuare la Richiamata.

Destinazione dopo la Richiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della Richiamata.

.. _imposta_callerid_ref_label:

Imposta Callerid
================

Descrizione
-----------

Imposta CallerID consente di cambiare l'ID chiamante della chiamata e poi proseguire per la destinazione desiderata, ad esempio, si può decidere di modificare l'id chiamante "Mario Rossi" a "Vendite: Mario Rossi".

Si prega di notare, il testo da inserire è quello modificato.

Per modificare il callerid corrente, utilizzare le variabili Asterisk adeguate, come ad esempio "$ {CALLERID (nome)} " per il nome callerid attualmente impostato e "$ {CALLERID (num)} "per il numero callerid attualmente impostato.

Configurazione
--------------

Descrizione
~~~~~~~~~~~

Campo descrittivo per individuare L'imposta CallerID configurato.

Nome CallerID
~~~~~~~~~~~~~

Il Nome CallerID che si desidera utilizzare.

Se si sta cercando di modificare il nome e non sostituendolo completamente, non dimenticare di includere le variabili Asterisk appropriate.

Se si lascia vuota questa casella, il nome verrà oscurato.

Numero CallerID
~~~~~~~~~~~~~~~

I Numero CallerID che si desidera utilizzare.

Se si sta cercando di modificare il numero e non sostituendolo completamente, non dimenticare di includere le variabili Asterisk appropriate.

Se si lascia vuota questa casella, il numero verrà oscurato.

Destinazione
~~~~~~~~~~~~

Destinazione della chiamata dopo le operazioni su Nome e Numero CallerID.

.. _cli_gruppi_caselle_vocali_label:

Gruppi Caselle Vocali
=====================

Descrizione
-----------

Il Gruppo di Caselle Vocali ha la funzione di ricevere un messaggio vocale e moltiplicarlo per tutte le caselle vocali che ha come membri.

Viene quindi creato un nuovo messaggio per ogni membro e se il messaggio viene ascoltato e/o cancellato da uno dei membri non vale per gli altri.

Configurazione
--------------

Numero Gruppo
~~~~~~~~~~~~~

Il numero da chiamare per questo Gruppo di Caselle Vocali.

Descrizione Gruppo
~~~~~~~~~~~~~~~~~~

Descrizione per individuare il gruppo.

Etichetta Audio
~~~~~~~~~~~~~~~

Riproduce un messaggio audio scelto dalle :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` al chiamante per comunicare che gruppo ha chiamato, oppure c'è un messaggio di sistema che riproduce il numero del gruppo.

Password Opzionale
~~~~~~~~~~~~~~~~~~

Password opzionale per accedere al Gruppo di Caselle Vocali.

Lista Caselle Vocali
~~~~~~~~~~~~~~~~~~~~

Sezionare tra gli interni con la :ref:`casella vocale <interni_sip_ref_label>` attiva.

Gruppo Caselle Predefinito
~~~~~~~~~~~~~~~~~~~~~~~~~~

Se viene indicato come Gruppo di Caselle Vocali predefinito, gli interni con voicemail saranno automaticamente aggiunti e tolti da questo gruppo.

