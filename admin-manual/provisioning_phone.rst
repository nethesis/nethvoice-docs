=========================
Provisioning dei telefoni
=========================

Telefoni supportati
===================

SANGOMA 
-------
* S205, S206
* S300, S305
* S400, S405, S406 
* S500, S505
* S700, S705

YEALINK 
-------

* T19(P) E2, T21(P) E2, T23G, T27G, T29G
* T40P/G, T41P/S, T42G/S, T46G/S, T48G/S, T49G
* T53, T54, T56, T57, T58, VP59

SNOM    
----

* D120
* D305, D315, D345, D375, D385
* D710, D712, D715, D717, D725, D735, D745, D765, D785

GIGASET 
-------

* Maxwell basic, Maxwell 2, Maxwell 3
   
FANVIL
------

* X3, X4, X5, X6


Provisioning
============

Cosa significa **Provisioning**?

**Provisioning** è configurare i telefoni in modalità automatica limitando al massimo le operazioni necessarie.

Il **Provisioning** si svolge in diversi passi:

1. Ricerca dei telefoni da configurare
2. Creazione dei file necessari alla configurazione dei telefoni
3. Pubblicazione dei file di configurazione
4. Aggiornamento del firmware dei telefoni
5. Indicare ai telefoni dove e come possono trovare i file di configurazione
6. Riavvio dei telefoni
7. Scambio file tra |product| e i telefoni


Ricerca dei telefoni
--------------------

|product| deve recuperare i MAC address dei telefoni da configurare, il MAC address è alla base del **Provisioning** in quanto strumento univoco di identificazione dei telefoni.

Due modalità possibili:

1. Scansione delle reti locali alla ricerca di apparati telefonici supportati già online come documentato :ref:`qui <telefoni_fisici_supportati>`
2. Scansione del codice a barre del MAC address del telefono tramite l’app :ref:`Scan & Play 14 <app_mobile>` in questo caso il telefono può essere ancora inscatolato

Creazione della configurazione
------------------------------
La configurazione dei telefoni viene creata tramite l’associazione del telefono all’utente nel :ref:`Wizard di configurazione <configurazioni>`.

Ad ogni utente possono essere associati al massimo 8 device telefonici che verranno configurati a partire dall’interno principale associato all’utente e a seguire nella modalità:

* Interno Principale
* 91+Interno Principale
* 92+Interno Principale
* 93+Interno Principale
* \.\.\.\.\.\.\.\.

Pubblicazione della configurazione
----------------------------------

La pubblicazione dei file di configurazione avviene quando viene premuto il pulsante :guilabel:`Configura e Riavvia` nel :ref:`Wizard di configurazione <configurazioni>`.

Aggiornamento firmware
----------------------

Contemporaneamente alla configurazione dei telefoni è possibile anche aggiornare il firmware.

Per farlo è necessario caricare il firmware nella directory :file:`/var/lib/tftpboot/`

Il file deve essere nominato seguendo le specifiche del produttore del telefono, di solito lo schema è **Modello.estensione** 

Ad esempio:  

::

 fw500.rom   per Sangoma 500
 T27P.rom    per Yealink T27P
 D745.bin    per Snom D745
 725.bin     per Snom D725
 maxwell.bin per Gigaset Maxwell Basic/2/3  


I telefoni SNOM richiedono necessariamente il firmware per un corretto avvio del telefono, se non presente il telefono mostrerà un errore a schermo superabile solo con la pressione di un tasto.

I telefoni GIGASET richiedono la creazione di un file ulteriore file oltre al caricamento del firmware, che dovrà essere nominato **firmware.xml** e contenere:

.. code-block:: bash

 <?xml version="1.0" encoding="UTF-8"?>
    <firmware version="1.0" productID="mx3b">
            <file version="VERSIONE" url="tftp://IP PBX/maxwell.bin" flags="FORCE_ACCEPT"/>
 </firmware>

Sostituire VERSIONE con la versione del firmware da caricare, ad esempio 2.24.12, e IP PBX con l'ip del |product|.


Dove e come trovare i file di configurazione
--------------------------------------------

I telefoni necessitano di conoscere dove si trova la configurazione a loro dedicata.

I metodi principali per farlo sono:

* DHCP
.. * Plug & Play(PNP)
* Interfaccia web


DHCP
~~~~

L’opzione 66 (114 per i telefoni Gigaset) del DHCP è quella che viene utilizzata dai telefoni per sapere dove si trova il server in grado di inviare loro la configurazione.

Il DHCP di |product| configura automaticamente questa opzione, quindi se è |product| a dare l’IP al telefono è tutto pronto.

Se invece è un altro server a dare l’IP ai telefoni è necessario configurare l’opzione necessaria con l’IP del |product|.


.. Plug & Play(PNP)
.. ~~~~~~~~~~~~~~~~

.. Il servizio Plug & Play che molti modelli supportano consente ai telefoni di autonomamente cercare in rete un server in grado di configurarli.

.. I telefoni effettuano traffico multicast alla ricerca del server della configurazione, |product| risponde a queste connessioni proponendosi.

.. Data la natura del protocollo, il successo del Plug & Play dipende molto dalla rete in cui viene utilizzato, switch, hub, virtualizzazione possono bloccare le richieste.


Interfaccia Web
~~~~~~~~~~~~~~~

Come ultima possibilità, è possibile collegarsi all’interfaccia web del telefono e indicare dove il telefono deve collegarsi per ottenere la configurazione.

Ricordarsi di disattivare le modalità automatiche se non utilizzate, DHCP e PNP.


Riavvio dei telefoni
--------------------

Una volta creata la configurazione e stabilito che il telefono saprà dove collegarsi per recuperarla, è ovviamente necessario riavviare il telefono se già online.

Per riavviarlo utilizzare la funzionalità nel :ref:`Wizard di configurazione <configurazioni>`.


Scambio file
------------

|product| e i telefoni supportati per lo scambio dei files di configurazione ed eventualmente del firmware utilizzano il protocollo **TFTP** sulla porta 69 UDP


Template
========

Qual è la configurazione che viene creata dal Wizard per i telefoni?

Viene utilizzato un template di configurazione che va ad impostare i parametri per adattarli al meglio all’utilizzo del telefono con |product|.

Tutti gli aspetti generici e necessari vengono configurati, da quelli basici (interno, password,..) a quelli funzionali (rubrica LDAP, function keys, soft keys,...)


Modifica Template
=================

Se si vuole modificare o personalizzare le impostazioni di telefoni configurati tramite il provisioning, NON bisogna intervenire sull'interfaccia dei singoli telefoni.

Infatti, ad ogni riavvio del telefono, quelle impostazioni non verranno mantenute, e il telefono riprenderà le configurazioni di default del provisioning.

Bisogna invece intervenire direttamente sull'interfaccia avanzata di |product|, modificando i template del provisioning. 

I valori modificabili sono:

* Lingua                                                         
* Fuso orario
* Formato data/ora                                        
* Toni
* Password utente admin                              
* Avviso di chiamata
* Suoneria                                                     
* Modalità di trasferimento
* Rubrica LDAP                                             
* VLAN
* Soft keys (Tasti del telefono sotto lo schermo)                                                    
* Line keys (Tasti linea)
* Exp keys  (Tasti linea dei moduli di espansione)                                                                                                                 
* Screen Saver e Sfondo (Sangoma, Yealink)

Le possibilità sono due:

1. Personalizzare singolo telefono

2. Personalizzare singolo modello (tutti i Sangoma S500 ad esempio)


Personalizzare singolo telefono
-------------------------------

Può emergere l’esigenza di cambiare la configurazione di un singolo telefono, ad esempio per utilizzare i tasti BLF, o variare una configurazione di default per un’esigenza particolare, ad esempio disattivare l’avviso di chiamata.

Queste operazioni possono essere effettuate nell’interfaccia avanzata di |product|, ma lavoreremo per integrare queste funzionalità direttamente nel Wizard.

Nel menù scegliere :guilabel:`Connettività -> OSS Endpoint Template Manager`.

In questa parte si trovano tutte le configurazioni create dal provisioning di |product|.

La chiave per individuare il telefono da modificare è il **MAC address**.

Entrando in modifica del telefono scelto, vengono mostrati i parametri che è possibile variare.

Dopo aver salvato i cambiamenti, per pubblicare la configurazione modificata è necessario applicare i cambiamenti.

Rimane il riavvio del dispositivo per consentire al telefono di recuperare la nuova configurazione, da effettuare con le modalità solite nel :ref:`Wizard di configurazione <configurazioni>` o da :guilabel:`Connettività -> OSS Endpoint Device List`.


Personalizzare singolo modello
------------------------------

Se l’esigenza invece quella di modificare la configurazione non di un singolo telefono ma quella di tutti i telefoni dello stesso modello, ad esempio tutti i telefoni Sangoma 500, non agiremo su una configurazione legata ad un MAC address ma dovremo creare un template ad hoc. 

Queste operazioni possono essere effettuate nell’interfaccia avanzata di |product|.

Nel menù scegliere :guilabel:`Connettività -> OSS Endpoint Template Manager`.

Cliccare in :guilabel:`Aggiungi Nuovo Template`.

Indicare il template che verrà utilizzato come base per la nuova configurazione.

Variare i parametri come si desidera per i telefoni.

Dopo aver creato un nuovo template per un modello specifico di telefono, è necessario segnalare a |product| per quali dei telefoni che sono stati già configurati utilizzarlo in sostituzione di quello standard.

Nel menù scegliere :guilabel:`Connettività -> OSS Endpoint Device List`.

Se si desidera utilizzare il template creato per diversi telefoni del modello scelto ma non per la loro totalità:

* selezionare il primo telefono a cui applicare il template appena creato
* fare clic su :guilabel:`Edit` (il simbolo della matita): il telefono apparirà nella parte alta della pagina, nella sezione Edit device
* nella voce Template, selezionare il template appena creato
* salvare il template
* applicare i cambiamenti
* riavviare il telefono (al riavvio, il telefono verrà configurato sulla base del template appena creato) con le modalità solite nel :ref:`Wizard di configurazione <configurazioni>` o sfruttando le funzionalità nelle opzioni globali a fondo pagina
* ripetere i passi per ogni telefono


Se invece si desidera variare la totalità dei telefoni del modello per cui è stato creato il template personalizzato è sufficiente utilizzare le opzioni globali a fondo pagina.

