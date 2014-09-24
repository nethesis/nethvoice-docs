=======================
Configurazione Avanzata
=======================

.. _provisioning_ref_label:

Provisioning
============

Descrizione
-----------

Il Provisioning è uno strumento che consente di configurare e amministrare gli apparecchi telefonici e i gateway telefonici direttamente dal |product|.

Il Provisioning altro non è che la configurazione da remoto dei propri apparati SIP tramite l’invio di un file di testo correlato all’indirizzo MAC dell’apparato da personalizzare.

Questa funzione, che sempre più spesso trova posto nell’ hardware recente, risulta essenziale per quanti si trovino nella situazione di dover replicare su larga scala impostazioni simili (si pensi ad esempio all’ipotesi di un centralino aziendale con molti interni) o comunque desiderino avere il “pieno controllo a distanza” di tutto l’hardware installato.

Il |product| è in grado di utilizzare il Provisioning grazie a due servizi integrati, il `DHCP <http://it.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_ e il `TFTP <http://it.wikipedia.org/wiki/Trivial_File_Transfer_Protocol>`_.

Per quanto riguarda la configurazione di rete degli apparecchi telefonici vedi anche :ref:`Rete <rete_ref_label>`.

Tutti i telefoni ip moderni possono chiedere all'avvio, al server che viene loro indicato dal dhcp o che è indicato nelle proprie impostazioni, la configurazione da applicare.

Il |product| ha un proprio server dhcp integrato che, se viene utilizzato dai telefoni per ottenere un ip di rete, fornisce tramite l\ **'opzione 66** del dhcp il server tftp, cioè se stesso.

E' consigliabile utilizzare il Provisioning con telefoni a *factory default*, in quanto in caso contrario si potrebbero perdere delle opzioni se non riportate correttamente nella configurazione sul |product|.

Il Provisioning si avvia entrando nel modulo :ref:`Provisioning Wizard <wizard_provisioning_ref_label>`, dove avviene la scansione della rete ed è possibile associare ogni apparecchio telefonico trovato ad un interno.

Fatta questa associazione e **Applicate le Modifiche** il |product| nella cartella ::

  /var/lib/tftpboot/

crea per ogni apparecchio telefonico sottoposto a Provisioning un file di configurazione e successivamente riavvia l'apparecchio telefonico che ripartendo contatterà il |product| prendendosi il file di configurazione appena creato.

Questa associazione viene anche riportata nella configurazione dell'interno :ref:`qui <interni_sip_ref_label>`.

Il telefono viene configurato con la configurazione standard per la sua marca e modello caricata sul |product|.

Il Provisioning di |product| da poi la possibilità di entrare nei dettagli della configurazione di un singolo apparecchio telefonico appena configurato tramite il modulo :ref:`Lista Terminali <provisioning_lista_terminali_ref_label>`.

E' anche possibile modificare le configurazione di ogni modello di telefono caricate sul |product| creando dei template per poi applicarli a tutti gli apparecchi telefonici dello stesso modello.

La gestione delle configurazioni è nel modulo :ref:`Gestione Template Terminali <provisioning_gestione_template_terminali_ref_label>`.

Il Provisioning comprende anche altri due moduli :ref:`Impostazioni Avanzate Terminali <provisioning_impostazione_avanzate_terminali_ref_label>` e :ref:`Configurazione Terminali <provisioning_configurazioni_terminali_ref_label>`.

Nelle :ref:`Impostazioni Avanzate Terminali <provisioning_impostazione_avanzate_terminali_ref_label>` si possono modificare alcune opzioni generali e in :ref:`Configurazione Terminali <provisioning_configurazioni_terminali_ref_label>` è possibile visualizzare l'elenco di marche e modelli supportati.

Configurazioni di Default Provisioning marche più utilizzate
------------------------------------------------------------

Yealink
~~~~~~~

I telefoni Yealink vengono supportati dalla versione di firmware **v70** in poi, la configurazione base che viene caricata con il Provisioning imposta:

*  Configurazione dell'interno selezionato.
*  Collegamento con il |product| per quanto riguarda sip, ntp, etc.
*  Accesso all'eventuale :ref:`Casella Vocale <casella_vocale_ref_label>`.
*  Codice di :ref:`Pickup <funzionalita_base_ref_label>`.
*  Rubrica LDAP collegata con |product| vedi :ref:`qui <rubrica_ref_label>`.
*  Rubrica remota collegata con |product| vedi `qui <Rubrica_|product|#Yealink>`.
*  Tasti Funzionali programmati con nell'ordine **Registro Chiamate**, **Rubrica LDAP**, **Pickup**, **Menù**.
*  Possibilità di aggiornare il firmware dei telefoni caricandolo nella cartella /tftpepm con nome MODELLO.rom ad esempio T22.rom T46.rom etc.

Snom
~~~~

I telefoni Snom vengono supportati dalla versione di firmware **v8**, la configurazione base che viene caricata con il Provisioning imposta:

*  Configurazione dell'interno selezionato.
*  Collegamento con il |product| per quanto riguarda sip, ntp, etc.
*  Accesso all'eventuale :ref:`Casella Vocale <casella_vocale_ref_label>`.
*  Codice di :ref:`Pickup <funzionalita_base_ref_label>`.
*  Rubrica LDAP collegata con |product| vedi :ref:`qui <rubrica_ref_label>`.
*  Tasti Funzionali programmati con nell'ordine **Gestione Identità**, **Registro Chiamate**, **Rubrica LDAP**, **Preferiti**.
*  Possibilità di aggiornare il firmware dei telefoni caricandolo nella cartella /tftpepm con nome MODELLO.bin ad esempio 300.bin 821.bin etc.
*  Per la serie 3XX, che da firmware superiori alla versione 6 per problemi di spazio non include il pacchetto linguaggi, se vengono caricati nella cartella /tftpepm i files gui\_lang\_IT.xml (Italiano) e gui\_lang\_EN.xml (Inglese), verranno caricati automaticamente

.. _suoneria_differenziata_ref_label:

Suoneria Differenziata
======================

La suoneria differenziata viene realizzata tramite le intestazioni del protocollo sip, in particolare il campo chiamato ALERT\_INFO. |product| gestisce questa funzione ma deve essere supportata anche dal telefono.  

E' possibile impostarla nei gruppi, nelle rotte in ingresso o nel FollowMe

Utilizzo dell'opzione ALERT\_INFO
=================================

I telefoni che attualmente supportano la suoneria differenziata tramite ALERT\_INFO sono, i Cisco, gli Snom e gli Yealink . La stringa da inserire nel campo *Suoneria differenziata* **varia da telefono a telefono**, per cui occorre rifarsi alla documentazione dello specifico modello, anche se di normalmente è qualcosa del tipo: ::

  http://127.0.0.1/Bellcore-dr3

Con questa opzione si stabilisce direttamente nel centralino quale suoneria utilizzare per tutti i telefoni.

I telefoni grandstream, con le versioni attuali di firmware, non supportano tale opzione, ma per questi è possibile usare la soluzione riportata di seguito

Utilizzo dell' ALERT\_INFO con parametro info
=============================================

In alternativa è possibile utilizzare il parametro info. Tale direttiva va indicata nel campo *Suoneria Differenziata* (o Alert Info) del Centralino (Gruppo, Rotte in Ingresso, Follow me) inserendo questa stringa: ::

  <http://notused >\;info=direct

in questa maniera si attiverà la suoneria custom relativa al Caller ID: direct

.. warning::   Per i telefoni Yealink dal firmware X.60.0.140 la stringa funzionate è 
    
    <http://www.notused >\;info=direct


Tale opzione permette di definire (a differenza di ALERT\_INFO) **una suoneria personalizzata per ogni telefono**, inoltre permette di gestire un **parco di telefoni misto** (snom e grandstream).

Esempio SNOM 360
----------------

Negli snom è possibile abilitare l'opzione *direct* tra le preferenze

*  Alert Internal Text: *direct*
*  Alert-Info Ringer: *scegliere la suoneria*

Esempio Grandstream
-------------------

Nelle impostazioni avanzate del telefono alla voce

*  Custom ring tone 2 (o 1 o 3),
*  usato se l'incoming caller ID è: "direct"

Esempio LinkSys
---------------

Anche per i Linksys (con i firmware più recenti) è possibile usare il campo info Nel telefono occorre specificare "direct" nella voce caller:

*  Alert External Text: -------- direct
*  Alert External Ringer: ------ Ringer1 (la suoneria da attivare)

Esempio Yealink
---------------

Collegarsi all'interfaccia web e spostarsi nel pannello Phone -> Ring, inserire la parola "direct" nel campo "Internal Ringer Text" e selezionare la suoneria preferita per le chiamate esterne (Internal Ringer File)

.. _interno_remoto_ref_label:

Interno Remoto
==============

Collegare un interno remoto, quindi non in rete locale, al |product| può essere fatto in diversi modi. La modalità più **sicura** e consigliata è quella di instaurare una **vpn** in modo che il collegamento venga equiparato a quello effettuato da rete locale. La vpn deve essere sempre instaurata tramite il gateway della rete del |product|.

I casi possono essere due:

|product| configurato come server&gateway
-----------------------------------------

Nel caso in cui il |product| sia il **gateway** della rete, è possibile utilizzare le modalità di vpn del |service_product| per collegare un interno remoto, vedi nella sua documentazione specifica.

In automatico la connessione vpn verrà considerata locale dal |product| e quindi tutti i servizi saranno raggiungibili anche dall'interno remoto. Sarà così possibile registrare l'interno remoto sul centralino ed utilizzarlo come se fosse in rete locale.

|product| configurato come server only
--------------------------------------

Se il |product| è configurato in modalità **server-only** la vpn dovrà essere configurata sul gateway della rete, firewall o router che sia.

Fatto questo se lo host remoto contatterà il |product| con un ip della rete locale (tipico di una vpn pptp) non c'è altro da fare, invece se l'ip sarà diverso, come ad esempio succede con openvpn, bisognerà aggiungere la rete della vpn tra le reti fidate del |service_product| accedendo all'indirizzo https://nomeserver:980 con lo username e password dell'utente admin.

E' teoricamente possibile in alternativa pubblicare i servizi del |product| su internet, facendo quindi accedere un interno remoto senza vpn.

Questa è una procedura **altamente sconsigliata** in quanto espone il |product| a problemi di sicurezza rilevanti, con esiti, soprattutto sulle bollette telefoniche, disastrosi.

.. _collegamenti_remoti_ref_label:

Collegamenti Remoti
=======================

Due o più |product| remoti, cioè non nella stessa rete posso essere collegati tra di loro tramite dei :ref:`fasci iax <fasci_iax_ref_label>`.  Si utilizza il protocollo IAX sia per le sue caratteristiche di semplicità, sia per il brillante comportamento in caso di nat, sia per le performance su chiamate multiple.

Se possibile è sempre indicato collegare le varie sedi remote con vpn tra di loro, in modo da far passare il traffico voce su di esse.

Collegamento con VPN
--------------------

La vpn deve essere sempre instaurata tramite il gateway della rete dei vari |product|.

I casi possono essere due:

*  |product| configurato come **server&gateway**

Nel caso in cui il |product| sia il **gateway** della rete, è possibile utilizzare le modalità di vpn del |service_product| per collegare un interno remoto, vedi nella sua documentazione specifica.

In automatico la connessione vpn verrà considerata locale dal |product| e quindi tutti i servizi saranno raggiungibili anche dall'interno remoto. Sarà così possibile registrare l'interno remoto sul centralino ed utilizzarlo come se fosse in rete locale.

*  |product| configurato come **server only**

Se il |product| è configurato in modalità **server-only** la vpn dovrà essere configurata sul gateway della rete, firewall o router che sia.

Fatto questo se il centralino remoto contatterà il |product| con un ip della rete locale non c'è altro da fare, invece se l'ip sarà diverso, come ad esempio succede con openvpn, bisognerà aggiungere la rete della vpn tra le reti fidate del |service_product| accedendo all'indirizzo https://nomeserver:980 con lo username e password dell'utente admin.

Collegamento senza VPN
----------------------

Ribadendo che la vpn è sempre consigliata, sia per ragioni di praticità ma soprattutto per ragioni di sicurezza, è possible collegare due o più |product| anche senza. Anche qui abbiamo due casistiche:

*  |product| configurato come **server&gateway**

Basta configurare tra le reti fidate del |service_product| gli ip pubblici delle sedi remote, andando all'indirizzo https://nomeserver:980 con lo username e password dell'utente admin. In questo modo il |product| aprirà i suoi servizi alle connessioni provenienti da quegli ip.

*  |product| configurato come **server only**

In questo caso il gateway della rete, firewall o router che sia, deve rigirare il traffico UDP entrante sulla porta 4569 al |product|, di solito con un port-forwarding, bisogna poi configurare tra le reti fidate del |service_product| gli ip pubblici delle sedi remote, andando all'indirizzo https://nomeserver:980 con lo username e password dell'utente admin.

Configurazione Fasci IAX
------------------------

Avendo permesso, tramite o la vpn e/o l'eventuale configurazione delle reti fidate, il traffico tra i due |product|, bisogna a questo punto configurare i :ref:`fasci iax <fasci_iax_ref_label>`. In pratica i centralini per interfacciarsi devono scambiarsi uno username e password che autorizza il collegamento.

.. warning:: L'utente è univoco, deve essere utilizzato per un solo collegamento, in caso di collegamento tra diversi |product| utilizzare username diversi per ogni fascio IAX.

Ecco un esempio pratico:

.. note:: Nel caso la VPN sia instaurata direttamente dal |product|, sul centralino remoto indicare l'ip del punto punto della vpn e non l'indirizzo della rete green.

Esempio configurazione fasci IAX per connessione tra due |product|
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sede A
^^^^^^

Impostazioni in Uscita
''''''''''''''''''''''
::

  Nome fascio: SedeA

  Dettagli PEER:

  host=IP_SEDE_B
  username=utenteB
  secret=passwordB
  type=peer
  qualify=60000

Impostazioni in Ingresso
''''''''''''''''''''''''
::

  Contesto UTENTE: utenteA

  Dettagli UTENTE:

  secret=passwordA
  type=user 
  context=from-internal

Sede B
^^^^^^

Impostazioni in Uscita
''''''''''''''''''''''
::

  Nome fascio: SedeB

  Dettagli PEER:

  host=IP_SEDE_A
  username=utenteA
  secret=passwordA
  type=peer
  qualify=60000

Impostazioni in Ingresso
''''''''''''''''''''''''
::

  Contesto UTENTE: utenteB

  Dettagli UTENTE:

  secret=passwordB
  type=user 
  context=from-internal

Configurazione Rotte in Uscita
------------------------------

L'ultima configurazione da effettuare è nelle :ref:`rotte in uscita <rotte_in_uscita_ref_label>`. Quello che dobbiamo fare è indicare al |product| come raggiungere gli interni remoti.

Le possibilità possono essere anche qui due:

Interni delle due sedi sovrapposti
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se i due |product| hanno la numerazione di interni sovrapposta, stessi interni in entrambi i centralini, si deve creare una rotta in uscita con il pattern di chiamata che includa gli interni remoti e un prefisso.

Il prefisso fa instradare la chiamata non per l'interno locale ma per l'interno remoto.

Ovviamente l'unico fascio da utilizzare sarà quello IAX precedentemente creato per il collegamento infrasede.

Ricordarsi di spuntare **Rotta Intra-Aziendale** se si vuole inviare al centralino remoto anche il nome del chiamante oltre che il numero. in modo che il chiamato sul display del telefono lo visualizzi.

Interni delle due sedi non sovrapposti
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nel caso che gli interni dei due |product| collegati siano ben distinti, non ci si deve preoccupare di distinguere con un prefisso la :ref:`rotta in uscita <rotte_in_uscita_ref_label>`.

E' necessario quindi creare una rotta con il pattern degli interni remoti e indicare il fascio iax di collegamento precedentemente creato.

Ricordarsi di spuntare **Rotta Intra-Aziendale** se si vuole inviare al centralino remoto anche il nome del chiamante oltre che il numero. in modo che il chiamato sul display del telefono lo visualizzi.

.. _codec_g729_ref_label:

Codec g729
==========


Introduzione
------------

Il G.729 è un codec che permette di minimizzare l'utilizzo della banda nelle comunicazioni audio digitali pur mantenendo una buona qualità sonora, ciò significa che usando G.729 è possibile veicolare, a parità di banda, un maggior numero di comunicazioni contemporanee [http://voiprevolution.blogosfere.it/2007/02/quanta-banda-per-il-voip.html\ \| rispetto agli altri codec] (come il G.711), con un consumo per canale pari a 8 kbit/s.

La licenza G.729 per Asterisk è a pagamento e viene venduta per singolo canale: è possibile acquistare più licenze per ogni server, così da poter instaurare più connessioni contemporanee utilizzando il codec G.729.

|product| ha anche una versione opensource di questo codec già installata che è possibile utilizzare in alternativa della versione a pagamento, consiglaimo di verificarne la compatibilità con un provider esterno.
Per migliore la qualità delle chiamate e minimizzare il consumo della banda, il codec G.729a diventa indispensabile:

*  nei fasci con :ref:`provider VoIP <configurazione_provider_voip_ref_label>`.
*  nei fasci :ref:`IAX infra-sede <collegamenti_remoti_ref_label>`.
*  negli interni posizionati fuori sede e collegati a |product| via VPN.

Una volta acquistata la licenza per il codec dal proprio rivenditore Digium (ART-00299) sarà possibile registrarla seguendo il documento
successivo.

Installazione
-------------

Per installare il modulo dare il comando

::
  yum install neth-g729

A questo punto registrare la licenza con il comando

::
 register

Selezionare le voci 1 e 5 ed inserire la key ID ricevuta via mail.

La Key ID è un codice del tipo: G729-9TLYBFP4XXXX (se c'è uno -01 o -02 finale, vanno tolti)

Inserire i dati anagrafici richiesti, la procedura dovrebbe concludersi in questo modo:

::
  Wrote license to /var/lib/asterisk/licenses/G729-GLP6742727P4.lic

Controllare che l'installazione sia andata a buon fine con il comando

::
  asterisk -rx "g729 show version"

il cui output dovrebbe essere simile a

::
  Digium G.729A Module Version 11.0_3.1.5 (optimized for i686_32)

Per usarlo sostituire nella configurazione dei fasci :ref:`sip <fasci_sip_ref_label>` o :ref:`iax <fasci_iax_ref_label>` questa voce (o equivalente):

::
  allow=gsm&alaw

con questa

::
  allow=g729

Per caricare il modulo riavviare il servizio |product|, tutte le chiamate saranno **terminate**,

 |product_command| restart

.. _strategie_squillo_ref_label:

Strategie Squillo
=================

Descrizione
-----------

Le Strategie di squillo servono a determinare come il |product| deve far suonare gli interni presenti nelle `Code <Code_|product|>`__, nel `Seguimi <Seguimi_|product|>`__ e nei `Gruppi di Chiamata <Gruppi_di_Chiamata_|product|>`__.

Ci sono varie opzioni tra cui scegliere, di cui alcune specifiche per ognuna delle tre voci sopracitate.

Configurazione
--------------

Opzioni Gruppi di Chiamata
~~~~~~~~~~~~~~~~~~~~~~~~~~

Le scelte possibili all' interno dei :ref:`Gruppi di Chiamata <gruppi_di_chiamata_ref_label>` sono:

*  **ringall**: chiama tutti i canali disponibili fino a quando uno non risponde (è impostato come predefinito).
*  **hunt**: chiama in rotazione tutti gli interni.
*  **memoryhunt**: chiama il primo interno della lista, poi a seguire il primo e il secondo, poi il primo il secondo e il terzo... ecc..
*  **\*-prim**: queste modalità sono descritte come sopra. Però se l' interno primario (il primo della lista) è occupato gli altri non saranno chiamati. Se il primario ha attivo il non disturbare il |product| non andrà avanti, mentre se è un trasferimento di chiamata incondizionato attivato su |product| squilleranno tutti gli interni.
*  **firstavaiable**: squillerà solo il primo disponibile.
*  **firstnotonphone**: squilla solo il primo che non è al telefono (ignora l' avviso di chiamata).

Opzioni Seguimi
~~~~~~~~~~~~~~~

Le possibilità sono le stesse dei Gruppi di Chiamata, con l'aggiunta di:

*  **ringallv2**: squilla l'interno principale seguito dagli interni restanti fino a quando non risponde.
*  **ringall-corner**: suonano tutti i telefoni solo se nessuno è occupato.

Opzioni Code
~~~~~~~~~~~~

*  **squillano tutti**: come ringall.
*  **leastrecent**: chiama l'agente che ha ricevuto meno chiamate all' interno della coda.
*  **fewestcalls**: chiama l'agente con il minor numero di chiamate completate nella coda.
*  **random**: chiama un agente a caso.
*  **rrmemory**: fa girare automaticamente le chiamate, ma, memorizzando dove l' ultima volta è passata senza risposta.
*  **rrordered**: come rrmemory, ma viene preservato l'ordine dei membri all'interno del file di configurazione.
*  **linear**: Suoneranno gli agenti nell' ordine stabilito. Per gli agenti dinamici, si usa l'ordine con il quale si sono registrati.
*  **wrandom**: causale, usando la penalità come fattore di ponderazione.

.. _pattern_ref_label:

Pattern
=======

Descrizione
-----------

I Pattern di Asterisk servono a inserire delle variabili in determinati moduli di |product| per ottenere delle regole più generali.

Possono essere utilizzati ad esempio nelle :ref:`Rotte in Entrata <rotte_in_entrata_ref_label>` o nelle :ref:`Rotte in Uscita <rotte_in_uscita_ref_label>`.

Sintassi
--------
::
  Regole:
  X corrisponde ad un numero da 0 a 9
  N corrisponde ad un numero da 2 a 9
  Z corrisponde ad un numero da 1 a 9
  . corrisponde a uno o più numeri
  [1237-9] corrisponde a tutti i numeri tra parentesi, il trattino indica un intervallo, in questo caso (1, 2, 3, 7, 8, 9).

Esempi:

::
  0721X.   Corrisponde a tutti i numeri che iniziano con 0721.
  [24-6]XX Corrisponde a tutti i numeri da 200 a 299, da 400 a 699.
  0ZX.     Corrisponde a tutti i numeri che iniziano con 0 seguiti da una cifra da 1 a 9.
  [135]XX  Corrisponde a tutti i numeri da 100 a 199, da 300 a 399 e da 500 a 599.

Per più informazioni vedi anche `qui <http://www.voip-info.org/wiki/view/Asterisk+Dialplan+Patterns>`_.

.. _struttura_filesystem_ref_label:

Struttura Filesystem
====================

Ecco come il |product| utilizza il filesystem sottostante:

Files di configurazione
-----------------------

I file di configurazione si trovano dentro la directory

::
 /etc/asterisk/

Si dividono in tre tipi:

-  **\*.conf**: sono i files di configurazione dei servizi. Quando questi servizi sono gestiti anche da interfaccia web e sono configurabili a mano includono gli altri tipi di file. Ad esempio sip.conf

-  **\*\_additional.conf**: sono i files dove viene scritta la configurazione effettuata tramite l'interfaccia web di |product|.  Ad ogni applica modifiche da interfaccia vengono azzerati e ricostruiti. Non fare modifiche in questo tipo di file, ad ogni applica modifiche verranno perse. Ad esempio sip\_additional.conf

-  **\*\_custom.conf**: sono files gestiti tramite Template dove è possibile inserire delle personalizzazioni che poi saranno salvate nel backup. Ad esempio sip\_custom.conf

Tutta la gestione telefonica del |product|, da come fare un trasferimento a come mettere in attesa, da cosa fare quando viene chiamata una coda a cosa deve fare un IVR, da come gestire le condizioni temporali a cosa fare quando viene lasciato un messaggio in voicemail, sono in files che iniziano con extensions\*

Nel file extensions.conf ci sono le funzionalità base, nel file extensions\_additional.conf le funzionalità configurate da interfaccia web (code, gruppi, rotte, etc.), il file extensions\_custom.conf invece serve a inserire funzionalità personalizzate.

Database Asterisk
-----------------

Il database di Asterisk, conosciuto anche come AstDB, è un meccanismo per conservare i dati di Asterisk su file. Si trova in

::
  /var/lib/asterisk/astdb.sqlite3

Files Musiche di Attesa
-----------------------

I files della categoria Predefinita delle ::ref:`Musiche di Attesa <musiche_di_attesa_ref_label>` si trovano in

::
  /var/lib/asterisk/mohmp3/

I files delle varie categorie configurate si trovano poi in sottocartelle nominate con il nome della categoria.

Files Caselle Vocali
--------------------

I files dei messaggi lasciati alle caselle vocali se configurati per essere conservati si trovano in

::
  /var/spool/asterisk/voicemail/

divisi in cartelle per ogni contesto e in sottocartelle con il numero di interno.

Files Registrazioni Chiamante
-----------------------------

I files delle registrazioni di chiamata sono in

::
  /var/spool/asterisk/monitor/

Files Registrazioni di Sistema
------------------------------

I files delle :ref:`Registrazioni di Sistema <registrazioni_di_sistema_ref_label>` si trovano in

::
  /var/lib/asterisk/sounds/custom/

I files delle registrazioni dei messaggi di sistema di |product| sono in

::
 /var/lib/asterisk/sounds

divisi in una cartella per ogni lingua.

Files Interfaccia Web
---------------------

I files dell'interfaccia web di |product| si trovano in

::
  /var/www/html/nethvoice/

Files Script Eseguibili
-----------------------

|product| nel flusso della chiamata può eseguire script che si devono trovare in

::
  /var/lib/asterisk/agi-bin/

Directory per creare una chiamata da file
-----------------------------------------

|product| crea una chiamata in base ad ogni file creato come da specifiche Asterisk presente in
::

 /var/spool/asterisk/outgoing
