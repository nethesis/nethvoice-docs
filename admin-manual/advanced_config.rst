Attivazione debug NethCTI
=========================

Di default il file di log riporta solamente messaggi di *warning* ed *errori*.
È possibile innalzare il livello di debug per avere maggiori informazioni:

.. code-block:: bash

  config setprop nethcti-server LogLevel info
  signal-event nethcti-server-update

.. warning::
  Innalzando il livello la dimensione del file di log aumenta rapidamente.

Per ripristinare il livello di default:

.. code-block:: bash

  config setprop nethcti-server LogLevel warn
  signal-event nethcti-server-update


Disattivazione della modalità di Click2Call automatico
======================================================

La modalità *Click2Call automatica* è attiva di default per tutti i :ref:`telefoni fisici supportati <telefoni_fisici_supportati>` e
offre la possibilità di pilotare le telefonate (chiamate e risposte) direttamente da NethCTI senza la
necessità di sollevare la cornetta telefonica.

In alcuni scenari potrebbe essere utile disattivare la funzionalità, ad esempio nel caso in cui
il centralino telefonico è in cloud ed i telefoni siano in LAN dietro NAT. Per disattivare:

.. code-block:: bash

  config setprop nethcti-server AutoC2C disabled
  signal-event nethcti-server-update

Per ripristinare il valore di default:

.. code-block:: bash

  config setprop nethcti-server AutoC2C enabled
  signal-event nethcti-server-update