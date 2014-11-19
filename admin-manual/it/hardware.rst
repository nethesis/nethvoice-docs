=================
Hardware
=================

Panoramica Tipologie Linee
==========================

Un generico centralino deve poter gestire telefoni analogici e isdn e spesso un cablaggio dedicato. Quindi i collegamenti con l'esterno possono essere di tipo:

-  **analogico:** un canale per ogni linea. Con comportamenti soliti: squillo, chiamata, visualizzazione del numero del chiamante solo se abilitato dal provider.
-  **ISDN**: passano due canali voce contemporaneamente, attraverso una borchia ISDN denominata NT1. La voce viene codificata in pacchetti, passando da analogico a digitale
-  **Accesso primario**: cablaggio dedicato tramite il quale è possibile ricevere/fare da 15 a 30 chiamate contemporaneamente.


Quindi per **Linee esterne** (Linee) si intendono i collegamenti del PBX verso la Rete Telefonica Pubblica (PSTN)

Linee Analogiche fonia
----------------------

-  Più linee analogiche, devono avere ognuna il proprio numero.
-  Per più telefonate contemporanee, viene definito un numero come capogruppo e si configurano le altre linee in ricerca automatica (servizio da richiedere al gestore).
-  Di default il numero del chiamante non viene passato al centralino, questa funzionalità va richiesta al provider
-  Necessario un gateway analogico di tipo FX0 per collegarla al |product|

Linee Accesso Base ISDN
-----------------------

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


.. note:: Sapere come'è stata  programmata la borchia è indifferente ai fini della connessione, alla borchia verrà collegato sempre e solo il centralino, ma è indispensabile per la configurazione del gateway isdn che deve sapere in che modalità lavorare. 

Linee Accesso Primario ISDN
---------------------------

-  30 canali per fonia/dati (PRI)
-  connessione **T1** lato PBX
-  da 15 a 30 chiamate contemporaneamente. Possono essere definite in
   ricezione ed uscita, quindi bidirezionali.
-  apparato del gestore telefonico denominato **DTE**
-  possibile servizio di selezione passante

Linee Voip
----------

E' possibile configurare sul |product| linee di tipo Voip. Basta configurare, secondo le specifiche del provider, un :ref:`fascio SIP <fasci_sip_ref_label>`


Hardware |product|
==================

L'utilizzo di |product| non è vincolante rispetto alla scelta dell'hardware da utilizzare, non è quindi obbligatorio scegliere determinate marche o modelli da affiancare al centralino. E' necessario però conoscere quali hardware scegliere in base alle proprie esigenze e all'apparato telefonico in cui |product| verrà installato.

Qualora si voglia installare |product| su dell'hardware proprio, per stabilire la compatibilità hardware di |product| fare riferimento a quella di |parent_product|.


L'obiettivo di questo documento è segnalare prodotti testati e consigliati, in base alle esigenze operative e strutturali del cliente.


Perché usare gateway esterni?
-----------------------------

|product| supporta esclusivamente l'utilizzo di gateway esterni (eccezion fatta per i flussi primari).

Ogni gateway esterno che utilizza correttamente il protocollo Sip è teoricamente compatibile.

I motivi di tale scelta sono molti:

-  sono più affidabili
-  gestiscono meglio i protocolli di comunicazione
-  :ref:`maggiormente configurabili <configurazione_patton_ref_label>`
-  non aumentano il carico del server
-  sono indipendenti dall'hardware del centralino
-  permettono di usare hardware compatto e miniaturizzato
-  sono facilmente espandibili (aggiungendo altri gateway)
-  in caso di malfunzionamenti non è necessario riavviare il server ma
   soltanto il gateway
-  in caso di malfunzionamenti non è necessario aprire il server per cambiare la scheda interna ma va sostituito soltanto il gateway


 .. note:: |product| supporta schede interne solo per flussi primari


Linee Esterne
=============

PRI
---

-  **Digium** schede a 1, 2 o 4 flussi primari

 :ref:`Configurazione Schede Interne <configurazione_schede_interne_ref_label>` 

- Ogni modello di **Patton** PRI è compatibile, esistono al momento **Patton** da una o quattro porte PRI.
 
 :ref:`Configurazione Patton <configurazione_patton_ref_label>`


Gateway ISDN
------------

-  Ogni modello di **Patton** ISDN è compatibile, esistono al momento **Patton** da una, due, quattro o otto porte ISDN.

 :ref:`Configurazione Patton <configurazione_patton_ref_label>`


Gateway Analogici
-----------------

-  Ogni modello di **Patton** analogico è compatibile, esistono al momento **Patton** da due o quattro porte FXO

 :ref:`Configurazione Patton <configurazione_patton_ref_label>`


Gateway Misti
-------------

-  Per gateway Misti si intende modelli di **Patton** che supportano sia linee ISDN che analogiche

 :ref:`Configurazione Patton <configurazione_patton_ref_label>`


Gateway GSM
-----------

-  **Portech** mv370 - 1 SIM
-  **Portech** mv372 - 2 SIM
-  **Portech** mv370 - 1 SIM UMTS
-  **Portech** mv372 - 2 SIM UMTS

 :ref:`Configurazione Portech <configurazione_portech_ref_label>`


Linee Interne
=============

ATA SIP
-------

-  **Cisco** SPA112 ad esempio, esistono anche adattatori FXS di altre marche.
-  Ogni modello di **Patton** analogico con porte FXS

ATA IAX
-------

-  `Iaxy <http://www.digium.com/en/products/analog/s101i.php>`_

Telefoni
========

WiFi e Dect
-----------

Il **wifi** non è adatto ad ambienti industriali, in quanto è un protocollo debole ed instabile in caso di rumore elettrico. E' adatto solo per piccoli uffici e coperture ridotte. L'alternativa dal punto di vista della copertura e della stabilità è il **dect**, utilizzando queste soluzioni a seconda del numero di cordless necessario e della vastità dell'area da coprire:

-  ata + cordless dect
-  cordless dect con base IP
-  cella radiobase polycom-kirk + cornette + eventuali ripetitori kirk

Telefoni IP
~~~~~~~~~~~

Ogni modello di telefono IP che gestisce correttamente Il protocollo Sip è compatibile. La scelta dipende poi dalle funzionalità desiderate in ogni postazione.

Al momento consigliamo **Yealink** o **Snom** come marca con il miglior rapporto qualità/prezzo.

