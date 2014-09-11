==========================
Panoramica Tipologie Linee
==========================


Introduzione
============

Un generico centralino deve poter gestire telefoni analogici e isdn e spesso un cablaggio dedicato. Quindi i collegamenti con l'esterno possono essere di tipo:

-  **analogico:** un canale per ogni linea. Con comportamenti soliti: squillo, chiamata, visualizzazione del numero del chiamante solo se abilitato dal provider.
-  **ISDN**: passano due canali voce contemporaneamente, attraverso una borchia ISDN denominata NT1. La voce viene codificata in pacchetti, passando da analogico a digitale
-  **Accesso primario**: cablaggio dedicato tramite il quale è possibile ricevere/fare da 15 a 30 chiamate contemporaneamente.

Quindi per **Linee esterne** (Linee) si intendono i collegamenti del PBX verso la Rete Telefonica Pubblica (PSTN)

Linee Analogiche fonia
======================

-  Più linee analogiche, devono avere ognuna il proprio numero.
-  Per più telefonate contemporanee, viene definito un numero come capogruppo e si configurano le altre linee in ricerca automatica (servizio da richiedere al gestore).
-  Di default il numero del chiamante non viene passato al centralino, questa funzionalità va richiesta al provider
-  Necessario un gateway analogico di tipo FX0 per collegarla al |product|

Linee Accesso Base ISDN
=======================

-  2 canali per fonia/dati (BRI)
-  Multinumero: si possono avere fino a 8 numeri diversi.
-  servizio di selezione passante: da richiedere al provider (non può essere fatto dal centralino). Il provider non mette a disposizione un numero ma una radice, l'utente può personalizzare le cifre terminali a proprio piacimento, direzionandole ad esempio ad interni specifici.
   Il centralino gestisce gli ultimi numeri, digitati dopo la radice.
-  connessione **T0 / S0** per il lato PBX
-  Necessario un gateway isdn per per collegare la borchia al |product|

Gli apparati per le linee ISDN possono essere di diverso tipo

-  **NT1**: sull'apparato (borchia) è disponibile solo un cavo digitale denominato bus S0. Non mette a disposizione linee analogiche.

-  **NT1 plus**: oltre al cavo digitale S0 ha anche due linee analogiche dove potete attaccare ad esempio telefoni analogici tradizionali.

Le borchie isdn possono essere programmate dal gestore telefonico, in modi diversi:

-  **PP Punto Punto**: un solo apparato ISDN su bus s0

-  **PPMP Punto MultiPunto**: più apparati ISDN possono essere collegati sul Bus s0


.. note:: Sapere com'è stata  programmata la borchia è indifferente ai fini della connessione, alla borchia verrà collegato sempre e solo il centralino, ma è indispensabile per la configurazione del gateway isdn che deve sapere in che modalità lavorare. 

Linee Accesso Primario ISDN
===========================

-  30 canali per fonia/dati (PRI)
-  connessione **T1** lato PBX
-  da 15 a 30 chiamate contemporaneamente. Possono essere definite in
   ricezione ed uscita, quindi bidirezionali.
-  apparato del gestore telefonico denominato **DTE**
-  possibile servizio di selezione passante

Linee Voip
==========

E' possibile configurare sul |product| linee di tipo Voip. Basta configurare, secondo le specifiche del provider, un :doc:`fascio SIP. <configurazione_provider_voip>`

