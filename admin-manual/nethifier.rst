===================
|product_nethifier|
===================

|product_nethifier| Windows Integration è l'applicazione per Microsoft Windows che consente
l'integrazione di |product| con il desktop Windows. In particolare consente la visualizzazione
di popup di notifica nel desktop in corrispondenza della ricezione di telefonate dirette a un
qualsiasi interno telefonico dell'utente.

Versioni di Windows compatibili: Windows 7 (64 bit), Windows 8 e Windows 10.

Per la personalizzazione dei popup seguire la :ref:`documentazione <custom-nethifier-label>`.

Requisiti
=========

- .NET Framework 4.5.
- Server |product| 3.x.
- Il pc su cui è in esecuzione |product_nethifier| deve risolvere l'indirizzo ``nomenethvoice.dominio``.

.. note:: Per ottenere il nome di dominio si può utilizzare il comando ``hostname -f``

Download
========

Il download è disponibile `nell'area relativa <http://helpdesk.nethesis.it/solution/folders/3000014059)>`_.

Installazione
=============

È sufficiente effettuare il download dell'installer
ed eseguirlo. Terminata la fase d'installazione il programma verrà
avviato automaticamente.

Per poter essere eseguito |product_nethifier| necessita di privilegi amministrativi perciò è necessario ricordarsi di installarlo utilizzando l'opzione "Esegui come amministratore".

.. warning:: Durante l'installazione su Windows 10 verrà mostrato un avviso di sicurezza di Windows Defender SmartScreen. È sufficiente cliccare la voce "Esegui comunque" e continuare nelle fasi successive. Qua maggiori `informazioni <https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-set-individual-device>`_.

Configurazione
==============

È necessaria solamente la prima volta. I dati da inserire sono:

-  indirizzo del server (nome o IP)
-  credenziali dell'utente

È necessario salvare i dati cliccando il pulsante apposito in maniera tale da non doverli più reinserire
agli avvii successivi. È anche possibile attivare l'esecuzione automatica di |product_nethifier| all'avvio di Windows.

Combinazione tasti chiamata
---------------------------

È possibile personalizzare la combinazione di tasti usati per effettuare una chiamata o per ricomporre l'ultimo numero, tramite la scheda "Dialer Hotkey" delle opzioni.

Rimozione
=========

È sufficiente aprire il menu *Programmi* di Windows e cliccare la voce
"|product_nethifier| -> Uninstall".

.. _custom-nethifier-label:

Personalizzazione
=================

I popup possono essere personalizzati sia nella *grafica*, sia nel *contenuto*
attraverso i seguenti template HTML: ::

 /usr/lib/node/nethcti-server/plugins/com_static_http/static/templates/notification_popup/call.html
 /usr/lib/node/nethcti-server/plugins/com_static_http/static/templates/notification_popup/streaming.html

Il primo serve a mostrare i dati di una chiamata generica, mentre il secondo quelli di una sorgente video,
quale ad esempio un videocitofono.

.. note:: Conoscenze richieste: linguaggi di programmazione HTML, CSS e Javascript.

Personalizzazione della grafica
-------------------------------

È sufficiente personalizzare il codice HTML e/o CSS dei template indicati. Supponiamo ad esempio di
voler modificare il colore del **nome e numero chiamante** in verde nel template ``call.html``: sarà sufficiente
aggiungere la regola css ``color: green`` nel selettore ``.contact-info``, che diventerà:

.. code-block:: css

    .contact-info {
        font-family: verdana;
        margin-top: 5px;
        margin-left: 15px;
        float: left;
        color: green;
    }

Personalizzazione del contenuto
-------------------------------

È possibile estendere le funzionalità presenti all'interno dei popup con nuovi comandi da eseguire.

1. Creare il template custom `win_popup.json`:

::

 mkdir -p /etc/e-smith/templates-custom/etc/nethcti/win_popup.json
 cp /etc/e-smith/templates/etc/nethcti/win_popup.json/10base /etc/e-smith/templates-custom/etc/nethcti/win_popup.json

2. Aprire il template appena creato con un editor di testi:

::

 vim /etc/e-smith/templates-custom/etc/nethcti/win_popup.json/10base

3. Aggiungere il nuovo comando all'interno dell'oggetto JSON `"commands"`, specificando
il percorso del programma eseguibile di Windows che si intenderà eseguire: ::

    ,"<NOME_NUOVO_COMANDO>": {
        "command": "<NOME_NUOVO_COMANDO>",
        "runwith": "<PATH_EXE>"
    }

Se ad esempio il nuovo comando si chiama **"gestionale"** e il programma da eseguire è
**"c:\\windows\\notepad.exe"**, la sezione da inserire sarà: ::

    ,"gestionale": {
        "command": "gestionale",
        "runwith": "c:\\\windows\\\notepad.exe"
    }


e quindi il template custom diventerà: ::

    {
        my $popupCtiProto = ${'nethcti-server'}{'PopupCtiProto'} || "https";

        $OUT = '{
        "call": {
            "width": "400",
            "height": "175"
        },
        "stream": {
            "width": "400",
            "height": "400"
        },
        "close_timeout": "10",
        "commands": {
            "url": {
                "command": "url",
                "runwith": ""
            }
            ,"gestionale": {
                "command": "gestionale",
                "runwith": "c:\\\windows\\\notepad.exe"
            }
        },
        "cti_proto": "' . $popupCtiProto .'"
    }';
    }

.. warning:: Il percorso dell'eseguibile di Windows deve utilizzare la stringa "\\\\\\" come separatore.

4. Adattare l'altezza del popup che si intende modificare, in base all'elemento grafico da aggiungere. Se ad esempio
si vuole inserire un nuovo pulsante nel template `"call.html"`, un'altezza pari a 175px può essere sufficiente: ::

    {
        "call": {
            "width": "400",
            "height": "175"
        },
        ...

5. Salvare la configurazione e uscire dall'editor di testi.

6. Eseguire il comando: ::

    signal-event nethcti-server3-update

7. Personalizzare uno o entrambi i template HTML in base alle proprie necessità:
è necessario inserire un **elemento grafico** e **un'azione da eseguire** in
corrispondenza del click sullo stesso. Supponiamo ad esempio di voler inserire
un nuovo pulsante nel template *"call.html"* cliccando il quale eseguire il nuovo
comando "gestionale".

Il codice HTML del nuovo pulsante grafico da inserire in *call.html* sarà:

.. code-block:: html

    <div class="contact-action">
        <div id="open-gestionale-but" cmd="gestionale" arg="" close="1" class="button" title="">Gestionale</div>
    </div>

8. **Opzionale:**
se si desidera passare l'identificativo del chiamante come parametro al programma di Windows,
è necessario aggiungere il seguente codice javascript in coda alla funzione `window.onload`:

.. code-block:: javascript

 $('#open-gestionale-but').attr('arg', params.callerNum);

9. Eseguire |product_nethifier| in Windows e connettersi al server cti.

Da questo momento alla ricezione di una chiamata generica nel popup sarà presente
un nuovo pulsante di nome "Gestionale", cliccando il quale si aprirà il notepad di Windows.

Ogni client |product_nethifier| può inoltre personalizzare i path dei programmi da eseguire:

- aprire l'interfaccia grafica |product_nethifier| attraverso la voce "Visualizza" del menù contestuale dell'icona nella system tray di Windows
- selezionare il tab "Esegui"
- personalizzare i path
- salvare la configurazione

Personalizzazione del protocollo
--------------------------------

È possibili modificare il protocollo con cui aprire |product| tramite il click sul popup.
Eseguire: ::

 config setprop nethcti-server PopupCtiProto "<PROTO>"
 signal-event nethcti-server3-update

dove <PROTO> può assumere i valori *http* o *https*.

Backup
------

Una volta effettuata una personalizzazione, ricordarsi di aggiungere i file alla lista dei backup
seguendo le istruzioni `qui riportate <http://docs.nethserver.org/en/latest/backup.html#inclusion>`_.
