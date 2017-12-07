===============
|product_hotel|
===============

|product_hotel| è un modulo di |product| che permette di gestire degli interni opportunamente configurati come camere di un hotel.

L’accesso al |product_hotel| è consentito di default all’utente admin e ad ogni utente membro del gruppo hotelmanager, che se non presente va creato.

Caratteristiche principali:

* Check-in/Check-out camere
* Sveglia
* Sveglia di gruppo
* Report chiamate
* Personalizzazione Tariffe
* Numeri brevi
* Storico chiamate
* Abilitazione/Disabilitazione chiamate fra camere

Configurazione |product|
========================

Tutti gli interni che fanno parte del contesto **camere** entrano a far parte della gestione |product_hotel|.

E' possibile trasformare un interno in camera modificando il contesto direttamente dai dettagli dell'interno, oppure attraverso il modulo **Gestione camere** nel pannello di configurazione di |product|.


Come configurare il centralino
==============================
Consigliamo di configurare il centralino in questo modo:

* tutti gli interni delle camere devono essere aggiunti al contesto camere sul pannello di gestione del centralino in Gestione Camere
* gli interni di servizio, come ad esempio la reception, non devono essere aggiunti al contesto camere e devono essere configurati con interni standard, seguendo la normale politica dell'hotel. Ad esempio se le camere avranno come range di interni dal 201 al 299, l'interno della reception dovrà essere sempre a 3 cifre, ad esempio 200 o 300. Per consentire alle camere di chiamare la reception bisognerà configurare un numero breve, invece gli interni di servizio tra di loro si dovranno chiamare direttamente.
* è consigliata la creazione di due rotte in uscita sul centralino, la prima senza prefisso **limitata agli interni di servizio** per farli chiamare all'esterno numeri di 5 o più cifre, la seconda con il prefisso scelto nelle opzioni del |product_hotel| per far chiamare le camere (**ATTENZIONE l'ordine è IMPORTANTE**). Un unico accorgimento bisogna ricordarsi, per chiamate dagli interni di servizio, nel caso di corrispondenza tra numeri di emergenza e numeri delle camere (112,113 etc..), di utilizzare per chiamare i numeri di emergenza il prefisso come se si fosse una camera.
* è possibile utilizzare un unica rotta in uscita con prefisso, sia per le camere che per gli interni di servizio, in questo caso però ad esempio dal telefono della reception non si potrà richiamare direttamente i numeri delle chiamate perse sul telefono per l'assenza del prefisso in questi ultimi.

Codici funzioni da telefono
===========================
Nell'interfaccia di gestione del centralino |product| in Codici Servizi si trovano i codici per utilizzare le funzionalità del |product_hotel| dai telefoni.

Ad esempio per aggiungere un extra per una camera dovrò chiamare ::

 *33 + Interno Camera + # + Id Extra + # + Numero

Gestione camere
===============

Nella pagina principale sono elencate tutte gli interni configurati. Le camere vengono divise in tab a seconda del valore numerico del campo callgroup dell'interno telefonico, configurabile dall'interfaccia di |product|. Le camere libere sono contraddistinte dal colore verde, quelle che hanno già effettuato il check-in invece dal colore rosso, quelle da pulire dal colore giallo.

Tutte le funzioni disponibili sono presentate direttamente nel riquadro della camere. E' possibile anche utilizzare il menu contestuale con il tasto destro del mouse.

Sveglia

La sveglia può essere programmata una tantum oppure reiterata su più giorni.
Ogni cliente può configurare la sveglia della propria camera componendo il numero ::

 977

Gruppi
======

E' possibile raggruppare più camere in un unico gruppo. Questo consente effettuare operazioni su tutte le camere membre del gruppo (checkin, checkout, sveglia) e avere delle politiche sulle chiamate dedicate alle camere che fanno parte del gruppo nelle impostazioni(abilitazione chiamate tra le camere, abilitazione chiamate tra tutte le camere, abilitazione chiamate esterne).


Aggiungere un Extra
===================

Per aggiungere un extra ad una camera cliccare sulla relativa icona.


Report
======

Per ottenere il report del conto delle camere attualmente occupate è sufficiente cliccare sulla relativa icona. Il report riporta il dettaglio di ciascuna chiamata e di ogni extra, in fondo c'è un riepilogo che visualizza in tempo reale il conto totale.


Tariffe
=======

All'interno di |product_hotel| è presente un set predefinito di tariffe che variano in base al tipo di chiamata (es. cellulari, locali, ecc).
E' possibile modificare le tariffe esistenti o crearne di nuove. E' anche possibile abilitare/disabilitare le chiamate verso particolari numerazioni.


Extra
=====

E' possibile configurare degli extra. E' possibile poi assegnarli alle varie camere sia da interfaccia web e sia da telefono (ad esempio basta chiamare il ::

 *33201#99#3 per addebitare alla camera 201 tre volte l'extra che ha codice 99).  


Opzioni 
=======

Le opzioni generali comprendono:

* Configurazione del prefisso per effettuare chiamate esterne
* Formato interni
* Abilitazione/disabilitazione delle chiamate fra camere
* Abilitazione/disabilitazione delle chiamate fra camere che non hanno eseguito il check-in
* Interno da contattare per allarmi sveglia non risposta
* Abilitare il codice per la pulizia camere


Numeri Brevi
============

La sezione Numeri Brevi consente di specificare delle scorciatoie per chiamare interni predefiniti, ad esempio 9 per contattare la reception. E' possibile associare ad un numero breve uno dei gruppi temporali caricati nell'interfaccia di gestione del centralino |product|. Questo consente di configurare le due destinazioni per la chiamata, se la condizione temporale viene rispettata in Destinazione, se non lo è in Altrimenti.


Storico
=======

Qualora sia necessario consultare uno storico di tutte le chiamate effettuate dalle camere è possibile utilizzare la sezione **Storico**. Lo storico delle chiamate è filtrabile per data e numero di camera.



