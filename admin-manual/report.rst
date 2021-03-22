======
Report
======

Il nuovo report unificato di |product| consente di utilizzare un'unica interfaccia web per consultare:

- report code
- report chiamate e costi (CDR, Call Detail Record)

Il report è accessibile all'indirizzo ``https://<server_name>/pbx-report``.
Ogni utente può accedere con le stesse credenziali utilizzate all'interno del |product_cti|.
Le tabelle e i grafici visualizzati saranno filtrati in base al profilo |product_cti| associato all'utente.
Accedendo con l'utente ``admin`` di |product|, sarà possibile visualizzare sempre tutti i dati.

Il report consente l'accesso solo ai dati storicizzati a partire dal giorno precedente, indietro fino alla data di primo
utilizzo del centralino. Tutte le notti un processo elabora gli eventi della giornata e li rende disponibili per visualizzare
grafici e tabelle.
Quindi, al termine della prima installazione, è necessario attendere il giorno successivo per consultare il report.

È possibile installare il report direttamente dal :guilabel:`Software Center` selezionando il modulo chiamato ``Nethvoice report (beta)``.

Report code
===========

Il report code mostra molteplici informazioni associate alle code del centralino, come ad esempio dati sugli agenti e sulle loro sessioni di lavoro, sulle performance delle code, sulle aree geografiche di provenienza delle chiamate e sulle durate dei tempi di attesa.

Il modulo si divide in varie sezioni che ricalcano in parte quelle presenti nel :ref:`vecchio report code <queuereport-ref-label>`.
Ulteriori sezioni sono accessibili dal menu laterale.

Le varie sezioni sono dotate di documentazione inline per specificare le varie funzionalità.

Report chiamate & costi (CDR)
=============================

Il report CDR mostra informazioni aggregate e di dettaglio relative al registro chiamate.
Oltre alla sezione :guilabel:`Dashboard`, che presenta alcuni grafici riepilogativi, sono presenti le seguenti sezioni:

- :guilabel:`Dati centralino`: informazioni sulle chiamate in ingresso, in uscita e interne al centralino
- :guilabel:`Dati personali`: informazioni sulle chiamate interne, ricevute, o effettuate dall'utente loggato

I grafici delle sezioni :guilabel:`Dati centralino` e :guilabel:`Dati personali` presentano la stessa struttura, mostrando:

- un grafico riepilogativo espandibile che mostra dati sui totali e le durate delle chiamate
- un registro chiamate tabellare che mostra numero sorgente, numero di destinazione, esito chiamata, durata e costo. Cliccando il pulsante :guilabel:`Mostra dettagli` è possibile visualizzare ulteriori dettagli di ciascuna chiamata

Una parte dei dati di questo report è consultabile anche sul :ref:`vecchio report chiamate <inboundreport-ref-label>` e da |product_cti|.

La prima volta che si accede al report CDR, viene mostrata una finestra di dialogo che suggerisce di configurare i costi delle chiamate al fine di includerli nel report. Per ulteriori informazioni riguardo i costi delle chiamate si veda la sezione :ref:`Impostazioni <report-settings-ref-label>`.

Le varie sezioni sono dotate di documentazione inline per specificare le varie funzionalità.

Interfaccia utente
==================

L'interfaccia utente è comune a *report code* e *report CDR*, ed è organizzata in tre aree principali:

* menu laterale
* filtri
* grafici

Menu laterale
-------------

Il menu laterale consente la navigazione dei report e contiene:

* un selettore per passare dalla consultazione del report code a quella del report CDR e viceversa
* una casella di ricerca per trovare rapidamente una vista o un grafico di interesse
* la struttura completa del report corrente (code o CDR), organizzato in sezioni e viste. Ogni sezione può aggregare un insieme di viste oppure essere autocontenuta (ad es. la sezione *Dashboard*)

Filtri
------

L'area dei filtri consente di configurare l'intervallo temporale e i parametri per generare il report della vista corrente.
La generazione del report può essere avviata cliccando il pulsante :guilabel:`Cerca`.
Il pulsante :guilabel:`Salva ricerca` consente di salvare una specifica configurazione dei filtri, in modo che possa essere riutilizzata rapidamente.

Nell'angolo in alto a destra dell'area filtri sono presenti i seguenti pulsanti, attraverso i quali è possibile (da sinistra a destra):

* nascondere/mostrare il pannello dei filtri
* selezionare lo schema di colori utilizzato dai grafici
* accedere alle impostazioni dei report; questa funzionalità è disponibile soltanto se è stato effettuato l'accesso con l'utenza ``admin``. Per ulteriori informazioni si veda la sezione :ref:`Impostazioni <report-settings-ref-label>`
* eseguire il logout

Grafici
-------

L'area dei grafici costituisce quella di maggior interesse per l'utente e costituisce il corpo del report della vista corrente.
Ciascun grafico può essere esportato in almeno uno dei seguenti formati: CSV, PNG e PDF.
Per motivi di leggibilità, alcuni grafici mostrano soltanto i dati più rilevanti: attraverso il pulsante :guilabel:`Mostra dettagli` è possibile accedere al set completo dei dati del grafico.
Alcuni tipologie di grafico consentono di nascondere uno o più set di dati che si vuole temporaneamente trascurare: per farlo è sufficiente cliccare sul relativo nome nella legenda del grafico.

.. _report-settings-ref-label:

Impostazioni
============

Le impostazioni dei report sono accessibili cliccando il pulsante con l'icona di ingranaggio nella barra degli strumenti in alto a destra.
Il pulsante è visibile soltanto se è stato effettuato il login con l'utenza ``admin``.

Le impostazioni sono organizzate nelle seguenti sezioni:

- Generali
- Destinazioni
- Costi
- Ripristina impostazioni

Generali
--------

In questa sezione è possibile configurare le seguenti impostazioni:

- :guilabel:`Inizio/fine orario lavorativo`: questa informazione è usata dai grafici che tracciano dati in riferimento alle fasce orarie della giornata
- :guilabel:`Numero massimo di risultati`: indica quanti risultati possono essere mostrati da un grafico tabellare. Se questo limite viene raggiunto, appare un'icona di avvertimento di fianco al titolo del grafico
- :guilabel:`Durata chiamate nulle`: le chiamate con durata minore o uguale a questo valore sono considerate nulle
- :guilabel:`Valuta`: usata per visualizzare il costo delle chiamate

Destinazioni
------------

Le destinazioni sono utilizzate per calcolare i costi delle chiamate. La configurazione predefinita prevede le seguenti destinazioni:

- ``National``: numerazioni nazionali
- ``Mobile``: numerazioni cellulari
- ``International``: numerazioni estere
- ``Emergency``: numerazioni di emergenza
- ``PayNumber``: numerazioni a tariffa maggiorata

È possibile aggiungere nuove destinazioni così come rimuovere quelle esistenti.

Espandendo la voce :guilabel:`Configura i prefissi di destinazione` è possibile configurare la destinazione di una chiamata tramite il prefisso del numero di telefono composto. Siccome ogni prefisso definito può avere lunghezza variabile e sono quindi possibili sovrapposizioni, la destinazione di una numerazione telefonica è stabilita selezionando il prefisso più specifico (ovvero il più *lungo*). 
Ad esempio, supponendo di associare il prefisso ``0039`` alla destinazione ``National``, e il prefisso ``00393`` alla destinazione ``Mobile``, una chiamata in uscita con numerazione ``00393401234567`` avrà come destinazione ``Mobile``, poiché il prefisso ``00393`` è più specifico rispetto al prefisso ``0039``.

Costi
-----

Dopo aver configurato le destinazioni delle chiamate e i prefissi di destinazione, è possibile configurare i costi delle chiamate.
Il costo di una telefonata è determinato dal fascio PBX e dalla destinazione della chiamata.
Per configurare un nuovo costo, quindi, è sufficiente specificare il fascio, la destinazione e la relativa tariffa al secondo.

Esempio di configurazione di un nuovo costo
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Si supponga di avere attivato su un fascio PBX di nome ``trunk_1`` un contratto telefonico secondo il quale le chiamate verso la Spagna hanno una tariffazione di 0.01 EUR al secondo. Per far sì che il costo di queste chiamate sia calcolato e mostrato nel report, è necessario seguire i seguenti passi:

- Accedere al report con utenza ``admin``
- Accedere alle impostazioni
- Definire una nuova destinazione, denominandola ad esempio ``Spagna``
- Configurare un nuovo prefisso di destinazione, indicando il prefisso nazionale spagnolo (``0034`` oppure ``+34``, in funzione di come è stato configurato il centralino) e selezionando ``Spagna`` come destinazione
- Configurare un nuovo costo, selezionando il fascio ``trunk_1``, la destinazione ``Spagna`` e indicando ``0.01 EUR`` come costo al secondo

Da questo momento, ogni notte un processo elaborerà i costi delle chiamate effettuate dal fascio ``trunk_1`` verso la Spagna.
I costi delle chiamate sono quindi disponibili dal giorno successivo alla configurazione.

Ripristina impostazioni
-----------------------

.. warning::

   Il ripristino delle impostazioni è irreversibile

In questa sezione è presente un pulsante per ripristinare tutte le impostazioni ai loro valori predefiniti. Cliccando il pulsante e confermando la scelta saranno ripristinate tutte le impostazioni contenute nella sezione :guilabel:`Generali`, tutte le destinazioni, i prefissi di destinazione e saranno eliminate tutte le configurazioni dei costi.
