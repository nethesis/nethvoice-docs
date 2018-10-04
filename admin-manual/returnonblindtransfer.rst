Ritorno da trasferimento Cieco
==============================

Il modulo gestisce il ritorno della chiamata trasferita in modo non cunsultativo all'interno autore del trasferimento se il destinatario del trasferimento non risponde per qualsiasi ragione, ad esempio interno occupato, non disponibile, etc.

E' possibile modificare il tempo di squillo del destinatario del trasferimento, e nell'eventuale ritorno della chiamata all'autore del tentato trasferimento cambiare il nome chiamante e la suoneria del telefono.


Configurazione
--------------

Attivato
~~~~~~~~

Attivare o disattivare il ritorno su trasferimento non cunsultativo.


Timeout
~~~~~~~

Tempo di squillo del tentativo di trasferimento non cunsultativo.

Caller ID
~~~~~~~~~

Impostare il Nome Chiamante per la chiamata di ritorno dal trasferimento fallito, è possibile usare *${xfer_exten}* che verrà sostituito con l'interno del destinatario del trasferimento e *${CALLERID(name)}* che verrà sostituito con il nome del chiamante originario.


Alertinfo
~~~~~~~~~

Inserire la stringa di alert info per variare la suoneria del telefono che riceve il ritorno dal trasferimento fallito, ad esempio *<http://www.notused>\;info=ring2*
