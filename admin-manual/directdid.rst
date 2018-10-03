Selezioni Passanti
==================

Il modulo Selezioni Passanti consente di attivare una selezione passante multinumero in entrata su |product|.

Facendo transistare la chiamata entrante in questo modulo, ad esempio da una rotta in entrata con numero chiamanto variabile che comprenda tutta la selezione passante, la destinazione sarà automaticamente l'interno di riferimento della numerazione chiamata.

Sarà poi possibile gestire il tempo di squillo e l'eventuale fallimento della chiamata per non risposta, destinazione occupata o non disponibile.


Configurazione
--------------

Radice selezione passante
~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire la parte numerica della selezione passante che non è variabile, ad esempio con selezione passante 07214055XX inserire 07214055.


Numero cifre variabili
~~~~~~~~~~~~~~~~~~~~~~

Inserire il numero di cifre della selezione passante che è variabile, ad esempio con selezione passante 07214055XX inserire 2.


Prefisso interni
~~~~~~~~~~~~~~~~

Inserire un eventuale prefisso da aggiungere alle cifre variabile per ottenere l'interno a cui destinare la chiamata entrante, ad esempio con selezione passante 07214055XX e interni 2XX, inserire 2.


Timeout
~~~~~~~

Inserire il tempo di squillo massimo dopo il quale considerare l'interno da contattare non raggiungibile.


Destinazione se timeout
~~~~~~~~~~~~~~~~~~~~~~~

Inserire la destinazione della chiamata entrante se l'interno di destinazione non ha risposto entro il tempo di Timeout.

Destinazione se occupato
~~~~~~~~~~~~~~~~~~~~~~~~

Inserire la destinazione della chiamata entrante se l'interno di destinazione è occupato.

Destinazione se non disponibile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserire la destinazione della chiamata entrante se l'interno di destinazione non è disponibile, ad esempio spento.
