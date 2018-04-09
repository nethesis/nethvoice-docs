========================
Provisioning dei gateway
========================

La configurazione dei gateway avviene nel Wizard.

Il provisioning per i gateway segue le stesse regole di quello per i telefoni con una fondamentale differenza:

al contrario dei telefoni, il |product| si collega in telnet direttamente al gateway per caricare la configurazione senza che siano loro che la debbano recuperare.

La configurazione dei gateway avviene con il gateway online, di default i gateway si avviano in DHCP.

E’ comunque possibile cliccando su Aggiungi Gateway creare una configurazione per un gateway non ancora collegato per poi configurarlo caricando il file dall'interfaccia web del gateway.

Configurazione dei gateway in rete
==================================

Effettuare la scansione delle reti locali nel Wizard in :ref:`Fasci Fisici <fisici>`.

Una volta trovato in rete il gateway che si vuole configurare è necessario specificare i pochi parametri di configurazione necessari:

1. Ip del dispositivo, la configurazione del gateway richiede un ip statico
2. Maschera di rete
3. Gateway di rete
4. Ip del |product|, in alcuni scenari d'installazione il gateway può raggiungere il |product| non tramite il suo ip locale
5. Eventuali caratteristiche necessarie alla configurazione delle linee collegate (per linee ISDN la modalità della borchia, per linee analogiche il numero chiamato della linea)

Dopo aver salvato la configurazione è possibile cliccando sul pulsante *Carica* consentire al |product| di collegarsi in telnet al gateway per caricare e/o indicare dove recuperare (a seconda della marca) la configurazione.

C'è anche la possibilità di scaricare la configurazione del gateway per caricarla tramite l’interfaccia web nel caso il gateway non sia raggiungibile direttamente dal |product| cliccando nel tasto per la gestione (simbolo con tre quadratini).
