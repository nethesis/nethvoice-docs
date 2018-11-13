==========
Google TTS
==========


Descrizione
===========

Il modulo Google TTS consente di generare le registrazioni di sistema utilizzando il Text To Speech di Google.

Questo modulo è installato automaticamente in |product|, ma è necessario configurare l'API key di Google per poterlo utilizzare.
L'API Key è una stringa alfanumerica che consente a Google di identificare chi usufruisce del servizio e addebitargli il costo. Per questo motivo va custodita adeguatamente.

Configurazione
==============

Accedendo alla pagina del modulo dall'interfaccia di configurazione avanzata per la prima volta, viene mostrata la pagina per configurare l'API key di Google.
Per ottenere l'API key, seguire questa guida https://cloud.google.com/docs/authentication/api-keys#creating_an_api_key



Creare una nuova registrazione TTS dal modulo FreePBX
=====================================================

Dopo aver configurato l'API key, il modulo presenterà l'interfaccia per creare una nuova registrazione TTS.
E' necessario inserire il nome e la descrizione per la registrazione. Questi verranno poi usati per identificare la registrazione tra le altre. Il nome deve essere univoco e inserendone uno uguale ad un altro già presente, questo verrà sovrascritto.

Le lingue disponibili sono quelle installate nel centralino.

E' possibile scegliere tra più voci tra quelle che Google mette a disposizione. Si consiglia di utilizzare le voci "wavenet" in quanto più naturali di quelle "standard", tenendo comunque presente che sono più care https://cloud.google.com/text-to-speech/

Inserire nel campo "testo" il messaggio che verrà convertito in audio.

Cliccando su conferma, il messaggio verrà registrato e si verrà rediretti alla pagina della registrazione. Da qui è possibile riascoltare il messaggio, convertirlo in un diverso formato o eliminarlo.


Utilizzo del TTS Google da VisualPlan
=====================================

E' possibile utilizzare il TTS da VisualPlan ovunque sia possibile inserire una registrazione (Annunci, IVR, CQR).
Nel dialog di aggiunta della registrazione sarà possibile inserire l'API key di Google se non è ancora stato fatto.
Se invece è già stata inserita un'API key, verranno mostrate due opzioni, una per la lingua e una per la voce da utilizzare, ed il campo di testo dove digitare il messaggio che verrà letto dal TTS. Dopo aver compilato questi tre campi, sarà possibile ascotare il messaggio premendo sul tasto con l'icona dell'altoparlante. Infine, dopo aver ascoltato la registrazione, sarà possibile inserire un nome ed una descrizione per salvarla come registrazione di sistema.
