============
Integrazioni
============


.. _integratio4:

vtenext 
=======

L'integrazione tra |product| e **vtenext** di default riguarda queste funzionalità:

1) permettere a |product| di risolvere in tempo reale le chiamate esterne in ingresso e/o in uscita tramite la *RESTAPI* di **vtenext** “get_caller_info”
2) permettere alla *rubrica centralizzata* di |product| di acquisire i contatti di **vtenext** tramite la *RESTAPI* di **vtenext** "query", serve se necessario a popolare ad esempio la rubrica di |product_cti| per effettuare delle chiamate partendo da |product_cti| e no da **vtenext**
3) notificare a **vtenext** l'arrivo di una chiamata esterna per l'utente tramite la *RESTAPI* di **vtenext** “notify_incoming_call”
4) consentire l'accesso al'elenco delle chiamate a **vtenext** per aggiungerle ai dati dei clienti
5) click to call dall'interfaccia di **vtenext**

Configurazione
--------------

1) copiare il file */usr/src/nethvoice/samples/lookup_vte.php* in */usr/src/nethvoice/lookup.d/* con il comando:
        
 cp /usr/src/nethvoice/samples/lookup_vte.php /usr/src/nethvoice/lookup.d/

  Modificare il file inserendo i valori di **$url** e **$authorization_token** con quelli forniti dagli amministratori di **vtenext**

2) copiare il file */usr/share/phonebooks/samples/vte.php* in */usr/share/phonebooks/scripts/* con il comando: 

 cp /usr/share/phonebooks/samples/vte.php /usr/share/phonebooks/scripts/

  Modificare il file inserendo i valori di **$url** e **$authorization_token** con quelli forniti dagli amministratori di **vtenext**

3) installare il pacchetto aggiuntivo *node-crm* con il comando 

 yum install node-crm

  copiare il file */usr/src/nethvoice/samples/vte_incoming_call.php* in */usr/src/nethvoice/*

  Modificare il file inserendo i valori di **$url** e **$authorization_token** con quelli forniti dagli amministratori di **vtenext**

  Aggiungere al backup il file */usr/src/nethvoice/vte_incoming_call.php* aggiungendo una riga al file */etc/backup-data.d/custom.include*

4) configurazione a carico dell'amministratore di **vtenext**, è necessario fornirgli le credenziali di una utenza creata ad hoc con il permesso :guilabel:`Telefono Avanzato` attivato  (è possibile usare la stessa anche al punto 5)

5) configurazione a carico dell'amministratore di **vtenext**, è necessario fornirgli le credenziali di una utenza creata ad hoc con il permesso :guilabel:`Telefono Avanzato` attivato  (è possibile usare la stessa anche al punto 4)
