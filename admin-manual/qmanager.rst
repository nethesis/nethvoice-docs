=================================
QManager (Supervisore delle Code)
=================================

.. _qmanager-ref-label:

QManager è l’applicazione sviluppata per il **«Supervisore delle Code»** e consente una gestione completa di tutte le code del |product|.

Per abilitarlo è necessario installare la relativa applicazione dal Software Center di |parent_product|.

Il QManager nasce per:

- avere in tempo reale i dati delle code monitorate

- essere avvisato in tempo reale di situazioni critiche (troppe chiamate, pochi agenti, attese elevate, etc.)

- interagire con lo stato degli agenti


Il QManager aggiunge un nuovo permesso nei profili di |product| che consente di discriminare per i vari utenti l'accesso alla sezione e le code che si vogliono monitorare.


Personalizzare le soglie degli allarmi
======================================

|product| include un demone che controlla lo stato delle code e scatena un allarme se alcuni parametri escono da valori predefiniti. Questi allarmi sono rivolti al manager del call center, che potrà così essere notificato tempestivamente nel caso in cui si verifichi un calo della qualità del servizio.

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

CheckInterval: secondi di intervallo tra i controlli alle code. Default 10

* ``Debug``: se impostato a ``True``, aumenta la verbosità del log su syslog (:file:`/var/log/messages`). Default: ``False``

EnableEmail: se impostato a True, abilita la notifica via email. Default False

EmailDestination: email di destinazione degli allarmi. È possibile specificare un solo indirizzo. Se vuota, le email sono inviate a voicemanagers@DOMAIN. Vuota di default.

* ``MaxCallPerOp``: chiamate massime per ogni operatore. Default ``3``.

* ``MaxCalls``: chiamate massime. Default: ``10``.

* ``MaxHoldtime``: attesa media massima della coda, espressa in secondi. Default: ``360``

* ``CallersMaxWait``: attesa massima del primo chiamante in coda, espressa in seconda. Default: ``360``

* ``status``: stato del servizio. Default: ``enabled.``
