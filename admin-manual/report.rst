=============
Report (beta)
=============

.. warning::

   Il nuovo report è una **beta**, ovvero il software non è in versione definitiva.
   Pertanto può contenere bug e funzionalità implementate solo in parte.

Il nuovo report unificato di |product| consente di utilizzare un'unica interfaccia web per consultare:

- report code
- report chiamate entranti e costi (in sviluppo)

Il report è accessibile all'indirizzo ``https://<server_name>/pbx-report``.
Ogni utente può accedere con le stesse credenziali utilizzate all'interno del |product_cti|.
Le tabelle e i grafici visualizzati saranno filtrati in base al profilo |product_cti| associato all'utente.

Il report consente l'accesso solo ai dati storicizzati a partire dal giorno precedente, indietro fino alla data di primo
utilizzo del centralino. Tutte le notti un processo elabora gli eventi della giornata e li rende disponibili per visualizzare
grafici e tabelle.
Quindi, al termine della prima installazione, è necessario attendere il giorno successivo per consultare il report.

È possibile installare il report direttamente dal :guilabel:`Software Center` selezionando il modulo chiamato ``Nethvoice report (beta)``.

Report code
===========

Il modulo si divide in varie sezioni che ricalcano in parte quelle presenti nel :ref:`vecchio report code <queuereport-ref-label>`.
Ulteriori sezioni sono accessibili dal menu di sinistra.

Report chiamate & report costi
==============================

Ancora **NON** implementato.
I dati sono consultabili dal :ref:`vecchio report chiamate <inboundreport-ref-label>` e da |product_cti|.
