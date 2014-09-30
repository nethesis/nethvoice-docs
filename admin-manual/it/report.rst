======
Report
======

.. _informazioni_sul_sistema_ref_label:

Informazioni sul Sistema
========================

Descrizione
-----------

Il modulo Informazioni Sistema serve a controllare lo stato di tutta la parte SIP e IAX del |product|, avendo dei delle notifiche anche particolareggiate per ogni tipo di servizio.

Sommario
--------

Pagina introduttiva che riepiloga lo stato di canali, registrazioni, :ref:`Fasci SIP <fasci_sip_ref_label>` e :ref:`Fasci IAX <fasci_iax_ref_label>`.

Registrazioni
-------------

Lo stato delle registrazioni dei :ref:`Fasci SIP <fasci_sip_ref_label>` e dei :ref:`Fasci IAX <fasci_iax_ref_label>`.

Canali
------

I canali attivi sia IAX che SIP con i dettagli delle varie chiamate.

Peers
-----

Lo stato degli oggetti Peers di Asterisk tipicamente i :ref:`Fasci SIP <fasci_sip_ref_label>` e i :ref:`Fasci IAX <fasci_iax_ref_label>`.

Anche gli :ref:`Interni SIP <interni_sip_ref_label>` e gli :ref:`Interni IAX <interni_iax_ref_label>` hanno una parte Peer, essendo degli oggetti friend di Asterisk(user + peer).

Info Sip
--------

Lo stato di tutti gli oggetti SIP presenti sul |product|.

Info IAX
--------

Lo stato di tutti gli oggetti IAX presenti sul |product|.

Conferenze
----------

Lo stato delle :ref:`Conferenze <conferenze_ref_label>` attive sul |product|.

Subscriptions
-------------

Elenco di tutti gli hints, oggetti creati dal |product| per consentire a tutti i terminali SIP di monitorare lo stato di altri interni e di tutti gli oggetti creati dai vari moduli che possono essere controllati.

Viene mostrato il loro stato, il codice per controllarli e quanti li controllano.

Utenti Caselle Vocali
---------------------

Stato di tutte le :ref:`Caselle Voceli <casella_vocale_ref_label>` configurate sul |product|.

Code
----

Stato di tutte le :ref:`Code <code_ref_label>` configurate sul |product|.

Rapporto Completo
-----------------

Tutti Report qui elencati uno dopo l'altro.

.. _file_log_di_asterisk_ref_label:

File Log di Asterisk
====================

Descrizione
-----------

Il modulo File Log di Asterisk serve a visualizzare sull'interfaccia di |product| porzioni di log di Asterisk per finalità di diagnostica.

Configurazione
--------------

Inserire il numero di righe da visualizzare e cliccare su Visualizza Log.

.. _report_cdr_ref_label:

Report CDR
==========

Descrizione
-----------

Il modulo Report CDR (Call Detail Record) riporta tutte le chiamate fatte, ricevute e tentate transitate per il |product|, con tutti i dettagli delle singole chiamate.

Viene mostrata l'ora, la data, il chiamante, il chiamato, l'esito, il canale sorgente e quello di destinazione e la durata per ogni chiamata.

Inoltre essendo integrato nel |product| anche il Channel Event Logging (CEL) è possibile cliccando nell'id univoco di ogni chiamata elencato nella colonna Sistema accedere ai dettagli più specifici della chiamata.

Vengono infatti elencati tutti gli eventi che hanno interessato la chiamata dall'evento di inizio (CHAN\_START) agli ultimi (HANGUP e LINKEDID\_END), si possono avere quindi informazioni dettagliate come se è stata messa in attesa, se è stata trasferita etc.

Gli eventi del CEL essendo molto numerosi vengono mantenuti sul |product| di default per 180 giorni.

Se si vuole modificare questa configurazione aumentando il numero di giorni (valutare bene che lo storage a disposizione sia sufficiente) o diminuendolo basta creare un Template per il file ::

  /etc/cron.daily/nethvoice_clean_cel

Configurazione
--------------

Il box di ricerca permette di selezionare solo le chiamate che interessano.

E' possibile filtrare le chiamate per tutti i campi proposti selezionando tramite il radio button per quale campo ordinare i risultati.

Per ogni campo, poi, è possibile indicare dei criteri di ricerca: per i campi temporali dei lassi di tempo, per gli altri dei valori che possono o non (se viene spuntata la checkbox Non) iniziare o contenere o finire o essere esattamente i valori digitati.

Passando con il mouse sul simbolo + in alto a destra del box di ricerca, si attiva un altro piccolo box per decidere con che tipo di output avere i risultati della ricerca, se nella pagina del modulo, Ricerca CDR, in un file CSV e se avere un resoconto grafico dei risultati.

E' poi configurabile un numero limite di risultati per la ricerca.

Data
~~~~

Seleziona l'intervallo di tempo per il report. E' possibile selezionare giorno, mese, anno ora e minuto.

Canale Sorgente
~~~~~~~~~~~~~~~

Seleziona il canale sorgente su cui ricercare. Inserire semplicemente il tipo canale, ad esempio SIP, IAX2 o Local, il fascio o il numero chiamante, o entrambi, ad esempio SIP/201.

Sorgente
~~~~~~~~

Ricerca nel sorgente chiamata. E' possibile inserire diverse sorgenti separate dalla virgola. Questo campo supporta i :ref:`Pattern di Asterisk <pattern_ref_label>`.

Numero Chiamante
~~~~~~~~~~~~~~~~

Cerca il numero chiamante.

Numero Chiamato
~~~~~~~~~~~~~~~

Cerca il numero chiamato.

Canale Destinazione
~~~~~~~~~~~~~~~~~~~

Seleziona il canale destinazione su cui ricercare. Inserire semplicemente il tipo canale, ad esempio SIP, IAX2 o Local, il fascio utilizzato o il numero chiamato, o entrambi ad esempio SIP/2001.

Destinazione
~~~~~~~~~~~~

Ricerca nella destinazione chiamate. E' possibile inserire valori multipli seprata da virgola. Questo campo supporta i :ref:`Pattern di Asterisk <pattern_ref_label>`.

Campo Utente
~~~~~~~~~~~~

Cerca campo userfiled (se abilitato).

Codice per Tariffazione
~~~~~~~~~~~~~~~~~~~~~~~

Cerca nel codice per tariffazione

Durata
~~~~~~

Cerca chiamate che corrispondono alla durata specificata.

Esito
~~~~~

Cerca chiamate che corrispondono allo stato RISPOSTO, OCCUPATO, FALLITO o NESSUNA RISPOSTA.

Prima il più ...
~~~~~~~~~~~~~~~~

Ordinare i risultati dal più recente o dal più vecchio.

Raggruppato per
~~~~~~~~~~~~~~~

Raggruppa i risultati per la voce specificata.

Tipo Report
~~~~~~~~~~~

Tipo di report, ricerca CDR, file CSV.

Limiti Risultato
~~~~~~~~~~~~~~~~

Limite ai risultati della ricerca.

.. _stato_sistema_ref_label:

Stato Sistema
=============


Descrizione
-----------

Il modulo Stato Sistema viene utilizzato come dashboard o pagina iniziale all'acceso in |product|.

Ha il semplice scopo di dare un colpo d'occhio sullo stato del |product|: su quello che sta facendo, sullo stato dei servizi indispensabili per il funzionamento, sull'utilizzo delle risorse hardware e sull'eventuale presenza di problematiche.

Notifiche |product|
-------------------

In questa sezione si trovano tutte le notifiche riguardanti il |product|, eventuali problemi gravi, warning e problemi di configurazione.

Statistiche di Sistema
----------------------

Viene dato in tempo quasi reale l'utilizzo delle risorse di sistema da parte del |product|, a partire dall'uso della CPU a memoria, dischi ed interfacce di rete.

Statistiche |product|
---------------------

Vengono elencate le attività in corso del |product|, le attuali chiamate in corso, i telefoni attivi, le registrazioni dei fasci effettuate.

Tempo di Esercizio
------------------

Il tempo da quanto i vari servizi di |product| sono attivi.

Stato Server
------------

Lo stato dei servizi alla base del |product|, Asterisk, MySQL e il Server Web(Apache).

