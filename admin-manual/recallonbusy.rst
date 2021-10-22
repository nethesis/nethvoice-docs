Ritorno da trasferimento Cieco
==============================

Questa funzione consente di prenotare la richiamata quando si tenta di chiamare un interno di |product| e questo è impegnato in un'altra conversazione. 


Configurazione
--------------

Di default questa funzione è disabilitata, la si può abilitare dall'interfaccia avanzata di amministrazione di |product|, nel menù :guilabel:`Applicazioni`-> :guilabel:`Richiama su occupato`.

Dalla pagina di configurazione è possibile impostare il comportamento di default e il tasto da premere per prenotare la richiamata. 

È possibile anche abilitare o disabilitare la richiamata su occupato per singolo interno dalla pagina di configurazione avanzata dell'interno. 
In questo caso, si configura il comportamento dell'interno che deve utilizzare il servizio.

Le impostazioni lato interno hanno priorità rispetto all'impostazione generale.

Quando un interno con il richiama su occupato chiama un altro interno impegnato in una conversazione, viene chiesto all'utente di premere il tasto 5 (modificabile) per prenotare la richiamata. 
Se l'utente preme il tasto, quando l'interno chiamato tornerà disponibile partirà una chiamata prima verso il chi ha richiesto il servizio e alla risposta verso l'interno con cui si desiderava parlare.

Se le richieste di richiamata saranno di diversi utenti, verranno accodate ed eseguite nell'ordine di creazione.

