|product|: installazione codec g729
===================================

Per installare ed attivare il codec g729 Open Source ecco la procedura (comporta il riavvio di Asterisk e quindi l'eventuale caduta di chiamate in corso):

.. code-block:: bash

  cd /usr/lib64/asterisk/modules/
  wget http://asterisk.hosting.lv/bin/codec_g729-ast130-gcc4-glibc-x86_64-pentium4.so
  mv codec_g729-ast130-gcc4-glibc-x86_64-pentium4.so codec_g729.so
  chmod 755 codec_g729.so
  systemctl restart asterisk

Il codec g729 Open Source non è compatibile con la versione a pagamento di Digium, che si può installare seguendo la procedura che vi forniranno con l'acquisto.

É possibile, quindi, utilizzare contemporaneamente solo una delle due versioni di g729, Open Source o Digium.

|product|: configurazione dell'IP locale
========================================

In fase di provisioning, l'IP usato come IP del centralino è l'IP della prima rete ``green`` (rete locale). 
Questo può essere modificato da linea di comando, per esempio se si hanno :index:`reti green multiple`.
Se si desidera forzare un determinato indirizzo IP, esempio ``192.168.123.11``, utilizzare i seguenti comandi: ::

  config setprop nethvoice LocalIP 192.168.123.11
  signal-event nethserver-nethvoice14-update

|product|: configurazione del transport PJSIP
=============================================

In |product| il modulo `chan_pjsip` di Asterisk è configurato per stare in ascolto su tutti gli indirizzi di tutte le reti green.
È possibile che sia necessario cambiare questa configurazione in situazioni particolari.
Se si desidera che chan_pjsip stia in ascolto anche sulle RED ed i loro alias, eseguire i comandi: ::

  config setprop nethvoice PJSIPBind all
  signal-event nethserver-nethvoice14-update

Se invece si desidera fare delle personalizzazioni maggiori, come ad esempio escludere una rete green, è possibile farlo dall'interfaccia della configurazione avanzata:
:menuselection:`Asterisk SIP Settings --> Chan PJSIP Settings`.
Sarà poi necessario abilitare le configurazioni avanzate :guilabel:`Show Advanced Settings` e fare le opportune modifiche. 


.. note::

   Se la visualizzazione delle configurazioni avanzate è abilitata, le impostazioni di transport **non** 
   verranno più sovrascritte in caso di aggiornamento o modifica delle interfacce di rete.


|product|: configurazione rubrica
=================================

La rubrica di |product| è la Rubrica Centralizzata di |product_service|. Vedere nella documentazione di |product_service| come popolarla e integrarla con la rubrica del |product_cti| e i :ref:`Numeri Rapidi <rapidcode-ref-label>`.

I telefoni vengono collegati alla rubrica di |product| automaticamente se configurati tramite il provisioning, altrimenti per i modelli che lo supportano è possibile configurare una rubrica di tipo LDAP.
I parametri da utilizzare per i vari modelli sono:

Parametri comuni
----------------

Indirizzo del server:
  ``Indirizzo IP o nome centralino``

Base:
  ``dc=phonebook,dc=nh``

Attributi nome LDAP:
  ``cn o``

Attributi numero LDAP:
  ``telephoneNumber mobile homePhone``

Porta:
  ``389`` per |parent_product| 6

  ``10389`` per |parent_product| 7

Filtro ricerca nomi LDAP:
  ``(&(telephoneNumber=*)(sn=%))`` per |parent_product| 6

  ``(|(cn=%)(o=%))`` per |parent_product| 7

Filtro ricerca numeri LDAP:
  ``(&(telephoneNumber=%)(sn=*))`` per |parent_product| 6

  ``(|(telephoneNumber=%)(mobile=%)(homePhone=%))`` per |parent_product| 7

Protocollo:
  ``Version3``


Sangoma
-------

Parametri aggiuntivi:

* Ricerca LDAP per chiamate in ingresso: Off
* Risultati di ordinamento LDAP: On

Snom
----

Parametri aggiuntivi:

* LDAP su TLS: off
* Ordina Risultati: on
* Predici Testo: on
* Fai una query iniziale: on

Yealink
-------

Parametri aggiuntivi:

* Battute massime (1-32000): 50
* Mostra nome LDAP: %cn %o
* Ricerca LDAP per chiamate in ingresso: Disabilitato
* Ricerca LDAP in uscita: Disabilitato
* Risultati di ordinamento LDAP: Abilitato





|product|: collegamenti remoti
==============================

Due o più |product| remoti, cioè non nella stessa rete posso essere collegati tra di loro tramite dei fasci iax.  Si utilizza il protocollo IAX sia per le sue caratteristiche di semplicità, richiede solo la porta 4569 UDP, sia per il brillante comportamento in caso di nat, sia per le performance su chiamate multiple.

Se possibile è sempre indicato collegare le varie sedi remote con vpn tra di loro, in modo da far passare il traffico voce su di esse.

Configurazione Fasci IAX
------------------------

Avendo permesso, tramite o la vpn e/o l'eventuale configurazione delle reti fidate, il traffico tra i due |product|, bisogna a questo punto configurare i fasci iax. In pratica i centralini per interfacciarsi devono scambiarsi uno username e password che autorizza il collegamento.

.. warning:: L'utente è univoco, deve essere utilizzato per un solo collegamento, in caso di collegamento tra diversi |product| utilizzare username diversi per ogni fascio IAX.

Ecco un esempio pratico:

.. note:: Nel caso la VPN sia instaurata direttamente dal |product|, sul centralino remoto può essere necessario indicare l'ip del punto punto della vpn e non l'indirizzo della rete green.

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
  context=from-intracompany

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
  context=from-intracompany

Configurazione Rotte in Uscita
------------------------------

L'ultima configurazione da effettuare è nelle rotte in uscita. Quello che dobbiamo fare è indicare al |product| come raggiungere gli interni remoti.

Le possibilità possono essere anche qui due:

Interni delle due sedi sovrapposti
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se i due |product| hanno la numerazione di interni sovrapposta, stessi interni in entrambi i centralini, si deve creare una rotta in uscita con il pattern di chiamata che includa gli interni remoti e un prefisso.

Il prefisso fa instradare la chiamata non per l'interno locale ma per l'interno remoto.

Ovviamente l'unico fascio da utilizzare sarà quello IAX precedentemente creato per il collegamento infra sede.

Ricordarsi di spuntare **Rotta Intra-Aziendale** se si vuole inviare al centralino remoto anche il nome del chiamante oltre che il numero, in modo che il chiamato sul display del telefono lo visualizzi.

Interni delle due sedi non sovrapposti
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nel caso che gli interni dei due |product| collegati siano ben distinti, non ci si deve preoccupare di distinguere con un prefisso la rotta in uscita.

É necessario quindi creare una rotta con il pattern degli interni remoti e indicare il fascio iax di collegamento precedentemente creato.

Ricordarsi di spuntare **Rotta Intra-Aziendale** se si vuole inviare al centralino remoto anche il nome del chiamante oltre che il numero, in modo che il chiamato sul display del telefono lo visualizzi.


|product_cti|: attivazione debug
================================

Di default il file di log riporta solamente messaggi di *warning* ed *errori*.
È possibile innalzare il livello di debug per avere maggiori informazioni:

.. code-block:: bash

  config setprop nethcti-server LogLevel info
  signal-event nethcti-server3-update

.. warning::
  Innalzando il livello la dimensione del file di log aumenta rapidamente.

Per ripristinare il livello di default:

.. code-block:: bash

  config setprop nethcti-server LogLevel warn
  signal-event nethcti-server3-update


|product_cti|: telefoni con modalità Click2Call automatico
=====================================================================

Quando si utilizza |product_cti| con associato un telefono fisico, è
necessario sollevare la cornetta quando si effettuano chiamate.
La modalità *"Click2Call automatico"* consente di bypassare l'uso della
cornetta sfruttando ad esempio il vivavoce del telefono o delle cuffie
audio direttamente indossate dall'utente.

La modalità è attiva di default e questa è la lista dei telefoni
supportati:

- Yealink
- Snom
- Sangoma
- Fanvil


Disattivazione della modalità Click2Call automatico
---------------------------------------------------

In alcuni scenari potrebbe essere utile disattivare la funzionalità,
ad esempio nel caso in cui il centralino telefonico fosse in cloud
e i telefoni siano in LAN dietro NAT. Per la disattivazione eseguire
i comandi:

.. code-block:: bash

  config setprop nethcti-server AutoC2C disabled
  signal-event nethcti-server3-update

Per la riattivazione:

.. code-block:: bash

  config setprop nethcti-server AutoC2C enabled
  signal-event nethcti-server3-update


|product_cti|: utilizzo di un server chat esterno
=================================================

È possibile configurare un server chat presente su un'altra macchina:

.. code-block:: bash

  config setprop nethcti-server JabberUrl <BOSH_URL>
  signal-event nethcti-server3-update

Per esempio:

.. code-block:: bash

  config setprop nethcti-server JabberUrl https://nethserver.mydomain.it/http-bind
  signal-event nethcti-server3-update

Per ripristinare il default:

.. code-block:: bash

  config setprop nethcti-server JabberUrl ""
  signal-event nethcti-server3-update

.. note::
  Il server chat specificato deve supportare `XMPP <https://en.wikipedia.org/wiki/XMPP>`_ su protocollo `BOSH <https://en.wikipedia.org/wiki/BOSH_(protocol)>`_.
  `NethServer <http://docs.nethserver.org/it/v7/chat.html>`_ lo supporta di default.


|product_cti|: configurazione di un prefisso telefonico
=======================================================

È possibile configurare un prefisso telefonico per qualsiasi chiamata:

.. code-block:: bash

  config setprop nethcti-server Prefix <PREFISSO>
  signal-event nethcti-server3-update


Per ripristinare il default:

.. code-block:: bash

  config setprop nethcti-server Prefix ""
  signal-event nethcti-server3-update


|product_cti|: configurazione Softphone WebRTC
==============================================

Il softphone WebRTC utilizza il `Gateway Janus <https://github.com/meetecho/janus-gateway>`_
installato direttamente nel centralino telefonico.

Janus-gateway può operare in tre differenti modalità di NAT:

1. STUN (default)
2. ICE
3. 1:1 (NAT)

Per la configurazione del NAT e delle opzioni, sono disponibili quattro proprietà sotto la
chiave *janus-gateway* del database di configurazione:

1. NatMode: <stun|ice|1:1>
2. StunServer: indirizzo del server STUN da usare. Il default è *stun1.l.google.com*. Viene ignorato se la modalità non è STUN
3. StunPort: porta del server STUN. Il default è 19302. Viene ignorato se la modalità non è STUN
4. PublicIP: è l'indirizzo IP pubblico del server su cui è in esecuzione janus-gateway. Viene ignorato se la modalità non è 1:1

In alcuni scenari d'utilizzo l'audio delle telefonate potrebbe non funzionare e conseguentemente le chiamate
vengono terminate automaticamente dal centralino dopo un certo intervallo temporale. In questi casi
è necessario configurare correttamente il WebRTC in base all'architettura di rete utilizzata.

*Esempio*

Nel caso si utilizzi un centralino in cloud dietro NAT, è necessario configurare il WebRTC come segue:

.. code-block:: bash

  config setprop janus-gateway NatMode 1:1
  config setprop janus-gateway PublicIP <DOMAIN OR PUBLIC IP>
  signal-event nethserver-janus-update


|product_cti|: disattivazione della gestione eventi dei fasci
=============================================================

È possibile disabilitare la gestione degli eventi dei fasci all'interno di |product_cti| Server come segue:

.. code-block:: bash

  config setprop nethcti-server TrunksEvents "disabled"
  signal-event nethcti-server3-update

Per riabilitarli:

.. code-block:: bash

  config setprop nethcti-server TrunksEvents "enabled"
  signal-event nethcti-server3-update

.. note::
  I fasci rimangono pienamente funzionanti: la disattivazione riguarda solamente |product_cti| Server.

  Tale disattivazione comporta solamente la non visualizzazione delle chiamate nella schermata dei "fasci" lato |product_cti| Client.

|product_cti|: effettuare chiamate in maniera non autenticata
=============================================================

|product_cti| offre la possibilità di fare telefonate invocando una particolare API senza autenticazione: :code:`astproxy/unauthe_call.`

**Questa funzionalità è disabilitata di default per motivi di sicurezza.**

Per l'attivazione eseguire:

.. code-block:: bash

  config setprop nethcti-server UnautheCall enabled
  signal-event nethcti-server3-update

per disabilitarla:

.. code-block:: bash

  config setprop nethcti-server UnautheCall disabled
  signal-event nethcti-server3-update

Una volta attivata è possibile effettuare una telefonata invocando la REST API `astproxy/unauthe_call. <https://nethvoice.docs.nethesis.it/en/v14/cti_dev.html#elenco-delle-api>`_

Di default solamente gli indirizzi appartenenti alle "Trusted Networks" sono abilitati all'utilizzo della API.
È comunque possibile personalizzare tale lista eseguendo:

.. code-block:: bash

  config setprop nethcti-server UnautheCallAddress "192.168.5.60 192.168.6.60/255.255.255.0 192.168.4.0/24"
  signal-event nethcti-server3-update

È consentito l'inserimento di campi multipli separati da uno spazio vuoto, è possibile specificare un singolo indirizzo
IP o un range, sia tramite netmask sia utilizzando la notazione CIDR.

.. warning:: Se la funzionalità viene abilitata, chiunque potrà eseguire telefonate da qualsiasi interno verso qualsiasi destinazione tramite richieste HTTP POST, ma solo dagli indirizzi indicati nella lista ottenuta col seguente comando :code:`"config getprop nethcti-server UnautheCallAddress".`

|product_cti|: disabilitare l'autenticazione
============================================

.. warning:: L'autenticazione è ABILITATA di default. Una volta disabilitata, sarà possibile eseguire il login a |product_cti| inserendo solamente il nome utente!

È possibile disabilitare l'autenticazione nella seguente maniera:

.. code-block:: bash

  config setprop nethcti AuthenticationEnabled false
  config setprop nethcti-server AuthenticationEnabled false
  signal-event nethcti3-update
  signal-event nethcti-server3-update

per riabilitarla:

.. code-block:: bash

  config setprop nethcti AuthenticationEnabled true
  config setprop nethcti-server AuthenticationEnabled true
  signal-event nethcti3-update
  signal-event nethcti-server3-update

|product_cti|: personalizzare il messaggio di fallito login per utenti non configurati
======================================================================================

Un utente non configurato **non** ha il permesso di accedere a |product_cti|.
In questo caso è possibile personalizzare il messaggio di warning visualizzato dopo un tentativo di login.
Procedere nella seguente maniera:

1. creare il template custom del file `/usr/share/cti/customizable/login-user-noconfig.html`:

.. code-block:: bash

  mkdir -p /etc/e-smith/templates-custom/usr/share/cti/customizable/login-user-noconfig.html
  cp /etc/e-smith/templates/usr/share/cti/customizable/login-user-noconfig.html/10base /etc/e-smith/templates-custom/usr/share/cti/customizable/login-user-noconfig.html/

2. personalizzare il contenuto del template custom `/etc/e-smith/templates-custom/usr/share/cti/customizable/login-user-noconfig.html/10base`
3. eseguire l'evento `nethcti3-update`

.. code-block:: bash

  signal-event nethcti3-update

Per ripristinare il messaggio originale:

.. code-block:: bash

  rm -f /etc/e-smith/templates-custom/usr/share/cti/customizable/login-user-noconfig.html/10base
  signal-event nethcti3-update


|product_cti|: eseguire uno script al termine di una chiamata
=============================================================

È possibile configurare NethCTI Server per eseguire uno script al termine di ogni chiamata.
Lo script verrà invocato tramite i seguenti parametri così come ricevuti da Asterisk stesso:

.. code-block:: bash

  "source, channel, endtime, duration, amaflags, uniqueid, callerid, starttime, answertime, destination, disposition, lastapplication, billableseconds, destinationcontext, destinationchannel"

Esempio:

.. code-block:: bash
  
  ./<SCRIPT_PATH> '200' 'PJSIP/200-00000000' '2019-01-17 18:05:13' '10' 'DOCUMENTATION' '1547744703.0' '"Alessandro Polidori" <200>' '2019-01-17 18:05:03' '2019-01-17 18:05:09' '201' 'ANSWERED' 'Dial' '3' 'ext-local' 'PJSIP/201-00000001' 


Per attivare l'esecuzione di uno script eseguire:

.. code-block:: bash

  config setprop nethcti-server CdrScript <SCRIPT_PATH>
  config setprop nethcti-server CdrScriptTimeout 5000
  signal-event nethcti-server3-update

Il secondo comando è opzionale e consente di stabilire un timeout (espresso in msec) per l'esecuzione dello script: il default è 5 secondi.

Per disattivarlo eseguire:

.. code-block:: bash

  config setprop nethcti-server CdrScript ""
  config setprop nethcti-server CdrScriptTimeout 5000
  signal-event nethcti-server3-update


.. note:: Lo script deve essere eseguibile dall'utente "asterisk" e si consiglia di configurare opportunamente i permessi del file.

|product_cti|: personalizzare le soglie degli allarmi
=====================================================

|product| include un demone che controlla lo stato delle code e lancia un allarme se alcuni parametri escono da valori predefiniti. Questi allarmi sono rivolti al manager del call center, che potrà così essere notificato tempestivamente nel caso in cui ci sia un calo della qualità del servizio.

Di default, le notifiche vengono mostrate nella dashboard del QManager (Supervisore delle code) di |product_cti|, ma è possibile anche riceverle via email

Gli allarmi generati sono:

- numero di agenti insufficiente nella coda: la notifica viene inviata se ci sono più di *MaxCallPerOp* (default 3) chiamate per ogni operatore
- tempo di attesa medio elevato sulla coda: la notifica viene inviata se il tempo medio di attesa in coda è maggiore di *MaxHoldtime* (default 360s)
- carico elevato sulla coda: la notifica viene inviata se ci sono più di *MaxCalls* (default 10) chiamate in attesa e il tempo media di attesa in coda è maggiore di *MaxHoldtime.*
- numero elevato di chiamate in attesa nella coda: la notifica viene inviata se ci sono più di *MaxCalls* chiamate in attesa e il tempo di attesa della prima chiamata è maggiore di *CallersMaxWait* (default 360s).

È possibile personalizzare i valori delle soglie di ciascun allarme modificando i valori nel DB di configurazione con i comandi:

.. code-block:: bash

  config setprop nethvoice-alerts <PROP> <VALUE>
  expand-template /etc/nethvoice-alerts.cfg
  systemctl restart nethvoice-alerts


I parametri modificabili sono:

CheckInterval: secondi di intervallo tra I controlli alle code. Default 10

Debug: se impostato a True, aumenta la verbosità del log su syslog (/var/log/messages). Default: False

EnableEmail: se impostato a True, abilita la notifica via email. Default False

EmailDestination: email di destinazione degli allarmi. Se vuota, le email sono inviate a voicemanages@DOMAIN. Vuota di default.

MaxCallPerOp: chiamate massime per ogni operatore. Default 3.

MaxCalls: chiamate massime. Default 10.

MaxHoldtime: attesa media massima della coda. Default 360 secondi.

CallersMaxWait: attesa massima del primo chiamante in coda. Default 360 secondi.

status: stato del servizio. Default enabled.

