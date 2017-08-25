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

- *Legacy*: il centralino diventa anche la base per i creare i vostri utenti, quindi al vostro server verrà installare una base LDAP su cui creare i vostri utenti
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

Gruppi
------
E' possibile creare dei gruppi utente che servono per raggruppare determinati utenti che poi saranno visibili nell'applicazione componenti

- Cliccare il bottone "Crea nuovo gruppo"
- Specificare un nome e salvare
- Il gruppo compare tra la lista

Profili
-------
Il centralino prevede di specificare determinate funzionalità per ogni utente e queste funzionalità vengono raggrupate in dei profili.

Con l'installazione, vengono creati di default 4 profili che contengono l'abilitazione o meno a certe funzionalità.

- Base: funzionalità minime per l'utente
- Standard: funzionalità di gestione classiche per l'utente
- Avanzato: quasi tutte le funzionalità sono sbloccate, per l'utente Avanzato
- Tutto: ogni funzionalità presente è abilitata, utilizzata per gli utenti amministratori

E' possibile creare anche nuovi profili, duplicando uno esistente o creandone di nuovi e specificando le varie funzionalità

Dispositivi
-----------
In questa sezione è possibile scansionare la propria rete e il wizard troverà in automatico i telefoni che sono collegati alla vostra rete, individuando, dove è possibile, marco e modello e vi fornisce inoltre l'indirizzo IP e il MAC address.

Se in alcuni telefoni non è stato possibile trovare automaticamente il modello, servirsi del menù a tendina per specificarlo.

Per rieseguire la scansione della rete, premere il pulsante *Scan*

Configurazioni
--------------
Lo step finale della sezione Utenti, prevede di raggruppare tutte le impostazioni create e definite nei passi precedenti.
La lista degli utenti mostra quelli a cui è stato associato un interno nel primo step. Selezionando un utente è possibile:

- Creare un dispositivo personalizzato (ad esempio softphone)
- Associare un telefono di quelli precedentemente configurati (effettuando il provisioning automatico)
- Inserire un numero di cellulare
- Abilitare il support alla voicemail
- Abilitare il support al WebRTC
- Scegliere il profilo da destinare all'utente (uno di quelli definiti allo step 3)
- Scegliere un gruppo a cui far parte (uno di quelli creati allo step 2)

Fasci
=====
Nella sezione fasci è possibile configurare i gateway per gestire le linee fisiche o creare fascio VoIP specificando le credenziali dei vostri provider

Fisici
------
Come per i dispositivi, questa sezione scansiona la vostra rete e cerca dei gateway dispobili, una volta individuati è possible specificare, selezionandone uno, due impostazioni:

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
E' possible creare dei fasci VoIP selezionando uno dei provider supportati, e inserendo le informazioni necessarie.

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

Premendo il tasto "Salva" la configurazione viene scritta nel centralino e da quel momento è possibile effeturare chiamate verso l'esterno (avendo oppurtunamente configurato i fasci negli step precedenti).

Applicazioni
============

Schede cliente
--------------

Sorgenti video
--------------

Amministratore
==============

Impostazioni
------------

Report
------
