========================
Configurazione Mediatrix
========================

Introduzione
------------

Gli apparati **Mediatrix** sono dei gateway SIP, sia isdn che analogici, alternativi ai Patton che possono essere recuperati se |product| va a sostituire un centralino che li utilizzava.

Configurazione tramite Interfaccia Web
--------------------------------------

La configurazione di un gateway Mediatrix per farlo funzionare con |product| è molto semplice da implementare.

Ecco i passi per configurare un gateway con quattro porte isdn come esempio, la configurazione di altri apparati è molto simile.

Presto aggiungeremo in questa pagina anche i files di configurazione per i gateway **Mediatrix** in modo tale che basterà caricare il file da interfaccia per configurare l'apparato.

Può essere utile effettuare il ripristino a factory default dell'apparato e successivamente aggiornare il firmware all'ultima versione.

- Collegarsi all'interfaccia web del Mediatrix http://ip_mediatrix le credenziali di default sono:  

::

  IP: 192.168.0.11
  Username: public
  Password:

- Andare su **SIP -> Gateways** e creare un gateway per ogni porta dell'apparato e collegarli alla porta di Uplink. Utilizzare una porta tcp diversa per ogni gateway.

.. image:: ../_static/mediatrix.png
               :alt: Configurazione Mediatrix

- In **SIP -> Servers** configurare l'ip del |product| alle voci Registrar Host, Proxy Host, Messaging Server Host con la sintassi IP:0 che indica la porta 5060

.. image:: ../_static/mediatrix_01.png
               :alt: Configurazione Mediatrix

- In **SIP -> Registrations** creare una unità di registrazione per ogni gateway configurato. Consigliamo di utilizzare username a partire da 4000 per poi facilitare la configurazione lato |product|.

.. image:: ../_static/mediatrix_02.png
               :alt: Configurazione Mediatrix

- In **SIP -> Authentication** creare una autenticazione per ogni gateway configurato. Consigliamo di utilizzare username a partire da 4000 con password uguale allo username per poi facilitare la configurazione lato |product|. In fase di creazione disabilitare Validate Realm.

.. image:: ../_static/mediatrix_03.png
               :alt: Configurazione Mediatrix
.. image:: ../_static/mediatrix_04.png
               :alt: Configurazione Mediatrix

- In **SIP -> Transport** assicurarsi che Add Sip Transport in Registration sia Enable.

.. image:: ../_static/mediatrix_05.png
               :alt: Configurazione Mediatrix

- In **Telephony -> Services** assicurarsi che per ogni Endpoint le tre voci Endpoint Specific siano a no.

.. image:: ../_static/mediatrix_06.png
               :alt: Configurazione Mediatrix

- In **ISDN -> Basic Rate Interface** configurare in caso di porte ISDN il tipo, punto-punto o punto-multipunto, in Connection Type e il massimo numero di canali in Maximum Active Calls, due per isdn ad esempio o una per analogiche.

.. image:: ../_static/mediatrix_07.png
               :alt: Configurazione Mediatrix

- Creare le rotte in **Call Router -> Route Config** per utilizzare le porte del Mediatrix. Servono una rotta in entrata e una rotta in uscita per ogni porta utilizzata. Le rotte in entrata vanno dalla porta fisica (isdn o analogica) al parte sip, le rotte in uscita l'esatto contrario. Fare attenzione ad associare alla porta la giusta destinazione sip e viceversa.

.. image:: ../_static/mediatrix_08.png
               :alt: Configurazione Mediatrix

Configurazione Lato |product|
-----------------------------

Per il gateway Mediatrix è necessario configurare :doc:`Fasci SIP <fasci_sip>` e :doc:`Rotte in Entrata <rotte_entrata>` per permettere a **NethVoice** di interagire con essi.

-  Le :doc:`Rotte in Entrata <rotte_entrata>` vanno create come al solito sul :ref:`Numero di Selezione Passante <numero_selezione_passante-label>`, che in questo caso sarà il numero della linea ISDN o della linea Analogica.

-  Inoltre è necessario creare un :doc:`Fascio SIP <fasci_sip>` per ogni linea configurata sul Mediatrix.

I :doc:`Fasci SIP <fasci_sip>` dovranno avere nome ad esempio 4001, 4002, 4003, 4004 (tanti quanti sono le linee) se il Mediatrix è stato configurato come descritto sopra, e dovranno riportare questa configurazione in `Dettagli Peer`: ::

  canreinvite=no
  nat=no
  context=from-pstn
  host=dynamic
  qualify=yes
  secret=4001
  type=friend
  username=4001
  insecure=very
  port=5060
  dtmfmode=inband

**Per i fasci successivi** (4002, 4003..) è necessario modificare `secret,username e port` di conseguenza, come è stato configurato sul Mediatrix, ad esempio se configurato come indicato sopra il :doc:`Fascio SIP <fasci_sip>` successivo avrà username e secret 4002 e port 5061.
