=============
Report (beta)
=============

.. warning::

   Il nuovo report è una **beta**, ovvero il software non è in versione definitiva.
   Pertanto può contenere bug e funzionalità implementate solo in parte.

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

Report chiamate & costi (CDR)
=============================

Il report CDR mostra informazioni aggregate e di dettaglio relative al registro chiamate.
I grafici delle sezioni :guilabel:`Dati centralino` e :guilabel:`Dati personali` presentano la stessa struttura, mostrando:

- un grafico riepilogativo espandibile che mostra dati sui totali e le durate delle chiamate
- un registro chiamate tabellare che mostra numero sorgente, numero di destinazione, esito chiamata, durata e costo. Cliccando il pulsante :guilabel:`Mostra dettagli` è possibile visualizzare ulteriori dettagli di ciascuna chiamata

Una parte dei dati di questo report è consultabile anche sul :ref:`vecchio report chiamate <inboundreport-ref-label>` e da |product_cti|.

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
* accedere alle impostazioni dei report. Questa funzionalità è disponibile soltanto se è stato effettuato l'accesso con l'utenza ``admin``
* eseguire il logout

Grafici
-------

L'area dei grafici costituisce quella di maggior interesse per l'utente e costituisce il corpo del report della vista corrente.
Ciascun grafico può essere esportato in almeno uno dei seguenti formati: CSV, PNG e PDF.
Per motivi di leggibilità alcuni grafici mostrano soltanto i dati più rilevanti: il pulsante :guilabel:`Mostra dettagli` è possibile accedere al set completo dei dati del grafico.
Alcuni tipologie di grafico consentono di nascondere uno o più set di dati che si vuole temporaneamente trascurare: per farlo è sufficiente cliccare sul relativo nome nella legenda del grafico.
