.. _wizard2-section:

==================================
Wizard prima configurazione (beta)
==================================

.. warning::
    
    Le funzioni descritte in questa pagina sono disponibili in anteprima solo
    ai membri del |product| Quality Team

In questa sezione sono descritte le nuove funzionalità introdotte dal sistema di
provisioning basato sul progetto Tancredi. Le differenze rispetto
all'interfaccia precedente riguardano le seguenti pagine:

- :guilabel:`Dispositivi` è stata spostata in una sezione del menù a sé stante, composta dalle voci :guilabel:`Telefoni` e :guilabel:`Modelli`.

- :guilabel:`Configurazioni` è stata spostata in una sezione del menù a sé stante.

- :guilabel:`Gestione multipla telefoni` è stata aggiunta sotto la sezione :guilabel:`Applicazioni`.

.. _wizard2-telefoni:

Dispositivi
===========

In questa sezione viene richiesta la conferma di alcune impostazioni
fondamentali. 

- :guilabel:`Indirizzo centralino` può essere l'indirizzo IP o il nome 
  dell'host di |product|, se correttamente inserito nel DNS

- :guilabel:`Crittografia` per funzionare correttamente richiede che il sistema
  disponga di un certificato X509 valido per il nome host inserito in
  :guilabel:`Indirizzo centralino`

La scelta delle impostazioni dipende da come i telefoni dovranno raggiungere il
centralino.

- Se i telefoni sono tutti nella stessa rete del centralino (LAN),
  :guilabel:`Crittografia` può essere disabilitata e :guilabel:`Indirizzo
  centralino` può contenere un indirizzo IP.

- Se uno o più telefoni raggiungono il centralino tramite rete pubblica (WAN),
  come nel caso in cui il centralino sia ospitato su una VPS in cloud, allora
  :guilabel:`Crittografia` deve essere abilitata e :guilabel:`Indirizzo
  centralino` deve contenere il nome completo e presente nel DNS pubblico.

In ogni caso è possibile scegliere su ogni singolo telefono se la crittografia è
abilitata o meno, a patto che il certificato X509 del sistema sia valido. A
questo proposito fare riferimento a :ref:`wizard2-configurazioni`.

Una volta confermate le impostazioni, sarà possibile modificarle ulteriormente
dalla pagina :guilabel:`Dispositivi > Modelli`, pulsante :guilabel:`Impostazioni
di default`.

Telefoni
--------

TODO

.. _wizard2-modelli:

Modelli
-------

TODO

.. _wizard2-configurazioni:

Configurazioni
==============

TODO

.. _wizard2-telefoni-multi:

Gestione multipla telefoni
==========================

TODO
