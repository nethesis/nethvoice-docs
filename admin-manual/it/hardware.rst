================================
Hardware |product|
================================

L'utilizzo di |product| non è vincolante rispetto alla scelta dell'hardware da utilizzare, non è quindi obbligatorio scegliere determinate marche o modelli da affiancare al centralino. E' necessario però conoscere quali hardware scegliere in base alle proprie esigenze e all'apparato telefonico in cui |product| verrà installato.

Qiualora si voglia installare |product| su dell'hardware proprio, per stabilire la compatibilità hardware di |product| fare riferimento a quella di |parent_product|.


L'obiettivo di questo documento è segnalare prodotti testati e consigliati, in base alle esigenze operative e strutturali del cliente.


Perchè usare gateway esterni?
=============================

|product| supporta esclusivamente l'utilizzo di gateway esterni (eccezion fatta per i flussi primari).

Ogni gateway esterno che utilizza corretamente il protocollo Sip è teoricamente compatibile.

I motivi di tale scelta sono molti:

-  sono più affidabili
-  gestiscono meglio i protocolli di comunicazione
-  :doc:`maggiormente configurabili <configurazione_patton>` 
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

Inserire la scheda sul centralino e da riga di comando digitare: ::

 nethvoice hwconf

per configurarla.

-  :doc:`Configurazione Patton <configurazione_patton>`

Ogni modello di **Patton** PRI è compatibile, esistono al momento **Patton** da una o quattro porte PRI.

Gateway ISDN
------------

 :doc:`Configurazione Patton <configurazione_patton>`

-  Ogni modello di **Patton** ISDN è compatibile, esistono al momento **Patton** da una, due, quattro o otto porte ISDN.

Gateway Analogici
-----------------

 :doc:`Configurazione Patton <configurazione_patton>`

-  Ogni modello di **Patton** analogico è compatibile, esistono al momento **Patton** da due o quattro porte FXO

Gateway Misti
-------------

 :doc:`Configurazione Patton <configurazione_patton>`

-  Per gateway Misti si intende modelli di **Patton** che supportano sia linee ISDN che analogiche

Gateway GSM
-----------

 :doc:`Configurazione Patton <configurazione_patton>`

-  **Portech** mv370 - 1 SIM
-  **Portech** mv372 - 2 SIM
-  **Portech** mv370 - 1 SIM UMTS
-  **Portech** mv372 - 2 SIM UMTS

Linee interne
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

