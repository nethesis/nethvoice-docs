Google TTS
=============================

Descrizione
-----------

Il modulo Google TTS consente di generare le registrazioni di sistema utilizzando il Text To Speech di Google.

Questo modulo è installato automaticamente in |product|, ma è necessario configurare l'API key di Google per poterlo utilizzare. 

Configurazione
--------------

Accedendo alla pagina del modulo dall'interfaccia di configurazione avanzata per la prima volta, viene mostrata la pagina per configurare l'API key di Google.
Per ottenere l'API key, seguire questa guida https://cloud.google.com/docs/authentication/api-keys#creating_an_api_key


Creare una nuova registrazione TTS dal modulo FreePBX
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dopo aver configurato l'API key, il modulo presenterà l'interfaccia per creare una nuova registrazione TTS.
E' necessario inserire il nome e la descrizione per la registrazione. Questi verranno poi usati per identificare la registrazione tra le altre. Il nome deve essere univoco e inserendone uno uguale ad un altro già presente, questo verrà sovrascritto.

Le lingue disponibili sono quelle installate nel centralino.

E' possibile scegliere tra piu' voci tra quelle che Google mette a disposizione. Le voci "standard" sembrano meno naturali di quelle "wavenet".

Il testo verra' letto dalla voce.

Cliccando su conferma, il messaggio verrà registrato e si verrà rediretti alla pagina della registrazione. Da qui è possibile riascoltare il messaggio, convertirlo in un diverso formato o eliminarlo.

