================
Backup & Restore
================


Backup
======

Il backup di |product| è completamente integrato nel backup di |parent_product|, sia per la parte di configurazione che di dati, vedi `qui <http://nethserver.docs.nethesis.it/it/latest/backup.html>`_.

Sia il backup della configurazione che il backup dei dati possono essere personalizzati seguendo questa documentazione: `Backup <http://nethserver.docs.nethesis.it/it/latest/backup.html>`_.


Restore
=======

Il ripristino dei dati deve essere fatto seguendo la documentazione di |parent_product|, vedi `Ripristino dati <http://nethserver.docs.nethesis.it/it/latest/backup.html#ripristino-dati>`_.


Disaster recovery
=================

Per il ripristino completo di un server dove era installato |product| vedere la documentazione relativa di |parent_product|: `Disaster recovery <http://nethserver.docs.nethesis.it/it/latest/backup.html>`_.

.. warning:: Dopo il restore, le app |product_cti| per Andorid e iOS non riceveranno più le notifiche finché non si registreranno di nuovo, ovvero finché non verranno aperte dall'utente.
