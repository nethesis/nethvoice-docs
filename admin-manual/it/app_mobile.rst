==========
App Mobile
==========

App Mobile è l'estensione di |product| per smartphone Android ed Apple e consente una rapida e facile configurazione degli apparati telefonici all'interno della rete. Attraverso la scannerizzazione del codice a barre in cui è presente il MAC address del telefono (sulla scatola del telefono o sul telefono stesso) è possibile effettuare il provisioning dei dispositivi, associando ad essi un interno ed un nome.


Installazione
=============

L'installazione dell'App Mobile avviene direttamente sullo smartphone a seconda della tua tipologia (Android, Apple) accedendo al relativo store. Basta cercare `nethvoice` o `nethvoice scan` sul relativo store e trovare l'applicazione pronta per l'installazione.

Il link diretto relativo ai vari store è il seguente:

 - `iOS <https://itunes.apple.com/us/app/nethvoice-scan/id1048079938?ls=1&mt=8>`_
 - `Android <https://play.google.com/store/apps/details?id=com.ionicframework.barcodevoice698406>`_


Configurazione
==============

Per accedere tramite l'App Mobile è necessario inserire le proprie credenziali del |product| e l'indirizzo del |product|.


Funzionamento
=============

L'App Mobile ha una sola vista, in cui sono concentrate tutte le informazioni e i dati richiesti. Appena aperta, cliccando sul pulsante `Scan MAC` si aprirà la visualizzazione dello scanner del codice a barre e posizionandosi sul relativo codice verrà identificato e successivamente inserito nel campo relativo della vista.

E' possibile inserire anche manualmente il MAC address qualora ci fossero problemi con il rilevamento del codice da fotocamera. L'unica accortezza da seguire è che deve esserci il carattere `-` o `:` ogni due caratteri del MAC address. Ad esempio:
 - 0089ef67ad15 => 00:89:ef:67:ad:15 oppure 00-89-ef-67-ad-15

In base al MAC address rilevato l'applicazione è in grado di capire la marca dell'apparato supportato che si è andati a scannerizzare, mostrando succesivamente i modelli disponibili. 

Una volta selezionato il modello relativo si può decidere se creare un nuovo interno da associare a quel telefono o scegliere un interno già disponibile.

Premendo il tasto `Save` si procede al salvataggio della configurazione sul centralino.

