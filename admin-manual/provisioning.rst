============
Provisioning
============

.. _provisioning_impostazione_avanzate_terminali_ref_label:

Provisioning Impostazione Avanzate Terminali
============================================


Descrizione
-----------

Il modulo Impostazioni Avanzate fornisce le configurazioni base del Provisioning.

Non ci dovrebbe essere motivo di effettuare cambiamenti in questo modulo in quanto viene pre-caricata una configurazione ottimale.

Il modulo ha diverse funzionalità, le configurazioni di base, l'associazione dei mac address monitorati ai produttori di apparecchi telefonici (OUI Manager), un editor per modificare i template caricati dei telefoni, importazione/esportazione lista terminali, importazione/esportazione pacchetti telefoni, mostra/nascondi marche modelli.

Configurazioni
--------------

Gestione dei parametri generali del Provisioning di |product|.

Questi parametri sono già stati configurati cercando di ottenere una configurazione ottimale e non dovrebbero avere bisogno di cambiamenti.

OUI Manager
-----------

Associazione tra i mac address ed i produttori di apparecchi telefonici.

Il Provisioning si basa su queste associazioni per effettuare l'auto-discovery tramite il modulo :ref:`Wizard Provisioning <wizard_provisioning_ref_label>`.

Editor Opzioni/Configurazione Prodotto
--------------------------------------

Questa parte del modulo consente di modificare i template pre caricati per effettuare dei cambiamenti che poi verranno applicati a tutti i telefoni del modello prescelto.

I template posso essere formati da più files, che si trovano una volta selezionato il modello, nell'elenco a sinistra, sotto *File Configurazioni Locale*.

Importa/Esporta Mia Lista Terminali
-----------------------------------

Possibilità di importare una lista di apparati per caricare le associazioni mac address, marca, modello, interno e linee direttamente sul |product| non passando per il :ref:`Wizard Provisioning <wizard_provisioning_ref_label>`.

E' possibile anche esportare le associazioni già caricate.

Carica/Esporta Manuale Modelli Terminali
----------------------------------------

Parte del modulo che da la possibilità di caricare pacchetti di configurazione per modelli di telefoni.

I pacchetti sono già stati caricati, consigliamo di **NON** utilizzare questa parte se non dietro specifiche indicazioni.

Mostra/Nascondi Marche/Modelli
------------------------------

Elenco dei pacchetti di configurazione dei telefoni caricati e possibilità di disattivare quelli non utili, consigliamo di **NON** utilizzare questa parte se non dietro nostre indicazioni.

.. _provisioning_configurazioni_terminali_ref_label:

Provisioning Configurazioni Terminali
=====================================

Descrizione
-----------

Il modulo Configurazione Terminali serve semplicemente ad avere l'elenco delle configurazioni dei modelli di telefoni che sono caricate su |product| per il :ref:`Provisioning  <wizard_provisioning_ref_label>`.

.. _provisioning_lista_terminali_ref_label:

Provisioning Lista Terminali
============================


Descrizione
-----------

Il modulo Lista Terminali fornisce l'elenco di tutti i telefoni gestiti dal Provisioning e permette di effettuare modifiche alle configurazioni già applicate.

E' possibile agire direttamente sul file di configurazione, oppure cambiare l'interno e/o il modello assegnato al telefono.

Se è stato creato un template personalizzato di configurazione tramite il modulo :ref:`Gestione Template Terminali <provisioning_gestione_template_terminali_ref_label>`.

Da questo modulo è anche possibile effettuare operazioni su tutti i telefoni di una certa marca o di un certo modello, come ad esempio riavviarli o riconfigurarli tutti.

Configurazione
--------------

Parte del modulo per ricercare in rete nuovi apparecchi telefoni e per caricare a mano delle assegnazioni mac address, marca, modello interno.

Consigliamo di utilizzare il :ref:`Wizard Provisioning <wizard_provisioning_ref_label>` per effettuare più agevolmente queste operazioni.

Elenco dei terminali configurati tramite il Provisioning.

Cliccando sul simbolo nella colonna Specifiche è possibile modificare la configurazione delle linee del telefono.

Facendo una selezione multipla è possibile modificare più telefoni contemporaneamente usando i tasti funzione sotto l'elenco(Opzioni Telefono/i Selezionate).

Le funzionalità previste sono la cancellazione, la rigenerazione delle configurazioni o l'aggiornamento di marca e modello per i telefoni
selezionati.

E' anche possibile agire su tutti i telefono in elenco senza la necessità di selezionarli tutti, utilizzando i tasti funzione più sotto(Opzioni Globali Telefoni), potendo rigenerare tutte le configurazioni, riavviare una marca specifica, o cambiare il template di configurazione o per marca o per modello.

Cliccando sul simbolo nella colonna Modifica, la configurazione viene caricata nella parte alta del modulo dove è possibile modificare nello specifico tutta il template creato dal provisioning (cliccando su sul simbolo di modifica), modificare il modello del telefono, le linee e l'interno associato.

Nell'elenco cliccando sul simbolo nella colonna Modifica, la configurazione viene caricata nella parte alta del modulo dove è possibile modificare nello specifico tutta il template creato dal provisioning (cliccando su sul simbolo di modifica), modificare il modello del telefono, le linee e l'interno associato.

E' possibile anche, in questo caso, cambiare il template di configurazione associato al telefono, vengono proposti tutti i template creati oltre a quello di default per la marca/modello selezionati.  

.. warning:: Ogni configurazione effettuata nei vari moduli del Provisioning ha bisogno per essere attivata che venga cliccato il pulsante **Applica Modifiche**

.. _provisioning_gestione_template_terminali_ref_label:

Provisioning Gestione Template Terminali
========================================

Descrizione
-----------

Il modulo visualizza la lista dei template creati per i vari modelli di telefoni sottoposti al Provisioning.

In questo modulo si possono modificare i template creati per i vari telefoni ed è possibile creare dei template personalizzati partendo dai template caricati su |product| per poi assegnarli ai vari telefoni utilizzando il modulo :ref:`Lista Terminali <provisioning_lista_terminali_ref_label>`.

Configurazione
--------------

Elenco di ogni template creato dal |product|.

Nella lista si trovano tutti i template generati per i telefoni rilevati utilizzando il modulo :ref:`Wizard Provisioning <wizard_provisioning_ref_label>`, con in aggiunta tutti i template personalizzati.

Per creare un template personalizzato basta dargli un nome per riconoscerlo e scegliere da che base partire selezionando marca e modello.

Se, invece, si clicca sul pulsante nella colonna Modifica si apre l'interfaccia per la configurazione del template.

L'interfaccia cerca di riprodurre quella del telefono selezionato per quanto possibile, quindi varia da modello a modello.

E' possibile modificare le opzioni più comuni che vengono proposte, oppure andare nel dettaglio cliccando sui pulsanti di modifica per accedere direttamente ai file del template.

