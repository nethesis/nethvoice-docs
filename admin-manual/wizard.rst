===========================
Wizard prima configurazione
===========================

Il wizard di prima configurazione consente di installare e configurare agevolmente tutte le componenti di un centralino.

Visitando:

- `https://IP_DEL_SERVER/NOME_PRODOTTO`

- `https://IP_DEL_SERVER/freepbx/admin`

è possibile raggiungere l'applicazione web.

Le credenziali per il login sono le seguenti:

`username: admin`

`password: Nethesis,1234`

Modalità centralino
===================
Una volta effettuato il login, vi viene subito proposto di scegliere che tipologia di centralino intendete installare:

- *Legacy*: il centralino diventa anche la base per creare i vostri utenti, quindi al vostro server verrà installata una base LDAP su cui creare i vostri utenti
- *Unified*: il centralino utilizza la base utenti già presente nel vostro server (LDAP o Active Directory)

Una volta scelta la modalità, si procede alla configurazione degli utenti

Utenti
======
Una volta scelta la modalità del centralino, vedrete una lista vuota (nel caso di Legacy) o la lista degli utenti già presenti nel server (nel caso di Unified).

Se siete in modalità Legacy create il vostro primo utente, scegliendo un username e il nome completo.


Interni
-------
E' possibile ora inserire gli interni relativi per ogni utente:

- Inserire il numero dell'interno (consigliato a partire dal numero 200) nel campo di testo
- Cliccare su Inserisci
- L'utente si evidenzia e una spunta verde compare se tutto è andato a buon fine

Importazione utenti da csv
..........................

Nei centralini che non usano un account provider esterno, è possibile importare gli utenti con un file CSV.

Creare un file di testo, con un utente per riga e il formato 

:: 

  <NOME UTENTE>,<NOME COMPLETO>,[INTERNO],[PASSWORD],[CELLULARE],[VOICEMAIL],[INTERNO WEBRTC],[GRUPPI CTI],[PROFILO CTI]

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

E' possibile utilizzare la funzione anche per assegnare gli interni ad utenti già creati, ma senza interno assegnato. 

In questo caso, il campo *password* verrà ignorato.

Il tasto esporta consente di scaricare un modello di CSV con gli attuali utenti da modificare per poi importare nuovamente. Le righe precedute da # verranno considerate commenti. I gruppi CTI, una lista separata da pipe `|` verranno creati automaticamente. Il profilo CTI deve essere scelto tra quelli già creati

Gruppi
------
E' possibile creare dei gruppi utente che poi saranno visibili e utilizzabili nelle applicazioni, come ad esempio nel |product_cti| 

- Cliccare il bottone "Crea nuovo gruppo"
- Specificare un nome e salvare
- Il gruppo compare tra la lista

Profili
-------
Il centralino prevede di specificare determinate funzionalità per ogni utente e queste funzionalità vengono raggruppate in dei profili.

Con l'installazione, vengono creati di default 4 profili che contengono l'abilitazione o meno a certe funzionalità.

- Base: funzionalità minime per l'utente
- Standard: funzionalità di gestione classiche per l'utente
- Avanzato: quasi tutte le funzionalità sono sbloccate, per l'utente Avanzato
- Tutto: ogni funzionalità presente è abilitata, utilizzata per gli utenti amministratori

E' possibile creare anche nuovi profili, duplicando uno esistente o creandone di nuovi e specificando le varie funzionalità

.. note:: Ricordarsi di abilitare sui profili dove necessario l'accesso ai gruppi utente precedentemente creati.

.. _telefoni_fisici_supportati:

Dispositivi
-----------
In questa sezione è possibile scansionare la propria rete e il wizard troverà in automatico i telefoni che sono collegati alla vostra rete, individuando, dove è possibile, marco e modello e vi fornisce inoltre l'indirizzo IP e il MAC address.

Se in alcuni telefoni non è stato possibile trovare automaticamente il modello, servirsi del menù a tendina per specificarlo.

Per rieseguire la scansione della rete, premere il pulsante *Scan*

.. _configurazioni:

Configurazioni
--------------
Lo step finale della sezione Utenti, prevede di raggruppare tutte le impostazioni create e definite nei passi precedenti.
La lista degli utenti mostra quelli a cui è stato associato un interno nel primo step. Selezionando un utente è possibile:

- Creare un dispositivo personalizzato per collegare all'utente un apparato telefonico non supportato (ad esempio softphone)
- Associare un telefono di quelli precedentemente configurati (effettuando il provisioning automatico)
- Inserire un numero di cellulare
- Abilitare la voicemail
- Abilitare il client WebRTC
- Scegliere il profilo da destinare all'utente (uno di quelli definiti allo step 3)
- Scegliere un gruppo a cui far parte (uno di quelli creati allo step 2)

Fasci
=====
Nella sezione fasci è possibile configurare i gateway per gestire le linee fisiche o creare fascio VoIP specificando le credenziali dei vostri provider

.. _fisici:

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
E' possibile creare dei fasci VoIP selezionando uno dei provider supportati, e inserendo le informazioni necessarie.

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

E' possibile inoltre specificare l'ordine con cui usare i fasci, precedentemente creati, e regolare così in maniera personalizzata il percorso delle chiamate in uscita.

Premendo il tasto "Salva" la configurazione viene scritta nel centralino e da quel momento è possibile effettuare chiamate verso l'esterno (avendo opportunamente configurato i fasci negli step precedenti).

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

E' possibile selezionare gli interni che si desidera modificare utilizzando la lista "Seleziona" o le checkbox accanto agli utenti elencati.

Cliccando poi sul tasto :guilabel:`Modifica`, verrà visualizzata una finestra con le impostazioni che possono essere modificate.

Il contenuto dei campi viene mostrato solo se gli interni selezionati hanno tutti lo stesso valore per quel campo, altrimenti rimane vuoto.

L'icona :guilabel:`lucchetto` chiuso alla destra del campo indica che il campo non verrà modificato.

Per esempio, se gli interni 201 e 202 hanno un valore differente per il gruppo di chiamata, il campo sarà vuoto, ma se il :guilabel:`lucchetto` è chiuso, il valore non verrà sovrascritto.

Se invece si clicca sul :guilabel:`lucchetto` in modo che sia aperto e si salva, il gruppo di chiamata verrà sovrascritto con il valore del campo.

Amministrazione
==============

La sezione "Amministratore" raggruppa le azioni che possono essere fatte dall'amministratore del centralino

Lingue
------

Nel menù Lingue è possibile impostare la lingua di sistema del |product| impostandola come quella di default e installare anche altri pacchetti lingua aggiuntivi.

Impostazioni
------------
Nella parte "Impostazioni", è possibile cambiare la password dell'utente admin.

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
- Password utente (se si è in modalità Legacy)

E' presente anche la possibilità di stampare l'elenco in formato PDF cliccando sul bottone "Stampa report PDF"
