===================
Configurazione Base
===================

.. _accesso_ref_label:

Accesso
=======

Il pannello di configurazione di |product| è raggiungibile all'indirizzo

https://nomeserver/|product_command|

dove per *nomeserver* si intende il nome (anche seguito dal dominio) dato al |product| in fase di installazione.

L'accesso è consentito anche sostituendo a *nomeserver* l'ip del |product|.

L'accesso è garantito di default all'utente admin che viene configurato durante l'installazione.

E' possibile poi accedere anche con altri utenti a patto che questi siano membri del gruppo **voicemanager** e che siano stati abilitati tramite il modulo :ref:`Amministratori <amministratori_ref_label>`.


.. _rete_ref_label:

Rete
====

Configurazione di Rete 
----------------------

Il |product|, essendo un centralino Voip, svolge le tutte le sue funzionalità via rete.

Tramite la rete comunica con gli apparecchi telefonici, con i gateway delle risorse telefoniche (Patton, Portech, Provider Voip...), tramite la rete si aggiorna e comunica al Centro Servizi il suo stato di funzionamento.

|product| non ha necessità di avere una rete dedicata alle comunicazioni Voip in praticamente nessun caso, può essere consigliata solo in caso di traffico elevatissimo e di switch non in grado di gestirlo insieme a tutto il resto.

Il |product|, quindi, può essere inserito tranquillamente in una rete preesistente insieme a tutti gli apparecchi e gateway telefonici.

|product| essendo un server a tutti gli effetti ha bisogno di un ip statico sulla sua interfaccia di rete.


Configurazione di Rete Gateway Telefonici e Telefoni
----------------------------------------------------

I gateway telefonici vanno preferibilmente configurati con un ip statico fuori da un eventuale range dhcp.

Questo li preserva da eventuali problemi di malfunzionamento del servizio dhcp e da possibili conflitti di indirizzo ip, in quanto se ci fossero minerebbero il funzionamento sostanziale del |product| essendo i gestori delle sorgenti telefoniche.

I telefoni, invece, non hanno necessità pratiche di un indirizzo statico, anzi lasciarli in dhcp permette di utilizzare appieno il :ref:`Provisioning <provisioning_ref_label>`.

Se, nonostante tutto, si ha l'esigenza di avere i telefoni con ip fisso, consigliamo di lasciarli in dhcp e configurare degli assegnamenti statici; è anche possibile con i telefoni in dhcp, configurare con il :ref:`Provisioning <provisioning_ref_label>` che prendano ip statici a configurazione ultimata, non è, però, una soluzione molto comoda perché richiede molto lavoro per ogni telefono.


.. _funzionalita_base_ref_label:

Funzionalità Base
=================


.. _interni_ref_label:

Interni
=======


.. _casella_vocale_ref_label:

Casella Vocale
==============


.. _fasci_ref_label:

Fasci
=====


.. _gestione_chiamata_in_entrata_ref_label:

Gestione Chiamata in Entrata
============================


.. _gestione_chiamata_in_uscita_ref_label:

Gestione Chiamata in Uscita
============================


.. _chiamata_video_ref_label:

Chiamata Video
==============


.. _rubrica_ref_label:

Rubrica
=======


.. _registrazione_chiamate_ref_label:

Registrazione Chiamate
======================


.. _fax_ref_label:

Fax
===


.. _backup_e_restore_ref_label:

Backup e Restore
================

