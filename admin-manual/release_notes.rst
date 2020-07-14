===========================
Note di rilascio |version|
===========================

|product| release |version|

Questa release è basata su `Asterisk 13 <https://wiki.asterisk.org/wiki/display/AST/New+in+13>`_
e `FreePBX 14 <https://www.freepbx.org/freepbx-14-release-candidate/>`_:

Cambiamenti principali al 2020-07-06
=====================================

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
