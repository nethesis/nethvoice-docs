===========================
Note di rilascio |version|
===========================

|product| release |version|

Questa release è basata su `Asterisk 18 <https://wiki.asterisk.org/wiki/display/AST/New+in+18>`_
e `FreePBX 14 <https://www.freepbx.org/freepbx-14-release-candidate/>`_:


Cambiamenti principali al 2023-06-14
====================================

* |product| Provisioning: aggiunto il supporto per i telefoni Fanvil serie V6X e X300X
* Corretto comporatamento rubrica LDAP per telefoni Fanvil che non gestivano più di 64 caratteri
* Report |product|: corretto calcolo posizione minima, massima, media in coda

Cambiamenti principali al 2023-03-05
====================================

* Aggiunta integrazione Google Speech to text con le caselle vocali
* Aggiunta integrazione con API custom per chiamate in ingresso
* Aggiornato Janus alla versione 0.12.3
* Aggiunto supporto Gateway FXS Grandstream
* Aggiunto NethPhone X210

Cambiamenti principali al 2022-05-30
====================================

* Aggiornato Asterisk alla versione 18
* Apertura URL parametrizzata anche da |product_nethifier|
* Aggiunto monitoraggio tempi di richiamata per Report e Qmanager 

Cambiamenti principali al 2022-03-08
====================================
* Nuova Presence per |product_cti|
* Supporto cuffie USB per |product_nethifier| 

Cambiamenti principali al 2022-02-21
====================================

* Refactor Chiamate Rapide |product_cti|
* Aggiunto controllo rotte in uscita nei profili di |product|
* Variato ordine sezioni wizard |product|

Cambiamenti principali al 2021-10-22
====================================

* Richiama su Occupato: la funzionalità consente di prenotare la chiamata con un altro utente che è impegnato al telefono.
* Infinite Scrolling in alcune sezioni dell'interfaccia web di |product|

Cambiamenti principali al 2021-07-24
====================================

* Nuova visualizzazione dello stato dei trunk (Dashboard e sezione Fasci VoIP) con vista su registrazione e stato provider su |product|
* Gestione Multipla Interni non cambia più il contesto ma il profilo (cambiando il profilo si cambia automaticamente anche il contesto)
* Migliorato il tono di disconnessione per i Patton analogici
* Corretto il pickup da tasto BLF per i telefoni Gigaset Maxwell
* Corretta la visualizzazione dati nella rubrica |product_cti| in modalità azienda
* Corretto il funzionamento del trasferimento di chiamata utilizzando il pannello operatore in |product_cti|
* Corretto il problema del conflitto di registrazione tra Janus e App Mobile in |product_cti|
* Corretto la visualizzazione del tempo di conversazione nel pannello operatore di |product_cti|
* Aggiunto nuovo indice alla tabella della rubrica di |product_cti| per migliorarne l’efficienza

Cambiamenti principali al 2021-06-21
====================================

* I profili diventano anche dei contesti Asterisk per tutti i dispositivi degli utenti.
* Creazione dei Trunk Voip usando la modalità PJSIP invece delle precedente SIP, solo i nuovi trunk saranno configurati in PJSIP 
* Codici Login/Logout e Pausa (di default \*45 e \*46) generalizzati per l’interno principale: usando il codice da un qualsiasi dispositivo sarà sempre riferito all’interno principale
* Aggiunta opzione per URL parametrizzato solo da chiamate provenienti dalle code
* Sistemazione delle traduzioni nell’interfaccia di |product|
* Corretta la configurazione del modulo di espansione dei telefoni Yealink

Cambiamenti principali al 2021-06-24
====================================

* Correzione del problema dell’aggiornamento del nome/numero chiamante in caso di trasferimento semi consultativo e trasferimento cieco ad una coda.
* Risoluzione del malfunzionamento del pickup diretto per chiamate che suonano in un gruppo di chiamata su interni in contesti diversi da quello di default.

Cambiamenti principali al 2021-04-23
====================================

Nuova funzionalità Videoconferenza
È ora possibile avviare delle riunioni direttamente da |product_cti|.

Al momento le modalità supportate sono:

* nuova riunione e link di invito via email
* avvio di una nuova riunione


Cambiamenti principali al 2021-03-26
====================================

* Rilasciata Rubrica |product| per nuova App Mobile |product_cti|


Cambiamenti principali al 2021-03-20
====================================

Rilasciati i Nuovi Report di |product|.

Vedi qui :ref:`Report <report>`

Cambiamenti principali al 2020-11-30
====================================

Rilasciata la gestione dei file CSV come nuova sorgente per i contatti della rubrica Centralizzata e di |product|.

Il modulo gestisce sia l’uso di uno specifico file CSV che il collegamento ad un file raggiungibile in HTTP/HTTPS che quindi può variare nel tempo, ad esempio esportazione periodica dei contatti in formato CSV di un software gestionale o CRM.

Il formato CSV è quello standard:

* il file CSV deve essere in codifica UTF-8
* intestazioni nella prima riga
* campi separati da virgola
* doppie virgolette "" come delimitatori del testo, obbligatori nel caso sia presente una virgola o uno spazio

Vedi qui :ref:`Sorgenti Rubrica <external-phonebook>`

Cambiamenti principali al 2020-07-06
====================================

Le nuove installazioni di |product| utilizzano il
:ref:`nuovo sistema di provisioning <provisioning-phone2-section>` basato sul
progetto Tancredi. Le differenze rispetto all'interfaccia di amministrazione precedente
(Wizard di prima configurazione) riguardano le seguenti pagine:

* :guilabel:`Dispositivi` è stata spostata in una sezione del menù a sé stante,
  composta dalle voci :guilabel:`Telefoni` e :guilabel:`Modelli`.
* :guilabel:`Configurazioni` è stata spostata in una sezione del menù a sé
  stante.
* :guilabel:`Gestione multipla telefoni` è stata aggiunta sotto la sezione
  :ref:`Applicazioni<wizard2-telefoni-multipli>`.

Le installazioni di |product| esistenti possono migrare al nuovo sistema di provisioning come
spiegato in :ref:`provisioning-migration-section`.

Cambiamenti principali al 2020-03-18
====================================

* Nuova gestione del Provisioning: :ref:`provisioning-phone2-section`, :ref:`wizard2-section`
* Gestione tasti linea per l'utente di |product_cti|
* Rilasciata nuova App Mobile |product_cti|


Cambiamenti principali al 2019-09-15
====================================

* Nuova App Posto Operatore avanzato per |product_cti|
* Qmanager Dashboard
* Condivione desktop per |product_cti|
* Statistiche personali agenti code in |product_cti|
* Qmanager chiamate perse
* Gestione funzionalità rimozione echo dei browser in |product_cti| 


Cambiamenti principali al 2019-01-14
====================================

* Migrazione da |product| 11 a |product| 14 maggiori approfondimenti :ref:`qui <migrazione-ref-label>`
* Nuova Dashboard 
* Nuovo |product_cti| QManager
* |product| Wizard: eliminata la distinzione tra “Legacy” e “Unified Communication”: ora gli utenti possono essere sempre creati in caso di provider utenti locale
* |product| Provisioning: aggiunto il supporto per i telefoni Fanvil X1, X3S, X4, X5S, X6, rimane solo da risolvere un problema sul clicktocall automatico da |product_cti| che genera una chiamata persa
* Report Code: aggiunta la visualizzazione per chiamata con esito e correzioni varie
* |product_cti|: l’utente non vede più i servizi per i quali non possiede il relativo permesso
* |product_cti|: deregistrazione del client Softphone WebRTC quando l’utente sceglie un altro dispositivo
* |product_cti|: risoluzione in rubrica anche delle chiamate interne
* |product_cti|: possibilità di aggiungere nuovi campi durante la creazione di nuovi contatti in rubrica (note, titolo…)


Cambiamenti principali al 2018-06-18
====================================

* Nuova Conferenza |product_cti|
* URL Parametrizzato
* Gestione Numero in uscita dal modulo bulk nel Wizard
* Implementazioni all’import csv nella sezione Utenti del Wizard
* Login/logout code e DND automatici
* |product| Rapid Code
* Utilizzo certificato di |parent_product| per |product|
* Import/export Speed Dial |product_cti|


Cambiamenti principali al 2017-08-31
====================================

Cambiamenti significativi dalla release 11:

* Wizard per la configurazione
* Nuovo |product_cti| più intuitivo e con supporto completo a WebRTC
* |product_cti|  mobile app per IOS e Android rinnovata
* |product| Scan & Play mobile app rinnovata

Aggiornamento
=============

É possibile seguire la procedura di migrazione dalla versione 11 come descritto :ref:`qui <migrazione-ref-label>`.
