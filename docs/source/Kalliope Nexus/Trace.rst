Trace
=====
Trace Inbound
----------

Descrizione del servizio
+++++++++++
Il modulo Kalliope Trace consente di gestire le chiamate inbound permettendo all’operatore di raccogliere e visualizzare una serie di informazioni relative al cliente associato al numero chiamante. Quest'ultimo viene automaticamente riconosciuto e, sulla base dei contatti già salvati nella piattaforma, vengono fornite le informazioni all’operatore che andrà a gestire la telefonata. Si potranno visualizzare diversi tipi di informazioni, dal semplice nome del cliente o dell’azienda, a ticket aperti per quest'ultimo o chiamate già registrate.

Le chiamate salvate sono visualizzate in un unico luogo affinché non si perdano note o descrizioni prese per ogni chiamata e per cui è stata utilizzata la schermata del modulo.

Maschera Chiamate
++++++++++
Il primo punto riguarda la ricezione o la risposta ad una chiamata da parte di un operatore. In base ad una specifica configurazione fatta sulla KCTI presente sul proprio PC (impostazioni -> azioni automatiche -> apertura url dinamica) e una preferenza indicata su Kalliope Nexus, un operatore che riceve o risponde alla chiamata vedrà aprirsi sul suo monitor una pagina del proprio browser contenente la maschera di Kalliope Nexus. La maschera contiene alcuni campi precompilati in modo da agevolare il riconoscimento dell'azienda e del suo stato finanziario.

Questo avviene nel momento in cui l'azienda risulta registrata nella sezione "Aziende" e quindi viene riconosciuta dal sistema, al contrario, l'operatore avrà la possibilità di inserire semplicemente i dati del chiamante e quindi registrare l'azienda.

Nella figura in basso è possibile osservare un esempio di chiamata da parte di un numero non riconosciuto dal sistema. In questo caso è l'operatore a creare l'azienda collegata cliccando sull'icona della matita a destra della "i". In questo modo dovranno essere inseriti i dati di ragione sociale, codice e partita iva.

Tramite le spunte è possibile: aggiungere il numero in blacklist, associare il numero all'azienda e associare il numero al referente.

Inbound1.png

Nel caso in cui il chiamante fosse già registrato nella piattaforma, i campi precedentemente vuoti verranno compilati automaticamente e i colori della parte finanziaria cambieranno automaticamente per rendere migliore la lettura.

Inbound2.png

In entrambi i casi, l'url che verrà aperto dalla KCTI grazie alla configurazione di "apertura url dinamico" sarà il seguente:

.. code-block:: console

   indirizzio_di_aladino/chiamataInbound/main/edit/?caller=<callernum>&callername=<callername>&callercompany=<callercompany>&callerunit=<callerunit>&extenNum=<extenNum>&queueName=<queueName>&uid=<uid>&called=<callednum>

Elenco delle chiamate ricevute
+++++++++
La seconda principale funzione di questa sezione consiste nell'elenco delle chiamate gestite in ingresso. Questo permette di visualizzare diverse informazioni, con la possibilità di collegarle e visualizzarle nella maschera "chiamata", precedentemente citata con i relativi dati. Le informazioni contenute nelle colonne consistono in:

- numerazione
- ragione sociale dell'azienda chiamante (CALLER)
- ragione sociale dell'azienda chiamata (CALLED)
- descrizione della chiamata
- propietario
- caller (nemero)
- called (numero)
- tipologia
- data e ora di inizio della chiamata
- data e ora di termine della chiamata
Elenco inbound.png

Da questa pagina sarà possibile visualizzare il dettaglio di ogni chiamata semplicemente cliccando sul numero che la identifica (evidenziato in blu sotto nella colonna "numerazione"). In questo modo saranno visibili le informazioni sulle aziende (caller e called), le note prese dall'operatore, la descrizione, la tipologia associata e il grado di priorità inserito, oltre alla data e all'ora di inizio e di fine della chiamata.

Inbound 3.png

Preferenze di sistema.png
Nella parte inferiore di questa maschera saranno disponibili due tasti: uno sulla sinistra ed uno sulla destra. Il primo (sinistra) "modifica", abilita l'utente ad effettuare modifiche alla chiamata, con la possibilità anche di eliminarla cliccando sul tasto rosso "elimina". In questa maschera è possibile visualizzare dei grafici riassuntivi, che possono essere abilitati tramite le "Preferenze di sistema".

Grafici 1 inb.JPG


I grafici permettono di visualizzare: report storico chiamate, chiamate in ingresso/uscita, agganciare un ticket, agganciare un contratto, visualizzare uno script ecc.

Dopo aver effettuato le modifiche alla chiamata, cliccare su "salva" per salvarle o su "dettaglio" per uscire dalla maschera di modifica senza salvare.

Il secondo tasto invece (destra), "invia per email" permetterà di selezionare il template del messaggio, il mittente, il destinatario e specificare oggetto e descrizione.

Griglie e widget
+++++++++
Dalla pagina principale della sezione, dove è visibile l'elenco, potrà essere variata la visualizzazione delle informazioni in elenco cambiando griglia utilizzata. Per fare ciò, cliccare sul tasto "griglie disponibili" e selezionare la griglia desiderata. Se questa non sarà presente, sarà sempre possibile crearne una nuova attraverso l'apposito tasto "+ nuova griglia" con cui si verrà reindirizzati alla maschera di creazione della sezione "Griglia". Dopo di che, eseguire le istruzioni della sezione indicata.

Per aggiungere ed utilizzare dei widget seguire la spiegazione indicata qui.

Trace Outbound
-----------
Descrizione del servizio
++++++++++
Il modulo Kalliope Trace permette la gestione delle chiamate outbound, ovvero chiamate effettuate dall'operatore verso un cliente, quindi in uscita rispetto alla centrale telefonica. Questo modulo vede la sua utilità nella registrazione dei dati delle chiamate effettuate e nell'apertura automatica di una maschera "chiamata" come quella delle Chiamate Inbound, con l'unica differenza che, in questo modulo, non sarà presente la maschera per l'azienda chiamante (essendo sempre la stessa) ma solo quella dell'azienda chiamata (CALLED).


Maschera Chiamata
++++++++
Anche qui, come per le chiamate inbound, l'automazione dell'apertura della maschera all'avvio della chiamata è dovuta alla configurazione della centrale telefonica, che questa volta genererà il seguente url:

.. code-block:: console

   nome_azienda.aladino.cloud/chiamataOutbound/main/edit/?caller=<callernum>&callername=<callername>&callercompany=<callercompany>&callerunit=<callerunit>&extenNum=<extenNum>&queueName=<queueName>&uid=<uid>&called=<callednum>

Questa schermata sarà disponibile anche cliccando il tasto verde "+" in basso a destra.

Come per le chiamate inbound, l'operatore potrà creare una nuova azienda per il contatto che ha chiamato, e che quindi non è stato riconosciuto dal sistema, semplicemente cliccando sull'icona della matita a destra della "i" nella riga "azienda called" o "referente called".

Verranno automaticamente popolati i campi finanziari dell'azienda (socre, outlook, crediti in sofferenza e esposizione/fido), colorandoli adeguatamente per renderli intuitivi. L'utente potrà sempre modificare i campi sottostanti, allegare dei documenti, scrivere una descrizione o aggiungere delle note.

A differenza del modulo delle chiamate inbound, in questo modulo vengono visualizzate tutte le chiamate effettuate allo stesso called tra le ultima 50, con informazioni quali:

- unique id
- data e ora di inizio
- numero caller
- numero called
- stato
Outbound1.png

Una volta che la chiamata sarà terminata, basterà premere su "salva" per memorizzarla nell'elenco o su "salva ed invia email" per inviare mail (si aprirà una maschera con i campi di una classica mail da compilare) in aggiunta al salvataggio.

Elenco
++++++++
L'elenco che sarà visibile appena aperta la pagina della sezione, sarà uguale a quello della sezione delle chiamate inbound, fatta eccezione per la ragione sociale del caller che non sarà presente. Le informazioni che saranno contenute nella griglia saranno:

- numerazione
- ragione sociale dell'azienda chiamata (CALLED)
- descrizione della chiamata
- propietario
- caller (nemero)
- called (numero)
- tipologia
- data e ora di inizio della chiamata
- data e ora di termine della chiamata
Elenco outbound.png

È possibile visualizzare la maschera di dettaglio di ogni chiamata cliccando sul numero nella colonna "numerazione". In questo modo saranno visibili le informazioni sull'azienda, le note prese dall'operatore, la descrizione la tipologia associata e il grado di priorità inserito, oltre alla data e all'ora di inizio e di fine della chiamata.

Preferenze di sistema.png
Come nelle chiamate Inbound, nella parte inferiore di questa maschera saranno disponibili due tasti: uno sulla sinistra ed uno sulla destra. Il primo (sinistra) "modifica", abilita l'utente ad effettuare modifiche alla chiamata, con la possibilità anche di eliminarla cliccando sul tasto rosso "elimina". In questa maschera è possibile visualizzare dei grafici riassuntivi, che possono essere abilitati tramite le "Preferenze di sistema".

Grafici 2 outbound.JPG

I grafici permettono di visualizzare: report storico chiamate, chiamate in ingresso/uscita, agganciare un ticket, agganciare un contratto, visualizzare uno script ecc. Dopo aver effettuato le modifiche alla chiamata, cliccare su "salva" per salvarle o su dettaglio per uscire dalla maschera di modifica senza salvare.

Il secondo tasto invece (destra), "invia per email" permetterà di selezionare il template del messaggio, il mittente, il destinatario e specificare oggetto e descrizione.

Griglie e widget
++++++++++
Dalla pagina principale della sezione, dove è visibile l'elenco, potrà essere variata la visualizzazione delle informazioni in elenco cambiando griglia utilizzata. Per fare ciò, cliccare sul tasto "griglie disponibili" e selezionare la griglia desiderata. Se questa non sarà presente, sarà sempre possibile crearne una nuova attraverso l'apposito tasto "+ nuova griglia" con cui si verrà reindirizzati alla maschera di creazione della sezione "Griglia". Una volta qui, seguire le istruzioni della sezione indicata.

Per aggiungere ed utilizzare dei widget seguire la spiegazione indicata qui

