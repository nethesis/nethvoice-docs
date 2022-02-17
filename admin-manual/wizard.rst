.. _wizard-section:

======================================
Wizard prima configurazione (obsoleto)
======================================

.. warning::

   Il nuovo sistema di provisioning basato sul progetto Tancredi è descritto in
   :ref:`wizard2-section`

Il wizard di prima configurazione consente di installare e configurare agevolmente tutte le componenti di un centralino.

Visitando:

- `https://IP_DEL_SERVER/NOME_PRODOTTO`

- `https://IP_DEL_SERVER/freepbx/admin`

è possibile raggiungere l'applicazione web.

Le credenziali per il login sono le seguenti:

`username: admin`

`password: Nethesis,1234`

Modalità utenti per il centralino
=================================
Una volta effettuato il login, se non è ancora stato configurato un account provider sulla macchina, l'interfaccia mostrerà la possibilità di scegliere se installare un account provider LDAP locale o configurarlo manualmente. 

Nel primo caso, non verranno richieste ulteriori configurazioni, mentre nel secondo si verrà rediretti all'interfaccia di |parent_product|, dove sarà possibile configurare il provider degli utenti. 

Se il provider scelto non è locale, non sarà possibile creare gli utenti, che dovranno essere quindi creati manualmente sul provider stesso prima di procedere con la configurazione, con un provider locale invece sarà possibile creare gli utenti direttamente in |product|.

Una volta scelta la modalità, si procede alla configurazione degli utenti.

Interni
=======
Il primo passo nella configurazione di |product| è definire la lista di utenti e l'abbinamento con il loro interno telefonico.

In caso di account provider remoto in questa sezione comparirà l'elenco degli utenti che |parent_product| recupera remotamente.

In caso di account provider locale in questa sezione comparirà invece l'elenco degli utenti l'elenco delgi utenti di |parent_product| e ci sarà la possibilità di crearne direttamente da qui di nuovi scegliendo username e il nome completo.

É possibile ora inserire gli interni relativi per ogni utente:

- Inserire il numero dell'interno (consigliato a partire dal numero 200) nel campo di testo
- Cliccare su Inserisci
- L'utente si evidenzia e una spunta verde compare se tutto è andato a buon fine

Importazione utenti da csv
..........................

Nei centralini che non usano un account provider esterno, è possibile importare gli utenti con un file CSV.

Creare un file di testo, con un utente per riga e il formato 

:: 

  <NOME UTENTE>,<NOME COMPLETO>,[INTERNO],[PASSWORD UTENTE],[CELLULARE],[VOICEMAIL],[INTERNO WEBRTC],[GRUPPI CTI],[PROFILO CTI]

Per esempio:

::

  mario,Mario Rossi
  paolo,Paolo Bianchi,200
  carlo201,Carlo Neri,201,Carlo1@.!
  francesco,Francesco Verdi,202,,33312312343,FALSE,TRUE,Sviluppo|Assistenza|Tecnici,Advanced
  andrea,Andrea Rossi,203,Andrea1234,,TRUE,TRUE,Commerciali,Standard

Cliccare su :guilabel:`Importa` e selezionare il file creato.

Nella finestra che si aprirà, fare click su :guilabel:`Importa` e attendere che gli utenti vengano creati.

Se viene omesso l'interno, verranno creati solo gli utenti.

Se il campo *password* non viene compilato, la password sarà generata casualmente.

É possibile utilizzare la funzione anche per assegnare gli interni ad utenti già creati, ma senza interno assegnato. 

In questo caso, il campo *password* verrà ignorato.

Il tasto esporta consente di scaricare un modello di CSV con gli attuali utenti da modificare per poi importare nuovamente. Le righe precedute da # verranno considerate commenti. I gruppi CTI, una lista separata da pipe `|` verranno creati automaticamente. Il profilo CTI deve essere scelto tra quelli già creati

Fasci
=====
Nella sezione fasci è possibile configurare i gateway per gestire le linee fisiche o creare fascio VoIP specificando le credenziali dei vostri provider

.. _fisiciold:

Fisici
------
Come per i dispositivi, questa sezione scansiona la vostra rete e cerca dei gateway disponibili, una volta individuati è possibile specificare, selezionandone uno, due impostazioni:

- Modello: specificare il modello del gateway
- Impostazioni dinamiche in base al modello:

 - ISDN (Specificare per la linea se è Point-Point or Point-MultiPoint)
 - PRI
 - FXS (Specificare per ogni porta, l'interno da assegnare scegliendo un utente precedentemente configurato)
 - FXO (Specificare direttamente il numero, nel campo di testo)

Una volta salvate le impostazioni è possibile caricare la configurazione sul gateway tramite il bottone "Carica"
Il gateway prende la configurazione e si riavvia, vengono inoltre creati i fasci relativi.

VoIP
----
É possibile creare dei fasci VoIP selezionando uno dei provider supportati, e inserendo le informazioni necessarie.

Premere "Crea" per creare la configurazione relativa per quel fascio VoIP.

Rotte
=====
Nella sezione rotte è possibile configurare le rotte in entrata e in uscita per il vostro centralino

In entrata
----------
Una volta in questa sezione, vi si presenta la lista delle rotte già configurate, con la possibilità di modificarle o eliminarle.

Premendo sul bottone "Crea nuova rotta" si apre una differente applicazione il Visual Plan, che vi consente di creare, modificare e collegare le varie componenti per gestire al meglio il flusso della chiamata su un determinato numero in ingresso.

Premendo il simbolo di spunta nell'applicazione Visual Plan, la configurazione della vostra rotta verrà salvata e da quel momento potrete ricevere chiamate e indirizzare il flusso a seconda della vostra scelta.

In uscita
---------
In questa sezione è presente la lista delle rotte in uscita presenti, la prima volta che questa pagina viene visitata, il wizard vi propone delle rotte in uscita di default con i pattern di chiamate specifici per le diverse lingue.

É possibile inoltre specificare l'ordine con cui usare i fasci, precedentemente creati, e regolare così in maniera personalizzata il percorso delle chiamate in uscita.

Premendo il tasto "Salva" la configurazione viene scritta nel centralino e da quel momento è possibile effettuare chiamate verso l'esterno (avendo opportunamente configurato i fasci negli step precedenti).

.. _telefoni_fisici_supportati:

Dispositivi
-----------
In questa sezione è possibile scansionare la rete del |product| e il wizard troverà in automatico i telefoni presenti, individuando, dove è possibile, marca e modello, mostrando inoltre l'indirizzo IP e il MAC address.

Se di alcuni telefoni non è stato possibile trovare automaticamente il modello, servirsi del menù a tendina per selezionarlo.

Per rieseguire la scansione della rete, premere il pulsante *Scan*

.. _configurazioni:

Configurazioni
==============

Gruppi
------
È possibile creare dei gruppi utente che poi saranno visibili e utilizzabili nelle applicazioni, ad esempio nel |product_cti|

- Cliccare il bottone "Crea nuovo gruppo"
- Specificare un nome e salvare
- Il gruppo comparirà nella lista

Profili
-------
|product| consente di selezionare le funzionalità a cui ogni utente potrà accedere e queste vengono raggruppate in dei profili.

Vengono creati di default 3 profili che contengono diversi livelli di funzionalità.

- Base: funzionalità minime per l'utente
- Standard: funzionalità di gestione classiche per l'utente
- Avanzato: quasi tutte le funzionalità sono consentite, indicato per l'utente avanzato

È possibile creare anche nuovi profili, duplicando uno esistente o creandone di nuovi e specificando le varie funzionalità.

Il profilo serve a stabilire le funzionalità abilitate per ogni utente a cui viene assegnato ed è valido per tutti i dispositivi dell'utente, sia per i telefoni fisici che per il dispositivo web utilizzato dal |product_cti| e la App mobile.

.. note:: Ricordarsi di abilitare sui profili dove necessario l'accesso ai gruppi utente precedentemente creati.

Utenti
------
Lo step finale della sezione :guilabel:`Configurazioni` consente di assegnare ad ogni utente le impostazioni create nei passi precedenti.
La lista degli utenti mostra quelli a cui è stato associato un interno nel primo passaggio. Selezionando un utente è possibile:

- Creare un dispositivo personalizzato per collegare all'utente un apparato telefonico che supporta lo standard SIP non supportato dal provisioning (ad esempio un softphone)
- Associare un telefono di quelli precedentemente configurati (effettuando il provisioning automatico)
- Inserire un numero di cellulare, che potrà essere usato dall'utente per abilitare l'inoltro di chiamata (se abilitato nel suo profilo)
- Abilitare la voicemail
- Abilitare il client WebRTC
- Abilitare l'app Mobile
- Scegliere il profilo da destinare all'utente (uno di quelli definiti allo step 3)
- Scegliere un gruppo a cui far parte (uno di quelli creati allo step 2)

.. warning::

   Le compatibilità dei telefoni e le istruzioni dettagliate di come effettuare il provisioning si trovano in :ref:`provisioning-section`

Applicazioni
============
La sezione "Applicazioni" consente di creare, modificare o eliminare determinate funzionalità del centralino, che nel wizard vengono solo create e configurate, ma che poi vengono utilizzate nel CTI.

Ad esempio le schede cliente, nel wizard, vengono configurate per accedere al database e per mostrare in maniera pratica le informazioni ottenute, ma il reale utilizzo sarà all'interno del CTI, durante le chiamate o durante la ricerca di determinate informazioni.

Schede cliente
--------------

La sezione schede cliente, permette di raggruppare le informazioni presenti su database esterni al centralino e mostrarle in fase di chiamata. Ad esempio, sulla chiamata di un certo cliente, prendere le informazioni sul database relative alle sue fatture o ad eventuali insoluti e valutare ad esempio, se fornire assistenza o meno. Per generare una nuova scheda cliente i passi sono i seguenti

Sorgenti
........

Cliccare sul bottone "Crea nuova sorgente" e compilare il form che si presenta:
- Tipo database: specificare la tipologia di database su cui andare a prendere le informazioni
- Nome database: specificare il nome del database a cui connettersi
- Indirizzo database: specificare l'indirizzo per collegarsi al database (localhost, socket o IP esterni)
- Porta database: specificare un porta del db diversa da quella di default proposta
- Utente database: specificare l'utente usato per connettersi al database
- Password database: specificare la password per collegarsi al database
- Connessione: premere il pulsante "Verifica" per testare che le informazioni inserite siano corrette per la connessione

Premere "Salva" per aggiungere la sorgente database. La sorgente appena creata apparirà tra la lista di quelle disponibili

Template
........

I template sono il fac-simile per le vostre schede cliente. Utilizzano il motore `ejs`, che ha una sintassi *JavaScript-like*, che vi permette di scrivere codice html utilizzando specifiche direttive che potete trovare nel sito https://github.com/tj/ejs.

Cliccare sul bottone "Crea nuovo template" per iniziare il processo di creazione:
- Nome: specificare il nome del template
- Results: contiene l'output della vostra query in formato JSON, utilizzate il campo di testo per effettuare delle prove e vedere come il vostro template HTML risulterà essere con i vostri dati.
- Codice (ejs): in questo campo di testo, inserite il codice del vostro template, che rispetta la sintassi `ejs`, utilizzando i valori sopra indicati (che non sono altro che le colonne di risultato della vostra query)
- Anteprima: combinando i risultati e il codice `ejs` vedrete l'output relativo HTML che sarà la vostra scheda cliente.

Il centralino prevede giù dei template predefiniti con codice HTML già scritto, che potete duplicare e modificare cambiando colore.

Schede
......

Una volta creata la sorgente e il template della vostra scheda, in questa sessione dovrete unire le due informazioni per far si che la scheda venga creata correttamente. Cliccare sul bottone "Crea nuova scheda" e compilare il form:
- Nome: nome della scheda cliente
- Sorgente: specificare la sorgente di database precedentemente creata
- Template: specificare il template da associare a quello precedentemente creato
- Profilo: scegliere il tipo di profilo utente a cui far vedere la scheda cliente che state creando
- Query: inserite la query che vi restituirà le informazioni relative
- Render: premendo il pulsante, la **query** verrà eseguita sulla **sorgente** specificata e i dati verranno inseriti nel **template** selezionato, producendo l'output desiderato.

Premere il tasto "Salva" per salvare la vostra scheda cliente.

.. warning:: Una volta creata la query e la scheda e verificato che il tutto funziona, utilizzare la variabile `$NUMBER` per sostituire i parametri numerici di ricerca delle vostra query.

*Esempio*:

Se la vostra query è di questo tipo:

`select * from phonebook where homephone like '%150' or workphone like '%850' or cellphone like '%150' or fax like '%850'`

dovrà diventare così:

`select * from phonebook where homephone like '%$NUMBER' or workphone like '%$NUMBER' or cellphone like '%$NUMBER' or fax like '%$NUMBER'`

La variabile `$NUMBER` non è altro che il numero chiamante del centralino a cui la scheda cliente fa riferimento per effettuare la raccolta dei dati da mostrare.

Sorgenti video
--------------
In questa sezione è possibile configurare le sorgenti video o telecamere IP. Cliccando sul bottone "Crea nuova sorgente" è possibile compilare un form per la creazione:

- Nome: specificare il nome da dare alla sorgente
- Extension: specificare l'interno relativo alla sorgente video (precedentemente creata nella sezione "Utenti")
- URL: specificare l'URL di collegamento in cui prendere i frame video da mostrare
- Codice d'apertura: inserire il tono DTMF relativo per un eventuale codice d'apertura (se la telecamera è collegata ad un cancello ad esempio)
- Profilo: specificare il profilo da assegnare alla sorgente per filtrare la tipologia di utente che ha accesso alla sorgente video
- Connessione: premere il bottone "Verifica" e verificare che l'URL inserito sia corretto, testando la connessione e ottenendo il frame video relativo.

Una volta completata la compilazione del form premere "Salva" per salvare le informazioni e creare una nuova sorgente video.

URL parametrizzati
------------------

Consentono all'utente finale di poter invocare un URL parametrizzato in corrispondenza della ricezione di una chiamata.
L'URL sarà parametrizzato coi dati del chiamante e potrà essere "aperto" in uno dei seguenti quattro scenari:

1) mai
2) quando la chiamata in ingresso sta squillando
3) quando la chiamata in ingresso è stata risposta
4) cliccando il pulsante apposito nel box di gestione chiamata

Per la creazione di un URL sono necessarie due informazioni:

- l'url stesso
- la scelta di un profilo utente

Tutti gli utenti che hanno quel profilo saranno abilitati all'utilizzo dell'URL appena creato.

.. note::

    1. Ad un profilo può essere associato un solo URL.
    2. Affinché l'URL possa essere invocato è necessario che l'utente finale abbia abilitato la visualizzazione dei popups nel proprio browser !

Gestione Multipla
-----------------

L'applicazione *Gestione Multipla Interni* consente di modificare massivamente gruppi di utenti.

É possibile selezionare gli interni che si desidera modificare utilizzando la lista "Seleziona" o le checkbox accanto agli utenti elencati.

Cliccando poi sul tasto :guilabel:`Modifica`, verrà visualizzata una finestra con le impostazioni che possono essere modificate.

Il contenuto dei campi viene mostrato solo se gli interni selezionati hanno tutti lo stesso valore per quel campo, altrimenti rimane vuoto.

L'icona :guilabel:`lucchetto` chiuso alla destra del campo indica che il campo non verrà modificato.

Per esempio, se gli interni 201 e 202 hanno un valore differente per il gruppo di chiamata, il campo sarà vuoto, ma se il :guilabel:`lucchetto` è chiuso, il valore non verrà sovrascritto.

Se invece si clicca sul :guilabel:`lucchetto` in modo che sia aperto e si salva, il gruppo di chiamata verrà sovrascritto con il valore del campo.

Aggiunta di rubriche esterne
----------------------------

È possibile aggiungere rubriche esterne a quella di |product| per integrarla con contatti aggiuntivi residenti su database esterni.

Per accedere al servizio è sufficiente selezionare il menù :menuselection:`Applicazioni -> Sorgenti rubrica`.

L'integrazione viene eseguita creando una nuova sorgente da cui verranno prelevati i dati da sincronizzare con la rubrica centralizzata (tabella ``phonebook`` del database ``phonebook``) in maniera schedulata.

Per creare una nuova sorgente sono necessari tre passaggi:

1. **Sorgente:** creazione nuova sorgente
2. **Mappa:** configurazione del mapping tra i campi del database sorgente e i campi del database destinatario (rubrica centralizzata ``phonebook.phonebook``)
3. **Impostazioni:** scelta dell'intervallo di sincronizzazione

**1. Sorgente**

Al momento l'integrazione riguarda sorgenti di tipo MySQL e per ognuna di esse è sufficiente inserire:

- *nome rubrica:* un qualsiasi nome significativo univoco che verrà utilizzato per identificare i dati importati nella rubrica centralizzata
- *dati di accesso al db*: tipo database, indirizzo e porta server, utente e password
- *query*: query utilizzata per prelevare i dati da importare nella rubrica centralizzata. Dal valore presente di default, sostituire la parola ``[table]`` con il nome della tabella da utilizzare

Il pulsante "Esegui" consente la visualizzazione dell'anteprima dei dati prelevati dalla sorgente.

**2. Mappa**

In questo passaggio è necessario stabilire la corrispondenza tra i campi del database sorgente e quelli destinatari della rubrica centralizzata.

Per esempio, si potrebbe associare il campo ``phone`` sorgente con quello destinatario ``workphone``.

**3. Impostazioni**

È possibile scegliere l'intervallo di sincronizzazione dei contatti tra:

- 15 minuti
- 30 minuti
- 1 ora
- 6 ore
- 24 ore

Una volta creata la sorgente, è possibile:

- eseguire subito la sincronizzazione tramite il pulsante :guilabel:`Sincronizza`
- abilitare/disabilitare la sincronizzazione

Amministrazione
===============

La sezione "Amministratore" raggruppa le azioni che possono essere fatte dall'amministratore del centralino

Lingue
------

Nel menù Lingue è possibile impostare la lingua di sistema del |product| impostandola come quella di default e installare anche altri pacchetti lingua aggiuntivi.

Impostazioni
------------

La pagina delle Impostazioni permette di gestire diversi aspetti della configurazione.

* :guilabel:`Password`: è possibile cambiare la password dell'utente admin dedicato all'accesso all'interfaccia web di |product|.

* :guilabel:`Impostazioni NAT`: per gestire correttamente il NAT nel protocollo SIP, |product| ha necessità di conoscere l'indirizzo che utilizzerà presentandosi all'esterno e le reti da considerare locali, per le quali non dovrà tenere conto del NAT e delle sue impostazioni: 

  1) Inserire in :guilabel:`Indirizzo Esterno` l'IP pubblico con il quale |product| effettuerà connessioni esterne alla propria rete. 
  2) Inserire in :guilabel:`Reti Locali` tutte le reti in formato CIDR dalle quali |product| si deve aspettare connessioni dirette senza considerare quindi il NAT.

* :guilabel:`Impostazioni Firewall`: il firewall di |product| nella configurazione di partenza non accetta connessioni da reti esterne per il protocollo SIP TLS (porta 5061 tcp e porte da 10000 a 20000 udp). 
  In questa sezione è possibile configurare il firewall per accettare traffico SIP TLS anche da reti non locali abilitando il SIPS esterno.

* :guilabel:`Impostazioni Rubrica`: in questa sezione è possibile abilitare l'esporazione della rubrica di |product| in LDAP per consentire di solito ai telefoni di accedervi in sola lettura. 
  La rubrica può essere pubblicata in LDAP in due modalità (la configurazione data ai telefoni sarà completa di tutti i parametri necessari):

  1) **LDAP**, che comporta una pubblicazione in chiaro e ad accesso anonimo (senza cioè la necessità di credenziali di autenticazione); questa modalità è indicata se tutti i telefoni sono nella stessa rete di |product|
  2) **LDAPS**, che utilizza la crittografia e richiede delle credenziali di autenticazione per accedere; questa modalità è indicata in presenza di telefoni che si collegano a |product| da reti esterne

.. warning:: 

    Per ridurre l'uso di memoria del sistema è consigliato attivare una sola delle precedenti modalità di pubblicazione della rubrica LDAP

Avanzate
--------

La sezione Avanzate consente l'accesso diretto all'interfaccia avanzata di |product|.


Report
------
La sezione "Report" riporta l'elenco completo degli utenti del centralino specificando il loro:

- Interno
- Username
- Nome e Cognome
- Password Voicemail
- Password utente (se l'utente è stato creato da |product|)

É presente anche la possibilità di stampare l'elenco in formato PDF cliccando sul bottone "Stampa report PDF"
