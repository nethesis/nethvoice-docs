========================
Report Chiamate Entranti
========================

Il Report delle Chiamate Entranti è un modulo di |product| che consente di avere un'analisi statistica e dei grafici dedicati a tutte le chiamate entranti.

L’accesso al Report Chiamate Entranti è consentito di default all’utente admin e ad ogni utente membro del gruppo inboundmanager, che se non presente va creato.

Il modulo si divide in due sezioni principalmente, quelle Generale e Distribuzione dove vengono racconti i dati statistici, e quella dei Grafici dove questi dati vengono utilizzati per produrre dei grafici che semplificano l'analisi dei dati.

Accedendo al modulo si entra nella Dashboard che riepiloga i grafici più significativi.

Generale
========

Rotte In Entrata
----------------

In questa sezione si trovano le chiamate ricevute per ogni Rotta in Entrata configurata in |product| suddivise in riposte, perse, occupate e fallite e il tempo di conversazione totale.

E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata ed esportare il risultato in un file .xls


Gruppi di Chiamata
------------------

In questa sezione si trovano le chiamate che hanno avuto come destinazione un Gruppo di Chiamata configurato in |product|, viene visualizzata la Rotta in entrata di arrivo, il numero del Gruppo di Chiamata, il totale delle chiamate ricevute e la durata totale.

E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata ed esportare il risultato in un file .xls


Code
---- 

In questa sezione si trovano le chiamate che hanno avuto come destinazione una Coda configurata in |product|, viene visualizzata la Rotta in entrata di arrivo, il numero della Coda, il totale delle chiamate ricevute e la durata totale.   
 
E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata ed esportare il risultato in un file .xls


Caselle Vocali
--------------

In questa sezione si trovano le chiamate che hanno avuto come destinazione una Casella Vocale configurata in |product|, viene visualizzata la Rotta in entrata di arrivo, il numero della Casella Vocale e il tipo ("b" busy , "u" unavailable, "s" no message) il totale delle chiamate ricevute e la durata totale. 
 
E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata ed esportare il risultato in un file .xls


IVR
---

In questa sezione si trovano le chiamate che hanno avuto come destinazione un IVR configurato in |product|, viene visualizzata  il nome dell'IVR, la scelta effettuata dal chiamate e il totale delle chiamate.
 
E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata ed esportare il risultato in un file .xls


Per Chiamante
-------------

In questa sezione si trovano tutte le chiamate ricevute dal |product| e viene mostrato il numero, nome, azienda, periodo, rotta in entrata utilizzata, numero chiamate risposte, perse, occupate, fallite, tempo di attesa e tempo di conversazione.

E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata, nel campo Chiamante si può indicare sia il numero chiamante, il nome o l'azienda, ed esportare il risultato in un file .xls

L'associazione nome azienda numero viene fatta da |product| attingendo alla Rubrica Centralizzata al momento della ricezione della chiamata ma è possibile attivare un processo settimanale che lo faccia a ritroso per utilizzare contatti inseriti magari successivamente alla ricezione della chiamata.
Per attivarlo::

 config setprop nethvoice neth-inbound-report-phonebook enabled


Distribuzione
=============


Oraria
------

In questa sezione le chiamate entranti vengono distribuite nell'arco temporale giornaliero per ogni Rotta in Entrata e suddivise per esito ( "R" risposte, "N" non risposte, "O" occupate, "F" fallite).

E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata ed esportare il risultato in un file .xls


Geografica
----------

In questa sezione le chiamate entranti vengono raggruppate per zona geografica e possono essere divise per Regione, Provincia o Prefisso.

E' possibile utilizzare il filtro per creare una ricerca più particolareggiata nel tempo o per singola Rotta in Entrata ed esportare il risultato in un file .xls


Grafici
=======

Carico
------

In questa sezione vengono mostrati i grafici per la distribuzione del totale delle chiamate entranti suddivise nelle varie Rotte in Entrata nella sezione di tempo scelta e di seguito divise per la zona geografica di provenienza scelta. 


Per ora
-------

In questa sezione vengono mostrati i grafici per la distribuzione oraria del totale delle chiamate entranti suddivise nelle varie Rotte in Entrata nella sezione di tempo scelta.


Per Rotta in Entrata
--------------------

In questa sezione vengono mostrati i grafici per il totale delle chiamate entranti suddivise nelle varie Rotte in Entrata nella sezione di tempo scelta.


Per zona
--------

In questa sezione vengono mostrati i grafici per il totale delle chiamate entranti suddivise nelle varie Rotte in Entrata nella sezione di tempo scelta in base alla zona geografica di provenienza.


Durata media
------------

In questa sezione vengono mostrati i grafici per la durata media delle chiamate entranti suddivise nelle varie Rotte in Entrata nella sezione di tempo scelta in base all'orario di entrata.


