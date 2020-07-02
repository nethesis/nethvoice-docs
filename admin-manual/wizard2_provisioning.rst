.. _wizard2-provisioning-section:

=========================================
Guida ai parametri di provisioning (beta)
=========================================

.. warning::
    
    Le funzioni descritte in questa sezione sono disponibili in anteprima solo
    ai membri del |product| Quality Team. Fare riferimento a
    :ref:`wizard-section` per la versione stabile.

Le funzioni dei telefoni configurabili mediante provisioning sono raccolte nei
pannelli dell'interfaccia di amminstrazione di |product| e descritti nelle seguenti sezioni.

Non tutti i modelli di telefono dispongono delle medesime funzioni, quindi alcuni 
parametri o interi pannelli potrebbero non essere visualizzati.

In generale lasciare un campo vuoto o selezionare l'opzione ``-`` (segno meno) indicano
il valore ereditato dal contesto con priorità inferiore; la priorità massima è per le impostazioni
del *telefono* e a seguire in ordine decrescente *modello* e *default*.
Fare riferimento a :ref:`provisioning-scopes-priority` per ulteriori informazioni.

.. _panel-softkeys:

Soft key
========

I *soft key* sono tasti del telefono programmabili specifici per
richiamare delle funzioni del telefono.

Qualora il telefono renda disponibili più tasti di quanti ne sono visualizzati
nell'interfaccia di amministrazione di |product|, è presente un pulsante
:guilabel:`Mostra altri` per aggiungerne di ulteriori.

In base al :guilabel:`Tipo` potrebbero doversi valorizzare anche i campi
:guilabel:`Valore` e :guilabel:`Etichetta`, secondo quanto indicato nella
tabella sottostante.

.. _panel-linekeys:

Line key
========

I *line key* sono tasti del telefono programmabili simili ai *soft key* ma
più specifici per la gestione delle chiamate e il monitoraggio degli altri interni.

Qualora il telefono renda disponibili più tasti di quanti ne sono visualizzati
nell'interfaccia di amministrazione di |product|, è presente un pulsante
:guilabel:`Mostra altri` per aggiungerne di ulteriori.

In base al :guilabel:`Tipo` potrebbero doversi valorizzare anche i campi
:guilabel:`Valore` e :guilabel:`Etichetta`, secondo quanto indicato nella
tabella sottostante.

.. _panel-expkeys:

Exp key
=======

Gli *expansion key* sono i tasti programmabili presenti sui *moduli di espansione*,
dispositivi collegabili al telefono che ne aumentano la quantità di tasti disponibili.

Qualora il modulo di espansione renda disponibili più tasti di quanti ne sono visualizzati
nell'interfaccia di amministrazione di |product|, è presente un pulsante
:guilabel:`Mostra altri` per aggiungerne di ulteriori.

Questo tipo di tasti si configura come i :ref:`panel-linekeys`.

.. _panel-display:

Schermo e suoneria
==================

* :guilabel:`Selezione suoneria` Ogni telefono ha alcune suonerie predefinite che possono essere
  selezionate in base al numero progressivo. Laddove supportata è possibile scegliere la suoneria
  personalizzata, che va poi caricata nel controllo descritto di seguito.

* :guilabel:`Gestione suoneria personalizzata` Seleziona un file audio per la suoneria personalizzata
  caricato in precedenza, o ne carica uno nuovo aprendo l'apposito modulo di gestione. Il formato
  audio deve essere compatibile con le specifiche del produttore del telefono.

* :guilabel:`Immagine di sfondo` :guilabel:`Immagine screensaver` Seleziona un file immagine
  rispettivamente per lo sfondo dello schermo del telefono e per lo screensaver, oppure ne carica
  una nuova aprendo l'apposito pannello di gestione. Il formato immagine deve
  essere compatibile con le specifiche del produttore del telefono.

* :guilabel:`Avvio screensaver` Intervallo di tempo dopo il quale viene avviato il salvaschermo.

* :guilabel:`Spegnimento illuminazione` Intervallo di tempo dopo il quale lo schermo abbassa la luminosità
  o spegne la retroilluminazione dello schermo.

* :guilabel:`Luminosità schermo` :guilabel:`Contrasto schermo` Selezionano il livello di luminosità
  e contrasto dello schermo.

.. _panel-preferences:

Preferenze
==========

* :guilabel:`Indirizzo server NTP` Il nome host o l'indirizzo IP del server 
  NTP (Network Time Protocol) per impostare automaticamente e correttamente l'orario del telefono.

* :guilabel:`Pianificazione del provisioning` Selezionando **Solo all'avvio** i telefoni
  rinnovano la propria configurazione dopo l'accensione o il riavvio. Invece Selezionando
  **Ogni giorno** i telefoni rinnovano la configurazione in maniera autonoma ad un orario
  casuale della notte. Vedere anche :ref:`provisioning2-aggiornamenti-automatici`.

* :guilabel:`Modalità di trasferimento per i line key` Specifica il modo in cui i line key 
  trasferiscono la chiamata in corso ad un altro interno.

  - **Nuova chiamata** avvia una nuova chiamata verso l'interno configurato sul line key, 
    ponendo in attesa quella corrente.

  - **Consultativo** pone sempre in attesa la chiamata corrente e il completamento del trasferimento
    può avvenire mentre l'interno configurato sul line key squilla o anche dopo la risposta.

  - **Senza conferma/Cieco** trasferisce immediatamente la chiamata corrente all'interno configurato.
  
* :guilabel:`Lingua telefono` Lingua utilizzata dallo schermo del telefono e dalla sua interfaccia web.
 
* :guilabel:`Fuso orario` Imposta il fuso orario del telefono, necessario il passaggio all'ora legale.

* :guilabel:`Toni di chiamata` Sono specifici di ogni nazione e indicano lo stato della chiamata mediante
  un segnale acustico: squillo libero, occupato, riagganciato...

* :guilabel:`Formato ora` :guilabel:`Formato data` Scelta del formato ora/data mostrato
  sul display del telefono.

* :guilabel:`Firmware` Caricamento e selezione di una nuova versione del firmware del telefono. 
  Vedere anche :ref:`provisioning2-firmware-upgrade`.


.. _panel-phonebook:

Rubrica LDAP
============

Le prime due voci della scelta :guilabel:`Tipo di rubrica` non consentono ulteriori modifiche. I telefoni 
utilizzeranno la rubrica centralizzata di |product| i cui parametri di configurazione sono fissi e non modificabili.
Selezionando invece :guilabel:`Rubrica personalizzata` è possibile modificare i restanti campi di questo pannello,
per collegare i telefoni ad un server LDAP di terze parti.

* :guilabel:`Indirizzo server` Nome host o indirizzo IP del server LDAP

* :guilabel:`Numero porta` Porta TCP utilizzata dal server LDAP

* :guilabel:`Nome utente` :guilabel:`Password` Credenziali di autenticazione per il servizio LDAP. Il nome utente potrebbe
  essere indicato come Distinguished Name (DN) LDAP o in altro formato, a seconda dei requisiti del server LDAP.

* :guilabel:`Crittografia` Protegge la connessione con TLS o con STARTTLS. *Attenzione!* Alcuni telefoni non supportano la crittografia ed
  è necessario selezionare **Nessuna**.

* :guilabel:`Base di ricerca (DN)` Limita l'accesso al ramo del database LDAP specificato come base. Di solito la base di ricerca 
  è obbligatoria.

* :guilabel:`Filtro di ricerca per nome contatto` :guilabel:`Filtro di ricerca per numero telefonico` I filtri di ricerca LDAP vanno
  specificati con la sintassi definita da RFC-4515 e successivi. Il carattere ``%`` (segno di percentuale) può essere utilizzato
  come segnaposto che il telefono sostituisce con il numero digitato.

* :guilabel:`Attributi per nome contatto` Separati da spazio vanno elencati i nomi degli attributi LDAP
  che possono contenere il nome del contatto.

* :guilabel:`Formato di visualizzazione nome` I nomi degli attributi preceduti dal carattere
  ``%`` (segno di percentuale) possono essere composti a formare il modello con cui il nome viene visualizzato 
  sullo schermo del telefono.

* :guilabel:`Attributo per numero di telefono principale` :guilabel:`Attributo per numero di cellulare` 
  :guilabel:`Attributo per altro numero di telefono` Questi tre campi contengono nomi di attributi LDAP per i rispettivi
  numeri di telefono.

.. _panel-network:

Rete
====

I telefoni utilizzano il protocollo DHCP per ricevere la configurazione di rete: 
IP, maschera di rete, DNS, gateway. In alcuni casi viene utilizzato DHCP anche per
ottenere l'URL di provisioning (fare riferimento a :ref:`provisioning-methods`).

Sono invece configurabili in questo pannello i seguenti parametri:

* :guilabel:`Identificativo VLAN (VID)` Indicando un numero compreso tra 1 e 4094 il 
  telefono aggiungerà la marcatura VLAN ai pacchetti generati dal telefono stesso,
  secondo lo standard IEEE 802.1Q.

* :guilabel:`Identificativo VLAN per porta PC` Indicando un numero compreso tra 1 e 4094 il telefono
  aggiungerà la marcatura VLAN ai pacchetti provenienti dalla porta PC (o porta dati), secondo
  lo standard IEEE 802.1Q.

Nei campi VLAN il valore "" (stringa vuota), come al solito, considera l'impostazione
a priorità inferiore (di modello o default), mentre lo "0" (zero) corrisponde a "disabilitato".

.. warning::

  Inserendo un identificativo VLAN errato il telefono può diventare irraggiungibile
  