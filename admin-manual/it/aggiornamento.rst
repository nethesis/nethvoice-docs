=============
Aggiornamento
=============

|product| ha gli aggiornamenti automatici abilitati di default, questo vuol dire che ogni notte verranno scaricati e installati eventuali aggiornamenti.

|product| però continuerà a rimanere in esecuzione con la configurazione precedente, per attivare gli aggiornamenti sarà necessario cliccare sul pulsante Applica Modifiche.

Solo in caso di aggiornamento di **Asterisk** o di un componente correlato sarà necessario oltre a cliccare sul pulsante Applica Modifiche dare il comando

 |product_command| restart

che comporta il riavvio di tutti i servizi, con caduta delle eventuali chiamate in corso, di |product| facendolo partire con le versioni aggiornate.

Per forzare gli aggiornamenti utilizzare il comando 

 yum update


Aggiornamento |product| installato su base differente
=====================================================

L'aggiornamento di una versione di |product| installata su base differente da |parent_product| è possibile tramite la procedura di migrazione.
La migrazione è il processo che consente di convertire un’installazione SME Server/|product_service_old| (:dfn:`origine`) in un nuovo server |parent_product| (:dfn:`destinazione`).

.. warning:: L'unico prerequisito è che la versione di |product| nel server di origine sia la 11.4 

Tutta la procedura da seguire è documentata qui `Migrazione <http://nethservice.docs.nethesis.it/it/latest/migration.html>`_.

