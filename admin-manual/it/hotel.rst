===============
|product_hotel|
===============

|product_hotel| è un modulo di |product| che permette di gestire degli interni opportunamente configurati come camere di un hotel.

Caratteristiche principali:
- Check-in/Check-out camere
- Sveglia
- Sveglia di gruppo
- Report chiamate
- Personalizzazione Tariffe
- Numeri brevi
- Storico chiamate
- Abilitazione/Disabilitazione chiamate fra camere


Configurazione |product|
========================

Tutti gli interni che fanno parte del contesto **camere** entrano a far parte della gestione |product_hotel|.

E' possibile trasformare un interno in camera modificando il contesto direttamente dai dettagli dell'interno, oppure attraverso il modulo **Gestione camere** nel pannello di configurazione di |product|.


Come configurare il centralino 
==============================
Consigliamo di configurare il centralino in questo modo:
- tutti gli interni delle camere devono essere aggiunti al contesto camere sul pannello di gestione del centralino in Gestione Camere
- gli interni di servizio, come ad esempio la reception, non devono essere aggiunti al contesto camere e devono essere configurati con interni standard, seguendo la normale politica dell'hotel. Ad esempio se le camere avranno come range di interni dal 201 al 299, l'interno della reception dovrà essere sempre a 3 cifre, ad esempio 200 o 300. Per consentire alle camere di chiamare la reception bisognerà configurare un numero breve, invece gli interni di servizio tra di loro si dovranno chiamare direttamente.
- è consigliata la creazione di due rotte in uscita sul centralino, la prima senza prefisso **limitata agli interni di servizio** per farli chiamare all'esterno numeri di 5 o più cifre, la seconda con il prefisso scelto nelle opzioni del |product_hotel| per far chiamare le camere (**ATTENZIONE l'ordine è IMPORTANTE**). Un unico accorgimento bisogna ricordarsi, per chiamate dagli interni di servizio, nel caso di corrispondenza tra numeri di emergenza e numeri delle camere (112,113 etc..), di utilizzare per chiamare i numeri di emergenza il prefisso come se si fosse una camera. 
- è possibile utilizzare un unica rotta in uscita con prefisso, sia per le camere che per gli interni di servizio, in questo caso però ad esempio dal telefono della reception non si potrà richiamare direttamente i numeri delle chiamate perse sul telefono per l'assenza del prefisso in questi ultimi.

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
=======

La sveglia può essere programmata una tantum oppure reiterata su più giorni.
Ogni cliente può configurare la sveglia della propria camera componendo il numero ::

 977

Gruppi
======

E' possibile raggruppare più camere in un unico gruppo. Questo consente di configurare la sveglia su una singola camera e poi estendere la configurazione a tutte le camere appartenenti al gruppo.


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
- Configurazione del prefisso per effettuare chiamate esterne
- Formato interni
- Abilitazione/disabilitazione delle chiamate fra camere
- Abilitazione/disabilitazione delle chiamate fra camere che non hanno eseguito il check-in
- Interno da contattare per allarmi sveglia non risposta
- Abilitare il codice per la pulizia camere


Numeri Brevi
============

La sezione Numeri Brevi consente di specificare delle scorciatoie per chiamare interni predefiniti, ad esempio 9 per contattare la reception. E' possibile associare ad un numero breve uno dei gruppi temporali caricati nell'interfaccia di gestione del centralino |product|. Questo consente di configurare le due destinazioni per la chiamata, se la condizione temporale viene rispettata in Destinazione, se non lo è in Altrimenti.


Storico
=======

Qualora sia necessario consultare uno storico di tutte le chiamate effettuate dalle camere è possibile utilizzare la sezione **Storico**. Lo storico delle chiamate è filtrabile per data e numero di camera.



Tono di chiamata alla digitazione del prefisso
----------------------------------------------

|product| non crea un tono di chiamata automaticamente con la digitazione del solo prefisso, ma aspetta l'intera digitazione del numero da chiamare.

Si può modificare questo comportamento con una piccola personalizzazione.

E' necessario creare un Template per il file::

  /etc/asterisk/extensions_nethesis.conf

che aggiunge il tono di chiamata.

Creare la directory ::

  mkdir -p /etc/e-smith/templates-custom/etc/asterisk/extensions_nethesis.conf

Creare il file ::

  /etc/e-smith/templates-custom/etc/asterisk/extensions_nethesis.conf/20nethhotel
 
inserendoci il seguente contenuto e sostituendo **XXX** con il prefisso impostato nell'interfaccia di |product_hotel| ::

 ;#------------------------------------------------------------
 ;# DO NOT MODIFY THIS FILE! It is updated automatically by the
 ;# SME Server software. Instead, modify the source template in
 ;# an /etc/e-smith/templates-custom directory. For more
 ;# information, see http://www.e-smith.org/custom/
 ;#
 ;# copyright (C) 1999-2003 Mitel Networks Corporation
 ;#------------------------------------------------------------
    
 [camere]
 exten => XXX,1,Noop(Chiamata Esterna)
 exten => XXX,n,Set(TIMEOUT(digit)=5)
 exten => XXX,n,Set(TIMEOUT(response)=10)
 exten => XXX,n,DISA(no-password,camere-disa,$\{CALLERID(number)\})
 exten => _[*#0-9]!,1,agi(camere.php,$\{CALLERID(number)\},$\{EXTEN\})
 exten => _[*#0-9]!,n,Set(CHANNEL(language)=it)
 exten => _[*#0-9]!,n(chiama),Goto(from-internal,$\{toCall\},1)
 exten => _[*#0-9]!,n,Macro(hangupcall)
 exten => _[*#0-9]!,n(chiudi),playback(alarm/contattare-reception)
 exten => _[*#0-9]!,n,Macro(hangupcall)
 exten => h,1,Macro(hangupcall)
    
 [camere-disa]
 exten => _[*#0-9].,1,Set(NETH_HOTEL_EXTEN=XXX$\{EXTEN\})
 exten => _[*#0-9].,n,Noop($\{NETH_HOTEL_EXTEN\})
 exten => _[*#0-9].,n,agi(camere.php,$\{CALLERID(number)\},$\{NETH_HOTEL_EXTEN\})
 exten => _[*#0-9].,n,Set(CHANNEL(language)=it)
 exten => _[*#0-9].,n(chiama),Goto(from-internal,$\{toCall\},1)
 exten => _[*#0-9].,n,Macro(hangupcall)
 exten => _[*#0-9].,n(chiudi),playback(alarm/contattare-reception)
 exten => _[*#0-9].,n,Macro(hangupcall)
 exten => h,1,Macro(hangupcall)
   
 [sveglia]
 exten => s,1,Noop(Sveglia)
 exten => s,n,playback(beep)
 exten => s,n,playback(alarm/sonoleore)
 exten => s,n,Set(CHANNEL(language)=it)
 exten => s,n,SayUnixTime(,,R)
 exten => s,n,playback(minutes)
 exten => s,n,MusicOnHold(sveglia)
 exten => s,n,Noop(fine) 
   
 exten => failed,1,Noop(Chiamata non risposta - ALLARME)
 exten => failed,n,AGI(svegliafallita.php,$\{CAMERA\},$\{ALARM\},$\{RECEPTION\})
 exten => failed,n,hangup()
   
 [allarmesveglia]
 exten => s,1,Noop(AllarmeSveglia)
 exten => s,n,playback(alarm/sveglianonrisposta)
 exten => s,n,playback(alarm/camera)
 exten => s,n,Set(CHANNEL(language)=it)
 exten => s,n,SayDigits($\{CAMERA\})
 exten => s,n,playback(hours)
 exten => s,n,SayUnixTime($\{ALARM\},,R)
 exten => s,n,playback(minutes)
 exten => s,n,MusicOnHold(sveglia) 
 exten => s,n,Noop(fine)
     

Dopo aver salvato il file appena creato dare i comandi ::

 expand-template /etc/asterisk/extensions_nethesis.conf
 asterisk -x "reload"

.. note:: Configurare il timeout di digitazione sui vari telefoni utilizzati dalle camere del |product_hotel| a valori bassi per facilitare il comportamento voluto


FIAS
====

grazie al protocollo FIAS, il neth-hotel può condividere col gestionale alberghiero lo stato delle camere, l'importo delle chiamate e le sveglie. È quindi possibile, per esempio, abilitare la sveglia di NethHotel dal gestionale o avere un feedback sul gestionale della sveglia che è stata abilitata.
Le informazioni comunicate sono: 
* Checkin e checkout delle camera
* Pulizia della camera
* Sveglia e cancellazione sveglia
* Importo delle chiamate effettuate 

Per abilitare il protocollo fias, installare il pacchetto neth-hotel-fias:: 
 
  yum install neth-hotel-fias

Configurare l'indirizzo del PMS (nell'esempio, il PMS è all'indirizzo 192.168.122.12)::
 
  config setprop fias host 192.168.122.12

Configurare la porta del PMS (nell'esempio, il PMS ha un servizio che gira alla porta 5010)::
 
  config setprop fias port 5010

Per applicare le modifiche, lanciare il comando::

  signal-event neth-hotel-fias-update

Per abilitare la comunicazion dell'importo delle chiamate effettuate dalla camera::

  config setprop nethcti-server CdrScript /var/lib/fias/cdr.php
  signal-event nethcti-server-update

Altre impostazioni
------------------

Unità di misura delle tariffe del cdr. 100 => €, 10 => 0.1€, 1 => 0.01€. Il dfault è 100, cambiare l'unità se il PMS si aspetta l'importo in centesimi o decimi di euro.::

  config setprop fias cdrAmountUnits 100

Lunghezza degli interni. È usata per dal software per analizzare le chiamate. Il default è 4, che è adeguato anceh per interni a 3 cifre. se gli interni hanno 5 o più cifre, aumentare il valore.::

  config setprop fias cdrExtensionLength 4

Interni aggiuntivi. Configurare qui eventuali numeri che devono essere trattati come interni anche se dalla lunghezza possono essere scambiati per numeri esterni, separati da virgola. Riportare i numeri come appiono nel campo dst del cdr.::

  config setprop fias cdrExternalExtensions "02313542254,anonymous":

numeri esterni aggiuntivi. Configurare qui eventuali numeri che devono essere trattati come esterni anche se dalla lunghezza possono essere scambiati per numeri interni, separati da virgola. Riportare i numeri come appiono nel campo dst del cdr.::

  config setprop fias cdrInternalExtensions "123,118,113"

Aggiungere pattern (regular expression) per considerare un insieme di numeri come esterni o interni::

  config setprop fias cdrExternalPatterns

o::

  config setprop fias cdrInternalPatterns

Modificare la verbosità del log. Il default è 1. Il file di log è /var/log/fias e alla verbosità di default registra tutti i messaggi scambiati tra PMS e nethhotel::

  config setprop fias logLevel 3

Dopo aver modificato queste variabili rendere sempre effettivi i cambiamenti lanciando l'evento neth-hotel-fias-update::

  signal-event neth-hotel-fias-update


