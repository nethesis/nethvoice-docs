=============
Installazione 
=============

Requisiti minimi
================

|product| è uno dei tanti prodotti installabile sulla base |parent_product|.


Installazione
=============

Per installare |product| quindi il primo passo è installare |parent_product|, per i requisiti minimi, la compatibilità hardware e le modalità di installazione fare riferimento alla documentazione 
specifica, vedi il manuale di |parent_product|: `Installazione <http://nethserver.docs.nethesis.it/it/latest/installation.html>`_.

Quando l'installazione di |parent_product| è stata completata con successo, per installare |product| è necessario prima registrare il server seguendo 
la procedura documentata: `Registrazione <http://nethserver.docs.nethesis.it/it/latest/registration.html>`_.

Registrato il server, dalla gestione pacchetti, vedi `qui <http://nethserver.docs.nethesis.it/it/latest/packages.html>`_, è possibile installare |product| e tutti i moduli correlati opzionali, come ad esempio il |product_cti|.

Una volta avviata l'installazione il server scaricherà i pacchetti occorrenti da vari repository per poi automaticamente installarli ed effettuare le configurazioni necessarie.

Terminata questa fase, |product| sarà pronto per essere utilizzato.

Il pannello di configurazione di |product| è raggiungibile *dalle reti locali e dalle reti fidate* all'indirizzo

https://nomeserver/|product_command|

dove per *nomeserver* si intende il nome (anche seguito dal dominio) dato al |product| in fase di installazione.

L'accesso è consentito anche sostituendo a *nomeserver* l'ip del |product|.

L'accesso è garantito di default all'utente admin che ha come password di default *Nethesis,1234*


.. _accesso_esterno_ref_label:

Accesso Esterno
===============

Interfaccia Web
---------------

Per accedere da una rete diversa da quelle locali o fidate all'interfaccia web di amministrazione di |product|, aggiungere la rete di provenienza nel menù *Accesso centralino-> Accesso interfaccia web* di |parent_product|.


Servizi
--------

|product| consente di aprire a reti esterne il protocollo IAX, il protocollo WebRTC e la WebSocket per l'accesso al |product_cti|.

.. warning:: L'apertura verso l'esterno del protocollo SIP è decisamente sconsigliata e per questo non prevista da interfaccia.

Per aprire IAX, WebRTC e la WebSocket accedere all'interfaccia di amministrazione di |parent_product| nel menù *Accesso centralino-> Accesso esterno*.
