Opzioni Coda
============

Il modulo Opzioni Coda consente di aggiungere delle opzioni aggiuntive ad una coda o di sovrascrivere alcune opzioni.

Configurazione
--------------
Il modulo è raggiungibile dal menù dell'interfaccia avanzata:

Applicazioni -> Opzioni Coda

Dalla pagina principale, si visualizza la lista dei set di opzioni.

Cliccando su "Aggiungi opzioni coda" si potrà creare un nuovo set di impostazioni

Nome
~~~~
il nome di questo set. è solo un'etichetta e la sua utilità è solo quella di riconoscere questo set se se ne creano diversi

Prefisso CID
~~~~~~~~~~~~

stringa che viene posta prima del nome e numero del chiamante mostrati

Alert Info 
~~~~~~~~~~

utilizza questa stringa di alert info per modificare la suoneria dei dispositivi

Messaggio di ingresso
~~~~~~~~~~~~~~~~~~~~~

la registrazione che sentirà il chiamante quando entra in coda

Non ritentare al timeout
~~~~~~~~~~~~~~~~~~~~~~~~

prosegui nel dial plan dopo che è stato raggiunto il timeout invece di ritentare

Continua dopo hangup
~~~~~~~~~~~~~~~~~~~~

prosegue nel dial plan dopo che il chiamante ha chiuso la chiamata

Go Sub
~~~~~~

specifica una sezione del dial plan da eseguire quando il chiamante e l'operatore vengono messi in comunicazione

AGI
~~~

specifica uno script AGI da eseguire sul canale del chiamante

Imposta posizione
~~~~~~~~~~~~~~~~~

se abilitato, tenta di inserire il chiamante in coda ad una specifica posizione

Posizione
~~~~~~~~~

la posizione in cui viene inserito il chiamante se "Imposta posizione" è abilitato

Annuncio di conferma chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

annuncio che viene fatto sentire all'operatore quando risponde alla chiamata

Annuncio agente
~~~~~~~~~~~~~~~

sovrascrive l'annuncio agente configurato nella coda

Musica di attesa
~~~~~~~~~~~~~~~~

sovrascrive la classe di musica di attesa

Imposta il tempo massimo di attesa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

se abilitato, il tempo massimo d'attesa verrà sovrascritto da quanto specificato in "Attesa massima"

Attesa massima
~~~~~~~~~~~~~~

se è stato abilitato "Imposta il tempo massimo di attesa", sovrascrive il tempo massimo d'attesa in coda

Sovrascrivi destinazione su fallimento
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

se abilitato, la destinazione su fallimento verrà sovrascritta da quella impostata su "Destinazione su fallimento"

Destinazione su fallimento
~~~~~~~~~~~~~~~~~~~~~~~~~~

destinazione in caso di fallimento

Coda di destinazione
~~~~~~~~~~~~~~~~~~~~

destinazione dopo aver impostato le opzioni. Può essere una coda o un qualunque oggetto del dial plan. Quando la chiamata arriverà alla coda, verranno utilizzate le opzioni configurate nel modulo.

