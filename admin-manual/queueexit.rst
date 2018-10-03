Uscita Coda
===========

Il modulo Uscita Coda (Queue Exit) permette di differenziare il comportamento di una chiamata che abbandona per un fallimento la coda.

A seconda della motivazione del fallimento (Timeout, Coda Piena, Coda senza Agenti etc.) è possibile far proseguire la chiamata verso ogni altro modulo di |product|.

Inoltre la motivazione di ogni fallimento verrà scritta anche nel database che raccoglie tutti i dati delle code in modo da essere utilizzabile nel :ref:`Report Code <queuereport-ref-label>`.

Configurazione
--------------

Nome
~~~~

Nome che poi verrà utilizzato da |product| nelle destinazioni dei vari moduli.

Destinazione Timeout
~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata se fallisce con motivazione TIMEOUT, tempo di attesa massimo superato.


Destinazione Full
~~~~~~~~~~~~~~~~~

Destinazione della chiamata se fallisce con motivazione FULL, numero massimo di chiamate in attesa superato.


Destinazione Joinempty
~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata se fallisce con motivazione JOINEMPTY, ingresso in coda senza agenti collegati.


Destinazione Leaveempty
~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata se fallisce con motivazione LEAVEEMPTY, uscita dalla coda per assenza di agenti collegati.


Destinazione Joinunavail
~~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata se fallisce con motivazione JOINUNAVAIL, ingresso in coda senza agenti disponibili.


Destinazione Leaveunavail
~~~~~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata se fallisce con motivazione LEAVENAVAIL, uscita dalla coda per assenza di agenti disponibili.


Destinazione Continue
~~~~~~~~~~~~~~~~~~~~~

Destinazione della chiamata se fallisce con motivazione CONTINUE, uscita dalla coda per chiusura della chiamata da parte dell'agente.


