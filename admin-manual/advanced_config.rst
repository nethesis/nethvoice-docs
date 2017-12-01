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


|product_cti|: disattivazione della modalità di Click2Call automatico
=====================================================================

necessità di sollevare la cornetta telefonica.

In alcuni scenari potrebbe essere utile disattivare la funzionalità, ad esempio nel caso in cui
il centralino telefonico è in cloud ed i telefoni siano in LAN dietro NAT. Per disattivare:

.. code-block:: bash

  config setprop nethcti-server AutoC2C disabled
  signal-event nethcti-server3-update

Per ripristinare il valore di default:

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