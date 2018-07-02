=======================================
Codici rapidi di chiamata (Rapid Code)
=======================================

Il modulo :index:`Codici rapidi di chiamata`, consente di configurare un numero breve per effettuare una chiamata.

Sostituisce il vecchio modulo Speed Dial ed è installato di default con |product|.

I codici di chiamata vengono inoltre inseriti nella rubrica centralizzata, l'etichetta verrà utilizzata come nome.

Configurazione
===============

Per aggiungere un nuovo codice rapido, andare nell'interfaccia avanzata di |product|, poi nel menù :menuselection:`Applicazioni -> Codice Rapido di Chiamata`.

Facendo click su :guilabel:`+ Aggiungi codice rapido di chiamata` verrà visualizzato un form in cui inserire un'"etichetta" cioè un nome da assegnare a questo codice, il numero di telefono da chiamare e il codice rapido da usare.

Per comporre il numero, sarà sufficiente digitare il codice di questa applicazione (\*99 di default) seguito dal codice assegnato.

Per esempio, se assegno il codice 1 al numero 1234567890, digitando da un telefono \*991 verrà composto il numero 1234567890.

Non è necessario applicare i cambiamenti dopo aver aggiunto un codice, questo sarà subito operativo.



Importazione da CSV
--------------------

Sempre dall'interfaccia, è possibile importare i codici da un file CSV. Ogni riga del file CSV deve avere questo formato: ``<NOME>,<NUMERO>,<CODICE>``
per esempio: ::

    Mario Rossi,33312341234,1

In questo caso, componendo \*991 verrà composto il numero 33312341234.


Modificare il codice applicazione
----------------------------------

Per utilizzare un codice diverso da quello di default (\*99), è possibile scegliere un altro codice dal modulo :guilabel:`Codici servizi` che si trova nell'interfaccia avanzata, :menuselection:`Amministrazione -> Codici servizi`
