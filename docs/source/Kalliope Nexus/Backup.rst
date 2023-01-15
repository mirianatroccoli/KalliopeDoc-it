Backup 
=====
La sezione di backup permette di gestire ed effettuare backup della propria centrale telefonica direttamente tramite interfaccia web, in questo modo è possibile avere più autonomia nella gestione di questo processo.

Elenco backup
----------
I backup possono essere effettuati manualmente tramite il tasto “+”, una volta premuto verrà aggiunta automaticamente una riga nell’elenco dei backup con il relativo file di backup della centrale appena generato. Nell'elenco i backup sono individuati tramite:

- Filename: nome del file
- Size: dimensione del file
- Data backup
- IP centrale master: indirizzo IP della centrale master

Dettaglio backup
-----------
Cliccando sul nome del file presente in elenco, si passa alla visualizzazione dettagliata del file di backup in cui sono contenute le stesse informazioni dell’elenco, ma con in più la specifica di:

- Tenant: nel caso in cui la centrale sia multitenant, è neceessario specificare il tenant a cui si è associati. In automatico invece, verrà impostato il valore "default"
- Path: dove è allocato il file di backup

Tramite il tasto verde in basso a destra, si può effettuare il restore del file di backup, per ricaricarlo all’interno della centrale, in modo da avere a disposizione tutti i dati al momento in cui è stato effettuato fatto il backup. Tramite il tasto rosso in basso a sinistra, elimina, è possibile eliminare il file di backup.


Dettagio bckp.png

Elenco centrali e restore.png
Elenco restore effettuati
---------
In questa sezione, raggiungibile tramite il menu a destra, è presente l’elenco dei restore effettuati, visualizzati tramite: esito, data e url della centrale su cui è stato effettuato e se in caso sia andato in errore.


Elenco centrali restore
In questa sezione è possibile indicare le centrali secondarie su cui attivare il restore. Si indicano quindi su quali altre centrali si può fare restore di un file di backup che è presente già nel sistema. Mentre la centrale principale su cui viene effettuato il backup si può visualizzare andando su: **Preferenze di sistema > Voip**.

Se risulta la principale e l’unica centrale inserita, viene riproposta in “centrali master” con le informazioni essenziali per effettuare il backup.

Tramite il pulsante “Nuova centrale” si possono specificare centrali secondarie, si può decidere di fare dei backup periodici per ogni centrale. Es. Un’azienda può trovarsi a gestire più centrali telefoniche, quindi si può decidere di fare backup periodici per ognuna. Periodicamente, grazie ai cron, la centrale può fare backup dei vari file.

