.. _wizard2-section:

===========================
Wizard prima configurazione
===========================

.. hint::
    
    Fare riferimento a :ref:`wizard-section` per la versione precedente

Il wizard di prima configurazione consente di installare e configurare agevolmente tutte le componenti di un centralino.

È possibile raggiungere l'applicazione web all'indirizzo

- ``https://IP_DEL_SERVER/NOME_PRODOTTO`` (es.: \https://192.168.1.1/|product_command|)

Mentre l'interfaccia per la configurazione avanzata, da utilizzare se necessaria solo dopo aver completato il wizard di prima configurazione, è possibile raggiungerla all'indirizzo web 

- ``https://IP_DEL_SERVER/freepbx/admin``

Per l'accesso iniziale utilizzare le credenziali

- nome utente ``admin``

- password ``Nethesis,1234``


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

È possibile ora inserire gli interni relativi per ogni utente:

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

È possibile utilizzare la funzione anche per assegnare gli interni ad utenti già creati, ma senza interno assegnato.

In questo caso, il campo *password* verrà ignorato.

Il tasto esporta consente di scaricare un modello di CSV con gli attuali utenti da modificare per poi importare nuovamente. Le righe precedute da # verranno considerate commenti. I gruppi CTI, una lista separata da pipe `|` verranno creati automaticamente. Il profilo CTI deve essere scelto tra quelli già creati

Fasci
=====
Nella sezione fasci è possibile configurare i gateway per gestire le linee fisiche o creare fascio VoIP specificando le credenziali delle linee SIP date dal provider.

I fasci, per collegare i gateway o le linee VoIP, vengono creati utilizzando la libreria PJSIP.

.. _fisici:

Fisici
------
Come per i dispositivi, questa sezione scansiona la vostra rete e cerca dei gateway disponibili, una volta individuati è possibile specificare, selezionandone uno, due impostazioni:

- Modello: specificare il modello del gateway
- Impostazioni dinamiche in base al modello:

  * ISDN (Specificare per la linea se è Point-Point or Point-MultiPoint)
  * PRI
  * FXS (Specificare per ogni porta, l'interno da assegnare scegliendo un utente precedentemente configurato)
  * FXO (Specificare direttamente il numero, nel campo di testo)

Una volta salvate le impostazioni è possibile caricare la configurazione sul gateway tramite il bottone "Carica"
Il gateway prende la configurazione e si riavvia, vengono inoltre creati i fasci relativi.

VoIP
----
È possibile creare dei fasci VoIP selezionando uno dei provider supportati, e inserendo le informazioni necessarie.

Premere "Crea" per creare la configurazione relativa per quel fascio VoIP.

Rotte
=====
Nella sezione rotte è possibile configurare le rotte in entrata e in uscita per il vostro centralino

In entrata
----------
Una volta in questa sezione, vi si presenta la lista delle rotte già configurate, con la possibilità di modificarle o eliminarle.

Premendo sul bottone "Crea nuova rotta" si aprirà un nuovo tab con l'applicazione Visual Plan, che vi consentirà di creare, modificare e collegare i componenti del centralino che gestiranno il flusso della chiamata per il numero in ingresso 

Premendo il simbolo di spunta nell'applicazione Visual Plan, la configurazione della vostra rotta verrà salvata e da quel momento potrete ricevere chiamate che seguiranno il flusso da voi scelto.

In uscita
---------
In questa sezione è presente la lista delle rotte in uscita. La prima volta che questa pagina viene visitata il wizard vi propone delle rotte in uscita di default, con i pattern di chiamata specifici per le diverse lingue.

È possibile inoltre specificare l'ordine con cui verranno usati i fasci precedentemente creati, avendo quindi la possibilità di personalizzare la priorità dei vari fasci.

Premendo il tasto "Salva" la configurazione viene scritta nel centralino e da quel momento è possibile effettuare chiamate verso l'esterno (avendo opportunamente configurato i fasci negli step precedenti).

.. _wizard2-dispositivi:


Dispositivi
===========

Durante la procedura guidata di prima configurazione in questa sezione viene
richiesta la conferma di alcune impostazioni fondamentali (pulsante
:guilabel:`Modifica impostazioni di default`).

- :guilabel:`Crittografia` per funzionare correttamente richiede che il sistema
  disponga di un certificato SSL/TLS valido per il nome host inserito in
  :guilabel:`Indirizzo centralino`.

- :guilabel:`Indirizzo centralino` può essere l'indirizzo IP o il nome 
  dell'host di |product|, se correttamente inserito nel DNS utilizzato
  dai telefoni e nel certificato SSL/TLS utilizzato dal sistema.

- :guilabel:`Password admin` sarà la password per accedere all'interfaccia web 
  dei telefoni configurati con l'utente amministratore.

- :guilabel:`Password utente` sarà la password per accedere all'interfaccia web 
  dei telefoni configurati con l'utente senza privilegi amministrativi.

La scelta delle precedenti impostazioni di Crittografia e Indirizzo Centralino
dipende da come i telefoni dovranno raggiungere il centralino.

- Se i telefoni sono tutti nella stessa rete del centralino (LAN),
  :guilabel:`Crittografia` può essere disabilitata e :guilabel:`Indirizzo
  centralino` può contenere un indirizzo IP.

- Se uno o più telefoni raggiungono il centralino tramite rete pubblica (WAN),
  come nel caso in cui il centralino sia ospitato su una VPS in cloud, allora
  :guilabel:`Crittografia` deve essere abilitata e :guilabel:`Indirizzo
  centralino` deve contenere il nome completo e presente nel DNS pubblico.

In ogni caso è possibile scegliere su ogni singolo telefono se la crittografia è
utilizzata o meno, a patto che il certificato SSL/TLS del sistema sia valido. A
questo proposito fare riferimento a :ref:`wizard2-configurazioni`.

Si tenga però presente che il centralino non consente connessioni senza
crittografia provenienti da rete pubblica (WAN).

Altre impostazioni da poter variare:

* :ref:`Preferenze <panel-preferences>`
* :ref:`Rubrica LDAP <panel-phonebook>`

Una volta salvate le impostazioni, sarà possibile modificarle di nuovo
dalla pagina :guilabel:`Dispositivi > Modelli`, pulsante :guilabel:`Impostazioni
di default`.

.. _wizard2-telefoni:

Telefoni
--------

La pagina :guilabel:`Dispositivi > Telefoni` consente l'identificazione dei
telefoni da parte di |product| mediante l'immissione dell'indirizzo MAC. È
possibile immettere l'indirizzo MAC con i seguenti metodi:

- **Incolla da file** di indirizzi MAC multipli. Vengono accettate le sintassi
  separate da segno meno ``-`` (es.: ``AA-BB-CC-11-22-33``), due punti ``:``
  (es.: ``AA:BB:CC:11:22:33``) o senza separatore (es.: ``AABBCC112233``). Le
  lettere possono essere indifferentemente maiuscole o minuscole.

- **Scansione rete** alla ricerca di indirizzi MAC di telefoni supportati. 

- **Aggiunta manuale** di un indirizzo MAC alla volta. Utile se si dispone di un
  lettore di codice a barre.

In ogni caso, dopo aver immesso l'indirizzo MAC è possibile selezionare il
**modello del telefono**. La selezione del modello esatto è richiesto per la
corretta configurazione del telefono. 

.. warning::

    Se il modello non viene selezionato o viene selezionato il modello sbagliato
    alcune funzioni del telefono, come il provisioning via RPS o i tasti linea, 
    potrebbero non essere disponibili

.. _wizard2-modelli:

Modelli
-------

La pagina :guilabel:`Dispositivi > Modelli` elenca i modelli base dei telefoni
selezionati in :guilabel:`Dispositivi > Telefoni` più eventuali modelli
personalizzati.

È possibile creare un modello personalizzato a partire da uno esistente, tramite
il pulsante :guilabel:`Crea nuovo modello`.

In questa pagina sono anche modificabili alcuni parametri ereditati da tutti i
modelli, tramite il pulsante :guilabel:`Impostazioni di default`. Questi
parametri comprendono :guilabel:`Crittografia` e :guilabel:`Indirizzo
centralino`, già impostati dalla procedura di prima configurazione come spiegato
in :ref:`wizard2-dispositivi`.

A seconda delle funzionalità proprie del modello, possono essere disponibili
i pannelli e le opzioni descritti in :ref:`wizard2-provisioning-section`.


.. _wizard2-configurazioni:

Configurazioni
==============

Gruppi
------
È possibile creare dei gruppi utente che poi saranno visibili e utilizzabili nelle applicazioni, come ad esempio nel |product_cti|

- Cliccare il bottone "Crea nuovo gruppo"
- Specificare un nome e salvare
- Il gruppo compare tra la lista

Profili
-------
Il centralino prevede di specificare determinate funzionalità per ogni utente e queste funzionalità vengono raggruppate in dei profili.

Con l'installazione, vengono creati di default 3 profili che contengono l'abilitazione o meno a certe funzionalità.

- Base: funzionalità minime per l'utente
- Standard: funzionalità di gestione classiche per l'utente
- Avanzato: quasi tutte le funzionalità sono sbloccate, per l'utente Avanzato

È possibile creare anche nuovi profili, duplicando uno esistente o creandone di nuovi e specificando le varie funzionalità

.. note:: Ricordarsi di abilitare sui profili dove necessario l'accesso ai gruppi utente precedentemente creati.

Utenti
------
La pagina :guilabel:`Utenti` stabilisce per ogni singolo utente le
impostazioni personali e i dispositivi associati.

- :guilabel:`Profilo`, decide di quali permessi l'utente dispone, 

- :guilabel:`Gruppo`, consente di raggruppare gli utenti per facilitare la
  distribuzione delle configurazioni mediante :ref:`wizard2-telefoni-multipli`,

- :guilabel:`Cellulare`, consente di associare un numero di cellulare all'utente da 
  mostrare nel pannello operatore del |product_cti| e da utilizzare nella gestione
  dello stato di presence

- :guilabel:`Casella Vocale`, consente di attivare la casella vocale per l'utente come
  destinazione di ogni fallimento di chiamate al suo interno

- :guilabel:`Associa dispositivo`, consente di selezionare un telefono non
  ancora associato e assegnarlo all'utente tra quelli gestiti con il provisioning.
  È possibile creare delle credenziali da utilizzare su di un dispositivo non supportato 
  dal provisioning: in tal caso è necessario utilizzare un dispositivo personalizzato.

Vengono poi mostrati i dispositivi associati all'utente.
I dispostivi possono essere di due tipologie, software (Web Phone e Mobile App) o 
fisici, legati ad un telefono configurato con il provisioning o ad un dispositivo 
personalizzato.

È possibile associare ad ogni utente fino a 9 dispostivi:

- :guilabel:`Web Phone` attiva il client telefonico del |product_cti| per gestire le 
  chiamate direttamente al suo interno senza necessità di avere telefoni fisici.

- :guilabel:`Mobile App` attiva la possibilità di configurare sullo smartphone un
  dispositivo (vedere :ref:`nethcti_mobile`).

Per ogni dispositivo fisico viene mostrato:

- :guilabel:`Crittografia` abilitata o meno. L'impostazione iniziale dipende dalla 
  configurazione di |product| effettuata durante la procedura di prima configurazione
  (vedi :ref:`wizard2-dispositivi`). Se il centralino viene raggiunto tramite rete 
  pubblica (WAN) è richiesta l'attivazione della crittografia.

.. warning::

    Se :guilabel:`Crittografia` è abilitata assicurarsi che il certificato SSL/TLS
    del sistema sia valido e contenga il nome del centralino, altrimenti i
    telefoni non possono stabilire la connessione TLS.

- :guilabel:`Modello di Configurazione` scelto. È possibile variare il modello di 
  configurazione tra quelli proposti.
- :guilabel:`Modifica Configurazione` È possibile modificare la configurazione del
  singolo telefono inserendo modifiche valide solo per questo dispositivo.
  Il singolo telefono ha di base la configurazione del modello e delle impostazioni
  di default. Fare riferimento a :ref:`wizard2-modelli` per maggiori dettagli.
- :guilabel:`Mac-Address` Viene mostrato l'indirizzo MAC del dispostivo associato.
- :guilabel:`Mostra password` per i dispositivi personalizzati. Viene mostrata la
  password SIP che insieme all'interno e all'indirizzo del |product| è possibile
  utilizzare per configurare manualmente il dispositivo personalizzato.
- :guilabel:`Riavvia` Se il dispositivo è registrato allora è possibile riavviarlo.
- :guilabel:`Disassocia` È possibile disassociare il dispositivo dall'utente.

.. _provisioning-scopes-priority:

Priorità configurazioni telefoni
================================

La configurazione creata dal provisioning di |product| per i dispositivi telefonici 
viene ricavata unendo le impostazioni provenienti da:

- :guilabel:`Impostazioni Default`: si trovano nella pagina :ref:`wizard2-modelli`.
- :guilabel:`Impostazioni Modello`: vengono presi i parametri dalla configurazione del 
  modello associato al dispositivo, la configurazione si trova nella pagina 
  :ref:`wizard2-modelli`.
- :guilabel:`Impostazione Telefono`: vengono presi i parametri della configurazione
  del singolo telefono che si trovano nella pagina :ref:`wizard2-configurazioni`.
- Impostazioni |product_cti| dove è possibile configurare 
  parametri del telefono fisico associato all'utente.

Nel caso in cui ci sia un parametro con una configurazione non omogenea nelle varie 
sezioni sopra elencate questo è l'ordine di priorità decrescente che verrà seguito:

- :guilabel:`Impostazione telefono` e Impostazioni |product_cti| sono 
  le impostazioni con la priorità massima, tra le due vale l'ultima effettuata.
- :guilabel:`Impostazioni Modello`
- :guilabel:`Impostazioni di Default`


Amministrazione
===============

Lingue
------

Nel menù Lingue è possibile impostare la lingua di sistema del |product| impostandola come quella di default e installare anche altri pacchetti lingua aggiuntivi.

Impostazioni
------------

La pagina delle Impostazioni permette di gestire diversi aspetti della configurazione.

* :guilabel:`Password`: è possibile cambiare la password dell'utente admin dedicato all'accesso all'interfaccia web di |product|.

* :guilabel:`Videoconferenza`: indicare l'URL del Sistema di Conferenza fornita dal fornitore. È possibile in alternativa inserire l'URL di un qualsiasi server Jitsi pubblico verificando le condizioni di utilizzo, la compatibilità con le proprie direttive privacy e necessità di continuità di servizio.

* :guilabel:`Impostazioni NAT`: per gestire correttamente il NAT nel protocollo SIP, |product| ha necessità di conoscere l'indirizzo che utilizzerà presentandosi all'esterno e le reti da considerare locali, per le quali non dovrà tenere conto del NAT e delle sue impostazioni:

  1) Inserire in :guilabel:`Indirizzo Esterno` l'IP pubblico con il quale |product| effettuerà connessioni esterne alla propria rete.
  2) Inserire in :guilabel:`Reti Locali` tutte le reti in formato CIDR dalle quali |product| si deve aspettare connessioni dirette senza considerare quindi il NAT.

* :guilabel:`Impostazioni Firewall`: il firewall di |product| nella configurazione di partenza non accetta connessioni da reti esterne per il protocollo SIP TLS (porta 5061 tcp e porte da 10000 a 20000 udp).
  In questa sezione è possibile configurare il firewall per accettare traffico SIP TLS anche da reti non locali abilitando il SIPS esterno.
  Abilitando l'accesso SIPS esterno, si concede anche l'accesso in TLS al proxy Flexisip sulla porta 6061, che consente l'uso dell'App mobile.

* :guilabel:`Impostazioni Rubrica`: in questa sezione è possibile abilitare l'esporazione della rubrica di |product| in LDAP per consentire di solito ai telefoni di accedervi in sola lettura.
  La rubrica può essere pubblicata in LDAP in due modalità (la configurazione data ai telefoni sarà completa di tutti i parametri necessari):

  1) **LDAP**, che comporta una pubblicazione in chiaro e ad accesso anonimo (senza cioè la necessità di credenziali di autenticazione); questa modalità è indicata se tutti i telefoni sono nella stessa rete di |product|
  2) **LDAPS**, che utilizza la crittografia e richiede delle credenziali di autenticazione per accedere; questa modalità è indicata in presenza di telefoni che si collegano a |product| da reti esterne
  
* :guilabel:`Sorgenti Rubrica`: in questa sezione è possibile abilitare/disabilitare le sorgenti di default da inserire nella rubrica di |product|.

  1) **Numeri brevi Centralino**, gestibili tramite la sezione :menuselection:`Amministrazione -> Avanzate -> Applicazioni -> Codice Rapido di Chiamata`
  2) **Interni Centralino**, gestibili tramite la sezione :menuselection:`Utenti -> Interni`
  3) **Contatti condivisi del CTI**, si riferisce ai contatti pubblici aggiunti tramite la rubrica del |product_cti|

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

È presente anche la possibilità di stampare l'elenco in formato PDF cliccando sul bottone "Stampa report PDF"

