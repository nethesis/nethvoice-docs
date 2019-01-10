=========================================
Migrazione da |product|11 a |product|14
=========================================

La migrazione consente di configurare |product| 14 partendo dalla configurazione di un |product| 11.

Ci sono due scenari possibili:

* un NethServer 7 con installato |product| 11
* il ripristino di un backup di un NethServer 7 con |product| 11 su una nuova macchina, su cui si installerà |product| 14

Entrambe le procedure comportano comunque un downtime 

NethServer 7 con installato |product| 11
========================================

Rimuovere |product| 11 e tutte le sue dipendenze lanciando il comando ::

    /etc/e-smith/events/actions/nethvoice-11-to-14-prepare-upgrade

Proseguire con "Installazione di |product| 14 e interfaccia di migrazione"

Ripristino di un backup di un NethServer 7 con |product| 11 su una nuova macchina, su cui si installerà |product| 14
====================================================================================================================

Ripristinare il backup (configurazione e dati) senza reinstallare i pacchetti.

Proseguire con "Installazione di |product| 14 e interfaccia di migrazione"

Installazione di |product| 14 e interfaccia di migrazione
=========================================================

Installare il gruppo |product| 14, avendo cura di verificare che la versione del pacchetto di nethserver-freepbx che verrà installato è >= 14.0.15-1 ::

    yum install @nethserver-nethvoice14

Al termine dell'installazione, raggiungere l'interfaccia web di nethvoice all'indirizzo https:///IP/nethvoice

Se non è ancora stato configurato un account provider sulla macchina, l'interfaccia mostrerà la possibilità di scegliere se installare un account provider LDAP locale o configurarlo manualmente. Nel primo caso, non verranno richieste ulteriori configurazioni, mentre nel secondo si verrà rediretti all'interfaccia di NethServer, dove sarà possibile configurare il provider degli utenti. Se il provider scelto non è locale, non sarà possibile creare gli utenti, che dovranno essere quindi creati manualmente sul provider stesso prima di procedere con la migrazione.

Dopo la selezione del provider degli utenti, l'interfaccia mostrerà la possibilità di iniziare la migrazione o saltarla. Saltando la migrazione, verrà poroposta la possibilità di migrare comunque il CDR (storico delle chiamate).

Iniziando la migrazione, verrà mostrata la lista degli interni presenti sul |product| 11. Se erano stati configurati degli utenti sul CTI, verranno consigliati, altrimenti si può associare agli interni uno degli utenti già creati o crearne di nuovi (sempre se si è configurato un provider di utenti locale)

Gli interni senza un utente associato non verranno ricreati, ma sarà sempre possibile farlo in un secondo momento

Quando si è soddisfatti, si può proseguire con la migrazione cliccando su "inizia migrazione"

Creati i nuovi interni ed utenti e cliccando su "avanti" verranno migrati gli altri oggetti del centralino e verrà mostrato l'esito. Per ogni categoria di oggetti del dialplan, verrà mostrata una spunta verde se la migrazione è avvenuta e una "x" rossa se c'è stato un errore. I singoli oggetti migrati, verranno elencati. Se non è possibile migrare alcuni di questi, verrà visualizzato un warning. Alla fine della migrazione, sarà possibile scaricare un report con i warning e gli errori, che può essere utilizzato per ricreare manualmente ciò che la procedura non è riuscita a ricreare.

Verranno ora migrati:

* fasci VOIP
* gateway e fasci fisici
* fasci e interni iax
* rotte in uscita
* gruppi
* code
* ivr
* cqr
* registrazioni
* annunci
* controllo flusso di chiamata
* rotte in entrata
* rubrica del CTI
* tabelle del report delle code
* messaggi delle voicemail
* paging
* contesti custom
* conferenze "meetme"
* disa
* priorità coda

andando avanti, si inizierà la migrazione del CDR. Questa richiede molto tempo, per cui verrà avviata in background.

Verrà mostrato ora il riepilogo di errori e warning, scaricabile anche come PDF

Arrivati a questo punto, la migrazione è terminata e viene mostrata la pagina del wizard di |product| 14. Si potrà ora seguire il wizard, verificando che la migrazione ha creato correttamente il dialplan e creando a mano eventuali destinazioni che non sono state migrate e che sono quindi sul report.

I vecchi interni verranno ricreati come interni custom, in modo che sia già possibile utilizzarli, ma andranno eliminati e associati di nuovo all'utente dalla pagina "Configurazioni".
