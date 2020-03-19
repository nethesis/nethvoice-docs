.. _wizard2-section:

==================================
Wizard prima configurazione (beta)
==================================

.. warning::
    
    Le funzioni descritte in questa sezione sono disponibili in anteprima solo
    ai membri del |product| Quality Team. Fare riferimento a
    :ref:`wizard-section` per la versione stabile.

In questa sezione sono descritte le nuove funzionalità introdotte dal
:ref:`nuovo sistema di provisioning <provisioning-phone2-section>` basato sul
progetto Tancredi. Le differenze rispetto all'interfaccia precedente riguardano
le seguenti pagine:

- :guilabel:`Dispositivi` è stata spostata in una sezione del menù a sé stante,
  composta dalle voci :guilabel:`Telefoni` e :guilabel:`Modelli`.

- :guilabel:`Configurazioni` è stata spostata in una sezione del menù a sé
  stante.

- :guilabel:`Gestione multipla telefoni` è stata aggiunta sotto la sezione
  :guilabel:`Applicazioni`.


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

La scelta delle precedenti impostazioni dipende da come i telefoni dovranno
raggiungere il centralino.

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

.. _wizard2-configurazioni:

Configurazioni
==============

La pagina :guilabel:`Configurazioni` stabilisce per ogni singolo utente le
impostazioni personali e i dispositivi associati.

- :guilabel:`Profilo`, decide di quali permessi l'utente dispone, 

- :guilabel:`Gruppo`, consente di raggruppare gli utenti per facilitare la
  distribuzione delle configurazioni mediante :ref:`wizard2-telefoni-multipli`,

- :guilabel:`Associa dispositivo`, consente di selezionare un telefono non
  ancora associato e assegnarlo all'utente. È possibile anche immettere
  l'indirizzo MAC di un dispositivo non supportato dal provisioning: in tal caso
  è necessario configurare il dispositivo manualmente.

Per ogni dispositivo è possibile selezionare se la :guilabel:`Crittografia` è
abilitata o meno. L'impostazione iniziale dipende dalla configurazione del
centralino effettuata durante la procedura di prima configurazione (vedi
:ref:`wizard2-dispositivi`). Se il centralino viene raggiunto tramite rete
pubblica (WAN) è richiesta l'attivazione della crittografia.

.. warning::

    Se :guilabel:`Crittografia` è abilitata assicurarsi che il certificato SSL/TLS
    del sistema sia valido e contenga il nome del centralino, altrimenti i
    telefoni non possono stabilire la connessione TLS.

.. _wizard2-telefoni-multipli:

Gestione multipla telefoni
==========================

La pagina :guilabel:`Applicazioni > Gestione multipla telefoni` consente di
selezionare più telefoni in base a criteri di gruppo utenti o di modello.

Una volta che sono stati selezionati uno o più modelli, in base alla selezione
sarà possibile effettuare le azioni descritte nei seguenti paragrafi.

Riavvio
-------

Tutte le impostazioni di provisioning vengono recepite dai telefoni
automaticamente ogni notte, se gli :ref:`aggiornamenti automatici
<provisioning2-aggiornamenti-automatici>` sono abilitati.

Altrimenti è necessario riavviare i telefoni mediante la pagina di
:guilabel:`Gestione multipla telefoni`. Solo i telefoni che hanno completato la
registrazione SIP possono essere riavviati da questa pagina.

Il riavvio può essere immediato oppure pianificato in un tempo futuro mediante i
pulsanti :guilabel:`Riavvia ora` e :guilabel:`Riavvio ritardato`.

Scelta modello
--------------

Se i telefoni selezionati appartengono al medesimo produttore, è possibile
assegnare a tutti lo stesso modello mediante il pulsante :guilabel:`Assegna
modello`.
