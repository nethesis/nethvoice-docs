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

E' possibile, quindi, utilizzare contemporaneamente solo una delle due versioni di g729, Open Source o Digium.

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
- Alcatel


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


