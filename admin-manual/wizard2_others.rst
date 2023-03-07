.. _applicazioni:

Applicazioni
============
La sezione "Applicazioni" consente di creare, modificare o eliminare determinate funzionalità del centralino, che nel wizard vengono solo create e configurate, ma che poi vengono utilizzate nel CTI.

Ad esempio le schede cliente, nel wizard, vengono configurate per accedere al database e per mostrare in maniera pratica le informazioni ottenute, ma il reale utilizzo sarà all'interno del CTI, durante le chiamate o durante la ricerca di determinate informazioni.

Schede cliente
--------------
a sezione schede cliente, permette di raggruppare le informazioni presenti su database esterni al centralino e mostrarle in fase di chiamata. Ad esempio, sulla chiamata di un certo cliente, prendere le informazioni sul database relative alle sue fatture o ad eventuali insoluti e valutare ad esempio, se fornire assistenza o meno. Per generare una nuova scheda cliente i passi sono i seguenti

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

I template sono il fac-simile per le vostre schede cliente. Utilizzano il motore `ejs`, che ha una sintassi *JavaScript-like*, che vi permette di scrivere codice HTML utilizzando specifiche direttive che potete trovare nel sito https://github.com/tj/ejs.

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

Se la vostra query è di questo tipo: ::

  select * from phonebook where homephone like '%150' or workphone like '%850' or cellphone like '%150' or fax like '%850'

dovrà diventare così: ::

 select * from phonebook where homephone like '%$NUMBER' or workphone like '%$NUMBER' or cellphone like '%$NUMBER' or fax like '%$NUMBER'

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

Aggiunta di rubriche esterne
----------------------------

Dal menù :menuselection:`Applicazioni -> Sorgenti rubrica` è possibile definire sorgenti di
rubriche esterne a quella di |product| per integrarla con contatti residenti su database esterni.

Per configurare una nuova sorgente sono necessari tre passaggi:

1. **Sorgente:** configurazione dell'accesso al database sorgente dei contatti

2. **Mappa:** associazione dei campi del database sorgente a quelli della rubrica di |product|

3. **Impostazioni:** scelta dell'intervallo di sincronizzazione

Sorgente rubrica
................

Alla sorgente va assegnato un :guilabel:`Nome rubrica` che deve essere
univoco, per poter distinguere l'origine dei contatti importati nella rubrica di |product|.

In base al :guilabel:`Tipo sorgente` vanno poi specificati ulteriori attributi:

MySQL

  Sono necessari nome database, indirizzo/porta server, nome utente e password del database
  sorgente.

  Inoltre nell'area di testo :guilabel:`Select query` va inserita l'interrogazione
  in linguaggio SQL utilizzata per prelevare i dati da importare nella rubrica centralizzata.
  Se presente nell'area di testo, sostituire la parola ``[table]`` con il nome della
  tabella sorgente.

CSV

  Nel campo :guilabel:`URL` si può indicare l'indirizzo web di un file in formato CSV
  (*Comma-Separated Values*, valori separati da virgola e doppie virgolette "" come qualificatori di testo, obbligatorio se il campo contiene una virgola o uno spazio). Sono accettati indirizzi che iniziano con ``http://`` e ``https://``.

  In alternativa è possibile caricare tramite il pulsante a destra dello stesso
  campo di testo un file in formato CSV. In questo caso il campo :guilabel:`URL` sarà
  valorizzato automaticamente.

  Il file CSV deve essere in codifica UTF-8 e contenere i nomi delle colonne sulla prima riga.

Il pulsante :guilabel:`Verifica` consente la visualizzazione dell'anteprima dei dati prelevati dalla sorgente.

Risoluzione nomi personalizzata
...............................

Nel caso si desiderasse utilizzare una sorgente diversa dalla rubrica centralizzata per risolvere i nomi, è possibile fare uno script custom di risoluzione e metterlo nella cartella `/usr/src/nethvoice/lookup.d`. 
Nella cartella `/usr/src/nethvoice/samples/` ci sono due script di esempio `lookup_dummy.php` e `lookup_vte.php` che possono essere usati come spunto per creare il proprio personalizzato. Il primo restituisce un risultato finto qualunque numero chiami o sia chiamato, il secondo utilizza un'API esterna.

Mappa
.....

In questo passaggio è necessario stabilire la corrispondenza tra i campi del database sorgente e quelli destinatari della rubrica di |product|.

Per esempio, si potrebbe associare il campo ``phone`` sorgente con quello destinatario ``workphone``.

Ecco la mappa dei campi della Rubrica Centralizzata e di come vengono usati:

.. list-table:: Campi Rubrica Centralizzata
    :widths: 10 10
    :header-rows: 1

    * - owner_id
      - Proprietario del contatto

    * - type
      - Sorgente di provenienza

    * - homeemail
      - Indirizzo email domicilio

    * - workemail
      - Indirizzo email lavorativo

    * - homephone
      - Numero telefonico domicilio

    * - workphone
      - Numero telefonico lavorativo

    * - cellphone
      - Numero cellulare

    * - fax
      - Numero fax

    * - title
      - Mansione

    * - company
      - Azienda

    * - notes
      - Note

    * - name
      - Nome e cognome

    * - homestreet
      - Indirizzo domicilio

    * - homepob
      - Casella postale domicilio

    * - homecity
      - Città domicilio

    * - homeprovince
      - Provincia domicilio

    * - homepostalcode
      - Codice postale domicilio

    * - homecountry
      - Stato/regione domicilio

    * - workstreet
      - Indirizzo lavorativo

    * - workpob
      - Casella postale lavoro

    * - workcity
      - Città lavorativa

    * - workprovince
      - Provincia lavorativa

    * - workpostalcode
      - Codice postale lavorativo

    * - workcountry
      - Stato/Regione lavorativa

    * - url
      -  Indirizzo WEB

Impostazioni
............

È possibile scegliere l'intervallo di sincronizzazione dei contatti tra:

- 15 minuti
- 30 minuti
- 1 ora
- 6 ore
- 24 ore

Una volta creata la sorgente, è possibile:

- eseguire subito la sincronizzazione tramite il pulsante :guilabel:`Sincronizza`
- abilitare/disabilitare la sincronizzazione

Per ulteriori informazioni sulla rubrica di |product| e su come integare altri tipi
di sorgenti, come database ODBC o script personalizzati, consultare
`Rubrica Centralizzata <http://nethserver.docs.nethesis.it/it/v7/phonebook-mysql.html>`_.

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

La composizione della URL può essere fatta utilizzando questi parametri valorizzati per ogni chiamata:

- `$CALLER_NUMBER` (Numero Chiamante)
- `$CALLER_NAME` (Nome associato da |product| al numero chiamante)
- `$CALLED` (Numero Chiamato)
- `$UNIQUEID` (Identificativo univoco della chiamata)


E' possibile abilitare l'opzione `Solo chiamate su code` per attivare la URL parametrizzata solo per chiamate che suonano in una coda.

Tutti gli utenti che hanno quel profilo saranno abilitati all'utilizzo dell'URL appena creato.

.. note::

    1. Ad un profilo può essere associato un solo URL.
    2. Affinché l'URL possa essere invocato è necessario che l'utente finale abbia abilitato la visualizzazione dei popups nel proprio browser !

In alcuni casi può essere necessario eseguire un'API per poter formare l'URL che dovrà essere visualizzato dal CTI, per esempio se si deve aprire un URL che contiene un codice cliente, ma è necessario eseguire un API esterna per poter trovare il corretto codice cliente a partire dal numero di telefono. Per ottenere questo comportamento, è necessario creare uno script personalizzato. Si può prendere d'esempio lo script `/usr/src/nethvoice/parametrized_url_customercode.php`

Gestione Multipla Interni
-------------------------

L'applicazione *Gestione Multipla Interni* consente di modificare massivamente gruppi di utenti.

É possibile selezionare gli interni che si desidera modificare utilizzando la lista "Seleziona" o le checkbox accanto agli utenti elencati.

Cliccando poi sul tasto :guilabel:`Modifica`, verrà visualizzata una finestra con le impostazioni che possono essere modificate.

Il contenuto dei campi viene mostrato solo se gli interni selezionati hanno tutti lo stesso valore per quel campo, altrimenti rimane vuoto.

L'icona :guilabel:`lucchetto` chiuso alla destra del campo indica che il campo non verrà modificato.

Per esempio, se gli interni 201 e 202 hanno un valore differente per il gruppo di chiamata, il campo sarà vuoto, ma se il :guilabel:`lucchetto` è chiuso, il valore non verrà sovrascritto.

Se invece si clicca sul :guilabel:`lucchetto` in modo che sia aperto e si salva, il gruppo di chiamata verrà sovrascritto con il valore del campo.

.. _wizard2-telefoni-multipli:

Gestione Multipla Telefoni
--------------------------

La pagina :guilabel:`Applicazioni > Gestione multipla telefoni` consente di
selezionare più telefoni in base a criteri di gruppo utenti o di modello.

Una volta che sono stati selezionati uno o più modelli, in base alla selezione
sarà possibile effettuare le azioni descritte nei seguenti paragrafi.

Riavvio
.......

Tutte le impostazioni di provisioning vengono recepite dai telefoni
automaticamente ogni notte, se gli :ref:`aggiornamenti automatici
<provisioning2-aggiornamenti-automatici>` sono abilitati.

Altrimenti è necessario riavviare i telefoni mediante la pagina di
:guilabel:`Gestione multipla telefoni`. Solo i telefoni che hanno completato la
registrazione SIP possono essere riavviati da questa pagina.

Il riavvio può essere immediato oppure pianificato in un tempo futuro mediante i
pulsanti :guilabel:`Riavvia ora` e :guilabel:`Riavvio ritardato`.

Scelta modello
..............

Se i telefoni selezionati appartengono al medesimo produttore, è possibile
assegnare a tutti lo stesso modello mediante il pulsante :guilabel:`Assegna
modello`.
