Servizi telefonici avanzati
====

Audioconferenza
-----

.. note::
   Il servizio di audioconferenza è stato profondamente modificato a partire dalla versione di firmware 4.7.12, in cui è stato introdotta la modalità "dial-out" e la disponibilità di un pannello web di supervisione e monitoraggio della stanza di conferenza in tempo reale, in grado di mostrare lo stato dei partecipanti alla conferenza ed effettuare alcune operazioni di gestione (espulsione o invito di partecipanti, disattivazione dell'audio proveniente da uno o più partecipanti, ecc.)

   
Il servizio di audioconferenza disponibile su KallipePBX permette di configurare più stanze con differenti caratteristiche, gestibili e monitorabili in modo autonomo da singoli utenti (anche non amministratori) della centrale.

Per ciascuna stanza è possibile attivare la modalità di accesso "dial-in" e/o la modalità di accesso "dial-out".

La modalità "dial-in" prevede che i partecipanti accedano al servizio chiamando un determinato numero e siano inseriti nella stanza previo inserimento di un PIN di accesso (inviato tramite toni DTMF). L'accesso ad una specifica stanza dial-in può avvenire secondo differenti modalità:

- **accesso con selezione interattiva della stanza**: il servizio di audioconferenza ha associata una selezione all'interno del piano di numerazione, il cui valore predefinito è 802; chiamando tale selezione da un interno una voce guida chiede di inserire il numero della stanza a cui collegarsi. In base alla configurazione della stanza può essere richiesto, dalla voce guida, l'inserimento di un PIN di accesso.
- **accesso diretto ad una specifica stanza**: si effettua una chiamata alla selezione associata al servizio concatenata al numero della stanza (es. 8021234, nel caso che il codice del servizio sia 802 e si voglia accedere alla stanza 1234). Anche in questo caso la voce guida richiederà l'inserimento del PIN di accesso, se previsto per la stanza.
Entrambe queste modalità sono fruibili anche da chiamanti esterni, configurando DID (sulle linee di ingresso) o inoltri (nel piano di numerazione oppure come uscite di IVR, o di altre entità telefoniche) verso la destinazione "Servizio audioconferenza" e selezionando la voce "Chiedi numero della stanza" o una delle stanze presenti.

La modalità "dial-out" prevede invece che sia la centrale stessa a chiamare i singoli partecipanti configurati, nel momento in cui viene dato dalla GUI il comando di avvio della stessa.

In una stessa stanza possono convivere sia partecipanti "dial-out" che partecipanti "dial-in" (se la configurazione lo permette); un pannello web di stato della stanza permette di monitorare in tempo reale l'operatività della stessa e dei relativi partecipanti, con la possibilità di effettuare operazioni di gestione quali il MUTE (e l'UNMUTE) di uno o più partecipanti, l'espulsione di un partecipante dalla stanza, o la sua chiusura (con conseguente espulsione di tutti i partecipanti).

Configurazione delle stanze
++++++++
La configurazione delle stanze di conferenza avviene in 2 fasi. Nella prima fase deve essere semplicemente definita la stanza, assegnandogli una identità (numero della stanza) ed alcuni parametri accessori. Una volta che sia stata creata la stanza (applicando le modifiche), è possibile passare alla fase di configurazione operativa. In questa seconda fase di configurazione è possibile definire la natura della stanza (dial-in e/o dial-out), specificare il comportamento all'ingresso di un nuovo partecipante (es. nel caso dial-in se richiedere un pin di accesso) oppure predisporre una lista di contatti (interni e/o esterni) che devono essere contattati dalla centrale al momento di attivazione della componente dial-out.

Creazione e configurazione stanza di audioconferenza
........
La configurazione di una stanza di conferenza si effettua dal pannello "Applicazioni PBX" > "Servizio Audioconferenza". Il pannello mostra la lista delle stanze esistenti, con i principali attributi. Per aggiungere una nuova stanza, o modificarne una esistente, è necessario acquisire il lock di scrittura. Per modificare una stanza esistente è necessario cliccare sull'icona di Modifica (matita); per aggiungere una nuova stanza si clicca invece sul link "Aggiungi nuova stanza" presente subito sopra l'elenco delle stanze. In entrambi i casi si apre la pagina di modifica della stanza, in cui si devono inserire i seguenti parametri:

Impostazioni generali
..........

- **Abilitato**: checkbox di abilitazione della stanza. Se si disabilita una stanza questa non sarà più utilizzabile, ma i relativi parametri di configurazione ed operativi vengono mantenuti al valore corrente.
- **Numero**: è l'identificativo primario della stanza, e deve essere numerico. Viene utilizzato dal sistema per identificare la stanza; nel caso di stanze con modalità dial-in, questa è la selezione che deve essere digitata al momento della richiesta o concatenata al codice di accesso al servizio.
- **Nome**: è il nome assegnato alla stanza, ed ha una funzione mnemonica e non operativa; viene utilizzato nelle varie select di selezione della stanza quando si configura un inoltro al servizio di audioconferenza, e si vuole specificare la stanza.


Impostazioni Dial-out
.........
Queste impostazioni sono necessarie nel caso in cui si voglia utilizzare la stanza in modalità Dial-out; nel caso in cui la stanza sia utilizzata nella sola modalità Dial-in questi parametri possono essere non impostati. I due parametri sono l'Identità e la Classe di instradamento di uscita e sono utilizzati dalla centrale quando deve effettuare le chiamate verso i partecipanti esterni che devono essere aggiunti alla stanza nella modalità Dial-out. La Classe di instradamento viene utilizzata per determinare l'instradamento sulle varie linee di uscita della specifica chiamata, mentre l'identità viene utilizzata per effettuare l'impostazione del numero chiamante

Utenti abilitati alla modifica operativa
........
Questo elenco raccoglie gli utenti che, indipendentemente dai permessi derivanti dal proprio ruolo, hanno la possibilità di effettuare modifiche alla configurazione operativa della stanza. Le attività di configurazione operativa su una stanza includono la modifica del PIN di accesso, la selezione della musica di attesa riprodotta nella stanza quando vi è un solo partecipante, l'abilitazione della funzione Dial-in e/o Dial-out, ecc. ma non quelle di supervisione e pilotaggio in tempo reale, che possono essere assegnate a differenti utenti.


Configurazione operativa
+++++++
Una volta creata la stanza è possibile procedere con la sua configurazione operativa, passando al tab "Configurazione operativa stanze", che elenca tutte le stanze definite, riassumendone i parametri operativi principali.

Ciascuna stanza può trovarsi nello stato "closed" (chiusa) oppure "open" (aperta). E' possibile modificare i parametri operativi di una stanza solo quando si trova nello stato "closed", cliccando sull'icona di Edit (matita)in fondo alla riga della tabella. Il passaggio dallo stato "closed" a quello "open" può avvenire in due modalità, una manuale ed una automatica. La modalità manuale è comandata da un utente abilitato (vedi sotto per quanto riguarda i permessi di supervisione e pilotaggio) cliccando sul pulsante corrispondente, adiacente a quello di modifica della configurazione operativa. L'apertura automatica è disponibile solo per le stanze per le quali è attiva la modalità Dial-in, ed avviene nel momento in cui un qualsiasi interno accede alla stanza.

La pagina di configurazione operativa della stanza è divisa in diverse sezioni; la prima sezione contiene delle impostazioni generali, che sono:

- **Lingua**: la lingua con la quale devono essere riprodotti ai partecipanti i vari prompt audio (es. la richiesta del PIN, oppure il messaggio di ingresso di un nuovo utente nella conferenza)
- **PIN di amministrazione**: il PIN di accesso alla stanza in modalità amministratore (admin); si noti che possono essere più utenti amministratori all'interno della stessa stanza di conferenza. Le peculiarità degli utenti amministratore sono per il momento associate alla funzione opzionale di espulsione automatica di tutti i partecipanti, al momento in cui l'ultimo utente amministratore esce dalla stanza
- **PIN**: il PIN di accesso alla stanza in modalità partecipante standard
- **Annunci abilitati**: flag che se abilitato richiede ai partecipanti che entrano nella conferenza di pronunciare il proprio nome, al fine di effettuarne l'annuncio ai partecipanti già presenti preliminarmente all'inserimento e a seguito di uscita dalla stanza
- **Espelli utenti su uscita ultimo admin**: flag che attiva la funzione di espulsione di tutti gli utenti presenti nella stanza di conferenza nel momento in cui l'ultimo partecipante con ruolo amministratore esce dalla stanza
- **Abilita ottimizzazione mixing**: permette di ottimizzare la qualità audio della stanza e le performance evitando di miscelare l'audio proveniente da partecipanti che non stanno parlando (Silence Suppression, o Talker Optimization) o comunque sotto una certa soglia di rilevazione (VAD - Voice Activity Detection). In questo modo viene ridotto il rumore di fondo della stanza, ma viene normalmente introdotto un breve clipping nell'audio dei partecipanti quando iniziano a parlare, tipico di tutti i sistemi con VAD, poiché il PBX deve rilevare il superamento di un determinato livello di intensità audio prima di considerare il partecipante come attivo. L'ottimizzazione mixing non modifica in modo significativo le performance del sistema in quanto il guadagno di computing relativo alla decodifica e miscelazione di un flusso audio in meno è compensato dal carico necessario ad effettuare la rilevazione del parlato (VAD - Voice Activity Detection), mentre la parte più onerosa dell'attività è la codifica del flusso audio risultante per inviarlo ai vari partecipanti, e questo è un contributo che rimane costante indipendentemente dal numero dei parlanti attivi
- **File della musica di attes**a: mentre vi è un unico partecipante nella stanza, è possibile riprodurre un file audio invece di lasciarlo nel silenzio; cliccando su "Scegli file" si apre la finestra del Sistema Operativo per poter selezionare il file audio da utilizzare.


La sezione Dial-in contiene solo la casella di spunta per l'abilitazione del servizio Dial-in; se si disabilita la modalità Dial-in non sarà più possibile accedere alla stanza effettuando una chiamata al servizio di Audioconferenza, ma si dovrà essere chiamati da essa, nella modalità Dial-out.

La sezione Dial-out raccoglie le impostazioni relative alla modalità omonima, in cui è il Kalliope ad effettuare le chiamate verso i partecipanti configurati, unendoli alla conferenza nel momento della risposta. I parametri configurabili sono:

- **Abilitazione Dial-out**: flag che determina se la modalità Dial-out è abilitata per questa stanza. Per poter utilizzare la modalità Dial-out con partecipanti esterni è necessario che nel pannello di configurazione della stanza siano state assegnate l'identità e la classe di instradamento di uscita da utilizzare per effettuare la chiamata uscente. In caso contrario non sarà possibile per la stanza effettuare chiamate verso i numeri esterni
- **Numero massimo di tentativi di chiamata per partecipante**: indica il numero massimo di tentativi di chiamata che possono essere effettuati per ciascun partecipante; una chiamata da parte della stanza verso uno dei partecipanti può difatti fallire per vari motivi (utenza occupata, o momentanemanete non raggiungibile, oppure utente che non accetta la chiamata). Nel momento in cui una chiamata fallisce (nel caso in cui la politica di invito di quel partecipante sia "automatica, con ripetizione") il sistema può effettuare un nuovo tentativo di chiamata, fino al raggiungimento del numero massimo qui configurato
- **Abilita riproduzione file audio stanza completa/incompleta e realtivi pulsanti di selezione dei file**: nel caso di utilizzo della stanza in modalità Dial-out, è possibile iniettare nella stanza un file audio differente nel caso in cui la stanza sia "completa" o "incompleta"; lo stato di completezza della stanza è valutato dal Kalliope in base alla presenza nella stanza di tutti i partecipanti Dial-out marcati come "obbligatori". Questa funzione può essere utile, in caso di stanze non supervisionate, per far sapere ai presenti nella stanza se manca qualcuno tra i partecipanti la cui presenza è marcata come richiesta.


A seguire è presente un elenco dei partecipanti Dial-out, che saranno quindi contattati dalla centrale in base alla rispettiva politica di invito nella stanza. Per aggiungere un partecipante si clicca sull'icona + (Aggiungi partecipante); viene inserita una nuova riga nella lista con cui specificare il partecipante, che può essere un interno del PBX (tipo "Interno") o un numero esterno ("Esterno"); nel primo caso il campo "Contatto" è una lista da cui selezionare uno degli interni della centrale, mentre nel secondo caso nel campo "Contatto" deve essere inserito il numero esterno da chiamare (privo del prefisso di impegno linea esterna). In quest'ultimo caso è possibile specificare anche il nome del partecipante, che sarà mostrato nel pannello di supervisione e gestione della stanza, quando questa è aperta. Per ciascun partecipante Dial-out è possibile scegliere una diversa politica di invito nella stanza, tra le 3 possibili: Automatica con o senza ripetizione, oppure manuale. I dettagli di funzioanmento delle tre politiche sono spiegate in seguito, nella sezione di descrizione del funzionamento del pannello di supervisione e gestione della stanza.

La politica di invito automatico prevede che la stanza effettui le chiamate verso i relativi partecipanti, in modo automatizzato a partire dal momento in cui l'utente che sta gestendo la stanza (che deve essere precedentemente messa nello stato "Aperto") effettui l'avvio del meccanismo di invito. Le chiamate vengono effettuate in modo parallelo; nel caso di partecipanti esterni, al momento della risposta il sistema si deve assicurare che la chiamata sia stata risposta da una persona e nno da un servizio automatico (messaggi di cortesia, o caselle vocali), per cui viene richiesta l'accettazione della chiamata mediante digitazione del tasto "1". In caso di ricezione del tono, la centrale inserisce il partecipante in conferenza, altrimenti si comporta come se la chiamata non sia stata risposta, e dopo un timeout la abbatte. In caso di fallimento di una chiamata, se la politica di invito per quel partecipante è "Automatica senza ripetizione", lo stato del partecipante viene impostato a "Fuori stanza", e se è marcato come "obbligatorio" si attiva (se abilitata) la riproduzione del file audio di stanza incompleta. Se la politica è invece "Automatica con ripetizione", il sistema effettuerà ulteriori tentativi fino al raggiungimento del numero massimo configurato per la stanza. Nel caso di politica di invito "Manuale", il partecipante non viene chiamato dalla centrale all'avvio del meccanismo di invito, ma deve essere comandata singolarmente per ciascuno di essi l'esecuzione della chiamata. Questa modalità di invito è sempre singola; in caso di fallimento un successivo tentativo può essere effettuato solo comandando manualmente una nuova chiamata.

L'ultima sezione del pannello permette di definire gli utenti che sono autorizzati ad effettuare le operazioni di supervisione e gestione della stanza, in aggiunta a quelli abilitati alla configurazione operativa (per ruolo - per i quali è necessaria l'abilitazione in scrittura - o perché specificati nel pannello di configurazione della stanza). 

**NOTA**: gli interni associati agli utenti che sono abilitati alla gestione della stanza possono entrare nella stessa in modalità dial-in (se abilitata), come amministratori, senza necessità di digitare il PIN

Gli utenti abilitati alla gestione della stanza visualizzeranno nella GUI il pulsante "Apri stanza" (icona play) per comandare l'apertura manuale della stanza (se chiusa) o il pulsante "Visualizza stato e gestisci stanza" (lente) per accedere al pannello di supervisione e gestione (se aperta).

Supervisione e gestione della stanza
+++++++++
Ciascuna stanza di conferenza può trovarsi, ad un dato istante, in uno di questi tre stati: "chiusa", "aperta", "aperta e attiva". Il passaggio tra questi 3 stati può avvenire in modo automatico o manuale, secondo una specifica macchina a stati.

Come indicato in precedenza, l'apertura di una stanza di conferenza può avvenire in modalità manuale o automatica. In modalità manuale, uno degli utenti abilitati alla sua gestione ne comanda esplicitamente l'apertura cliccando sul pulsante "Apri stanza" (icona play) Nel caso di stanza abilitata alla modalità dial-in, la stanza viene automaticamente aperta nel momento in cui un interno vi entra. In entrambi i casi, l'icona di stato presente nel pannello di configurazione operativa delle stanze si trasforma in una lente, e viene inibita la possibilità di apportare modifiche alla configurazione operativa; per poter apportare modifiche alla configurazione operativa della stanza è necessario prima chiuderla (entrando nel pannello di gestione della stessa). Lo stato "aperta e attiva" (o più brevemente "attiva") indica che per quella stanza è attivo il servizio di invito dial-out dei partecipanti (per quelli caratterizzati da una politica di invito automatico)

L'utente, cliccando sull'icona "Visualizza stato e gestisci stanza" accede al pannello di supervisione e gestione della stessa, suddiviso in 3 sezioni.

Nella prima sezione ("Informazioni stanza") sono riportati il nome ed il numero della stessa, ed il relativo stato, che può essere "Aperta" o "Attiva"; nel primo caso la stanza è operativa ma gli inviti automatici sono arrestati, mentre nel secondo caso la centrale si occupa di effettuare le chiamate automatiche verso i partecipanti con politica di invito automatico, e di ripetere l'invito nel caso in cui uno di tali partecipanti esca per qualsiasi motivo. Accanto allo stato è presente un pulsante a forma di X che permette di espellere tutti i partecipanti e tornare allo stato di stanza "chiusa".

La seconda sezione ("Dial-out") riporta le informazioni di stato relative a questa modalità della stanza, ed i pulsanti utilizzabili per comandarne le operazioni. Il primo flag "Dial-out automatico" indica se la funzione di invito automatico dei partecipanti è attiva o inattiva; in caso di servizio di invito inattivo, è possibile avviarlo cliccando sull'icona "Play" adiacente; in caso di servizio attivo, il pulsante "Stop" permette di espellere tutti i partecipanti e arrestare il meccanismo di invito automatico.

L'indicatore di stato seguente indica se la stanza è completa o incompleta, in base alla presenza dei partecipanti che sono marcati come obbligatori. Se anche uno solo dei partecipanti obbligatori si trova fuori dalla stanza (salvo che sia stato messo in stato "Sospeso" - vedi sotto per gli stati possibili dei partecipanti alla stanza) allora la stanza è considerata incompleta, altrimenti è nello stato completa. In ciascuno dei due stati può essere riprodotto un file audio di sottofondo nella stanza di conferenza per informare i partecipanti della condizione.

Nella parte bassa del pannello è presente la lista dei partecipanti alla stanza di conferenza, in forma di tabella; per ciasun partecipante si hanno le seguenti informazioni ed un set di azioni effettuabili (in funzione della natura e dello stato del partecipante):


- **Nome**: Identità dell'interno oppure nome assegnato in fase di aggiunta del partecipante alla stanza
- **Selezione**: Numero dell'interno, oppure numero esterno
- **Politica di chiamata**: modalità con la quale il partecipante viene inserito nella stanza di conferenza. Nel caso di partecipanti dial-out, la politica può essere manuale o automatica (con 1 singolo tentativo di chiamata, oppure con ripetizione fino al numero massimo di tentativi configurati per la stanza). In questa lista compaiono anche gli eventuali partecipanti dial-in, che quindi sono entrati nella stanza chiamando il servizio di audioconferenza, selezionando la stanza e digitando il relativo PIN. A questi utenti risulta associata la modalità manuale.
- **Richiesto**: flag che indica se la presenza del partecipante è obbligatoria per la valutazione dello stato di completezza della stanza. Gli utenti dial-in hanno sempre questo flag disabilitato
- **Dinamico**: flag che indica se il partecipante è configurato in modo statico come appartenente alla stanza (partecipante dial-out definito nella pagina di configurazione operativa della stanza) oppure se è presente solo in modo temporaneo. Un partecipante può essere presente in via temporanea in due casi: se si tratta di partecipante dial-in, oppure se viene aggiunto dinamicamente mediante il pulsante "Aggiungi partecipante dial-out" presente nella sezione "Dial-out" precedente. In caso di chiusura di una stanza, tutti i partecipanti temporanei vengono cancellati, ed una successiva apertura vedrà quindi come partecipanti i soli utenti configurati staticamente; in caso di apertura automatica della stanza a seguito di ingresso di un utente dial-in, allora anche tale utente sarà presente in modalità "Dinamica".
- **Direzione**: indica se il partecipante è di tipo dial-out o dial-in. In caso di utente dial-in, se questo chiude la conversazione o se viene espulso da GUI, oppure se la stanza viene arrestata senza essere chiusa, questo rimane nella lista dei partecipanti. E' possibile cliccare sull'icona della cornetta telefonica presente nella colonna "Azioni" per farlo chiamare dalla stanza di audioconferenza, di fatto trasformandolo in partecipante dial-out dinamico ad invito manuale.
- **Stato**: ciascun partecipante può trovarsi in uno dei seguenti stati:
  - **Fuori dalla stanza**: l'utente non sta partecipando alla conferenza; è la condizione iniziale quando la stanza è aperta ma non ancora attiva (quindi gli inviti automatici sono disabilitati).
  - **Nella stanza:** l'utente è all'interno della stanza e partecipa all'audioconferenza.
  - **Invitato**: il KalliopePBX sta effettuando la chiamata verso il partecipante per inserirlo nella stanza. L'esito di questo tentativo di chiamata può essere negativo (utente occupato, non risponde, non accetta l'inserimento) nel qual caso il sistema può ripetere il tentativo di chiamata (se il partecipante ha una politica di invito automatica con ripetizione, e non sono stati esauriti i tentativi configurati) oppure marcare l'utente come "Fuori dalla stanza". Se invece la chiamata ha esito positivo (l'utente riceve la chiamata e accetta l'inserimento nella stanza) allora questo passa nello stato "Nella stanza".
  - **Sospeso**: questo stato esclude temporaneamente un partecipante dalla stanza, ne sospende gli inviti e lo esclude dal computo dei partecipanti che concorrono alla valutazione di completezza della stanza.
  
  
  Le azioni disponibili per ciascun partecipante riguardano la sua partecipazione alla stanza e l'abilitazione o disabilitazione del suo microfono. Le azioni disponibili dipendono dallo stato dell'utente:

- se l'utente si trova nello stato "Fuori dalla stanza" ed ha una politica di invito manuale, oppure la stanza ha il servizio di invito non attivo, oppure ancora il servizio di invito è attivo ma sono terminati tutti i tentativi di invito per questo utente, sono disponibili le azioni "Invita" (cornetta) e "Sospendi" (icona stop). La prima azione effettua la chiamata verso la selezione dell'utente per inserirlo nella stanza (con eventuali ripetizioni in caso di insuccesso, se previsto per questo utente); la seconda lo porta nello stato "Sospeso".
- se l'utente si trova nello stato "Sospeso" è disponibile l'azione "Invita", che causa l'esecuzione di una chiamata verso la selezione dell'utente per inserirlo nella stanza (con le eventuali ripetizioni, come indicato sopra).
- se l'utente di trova nello stato "Nella stanza" è disponibile l'azione "Riaggancia" che abbatte la chiamata di questo utente e, nel caso in cui l'utente abbia politica di chiamata automatica, ne sospende l'esecuzione, per evitare che venga nuovamente reinserito in conferenza).

E' inoltre possibile andare a comandare il "mute" (disabilitazione del microfono) per i partecipanti che si trovano nella stanza, singolarmente o per tutti i partecipanti; nel primo caso la commutazione dello stato del microfono si effettua cliccando sull'icona a forma di microfono presente nella colonna "Azioni", mentre per agire su tutti i partecipanti si utilizzano i due pulsanti presenti sopra la lista dei partecipanti (e che riportano le voci "Disabilita tutti i microfoni" e "Abilita tutti i microfoni").

Blacklist su linee di ingresso
-----------

.. note::

   Introdotto in Release: 4.5.17
   
Descrizione del servizio
++++++++
Questo servizio consente di definire un instradamento specifico per le chiamate in ingresso in base alla coppia numero chiamante e numero chiamato.
Per ogni coppia è possibile stabilire se riprodurre un file audio (anche “in progress”) e definire l’azione di trabocco da effettuare (una qualsiasi delle azioni di instradamento presenti su KPBX).
Le coppie per cui deve essere applicata la stessa politica di instradamento possono essere raggruppate in blacklist da riutilizzare su diverse linee di ingresso.
Le blacklist si applicano alle chiamate entranti, pertanto in uno scenario single tenant possono essere agganciate ai gateway ed ai domini VoIP. Nel caso di multitenant le blacklist sono gestite dai singoli amministratori di tenant e vengono agganciate alle linee assegnate.
Ad ogni linea in ingresso è possibile associare un elenco di blacklist che verranno applicate in cascata dopo l’applicazione delle regole di manipolazione e prima delle regole DID associate alla linea.

Configurazione del servizio
+++++++++
La configurazione del servizio richiede di definire prima la blacklist e quindi associarla alla linea di ingresso su cui deve essere applicata.

La configurazione della blacklist e delle regole che la compongono viene effettuata nel pannello PBX -> Gateway e domini VoIP -> Lista delle blacklist.

**Nel caso di PBX multitenant la configurazione viene effettuata nel pannello PBX -> Gestione delle linee assegnate -> Lista delle blacklist.**

In questo pannello è possibile creare una nuova blacklist attraverso il pulsante “Aggiungi blacklist” oppure editarne una esistente.


I campi principali del form per la definizione della blacklist sono i seguenti:

- Abilitazione
- Nome
- Trabocco
- Regole

Le regole sono ordinabili ma anche l’ordinamento, come le note, ha uno scopo puramente gestionale per raggruppare logicamente delle regole. Avendo tutte la stessa azione di failover, il primo match innesca l’azione.

L’associazione della blacklist alla linea di ingresso viene effettuata su gateway e domini VoIP nel pannello PBX -> Gateway e domini VoIP -> Linee in ingresso / uscita
Nel caso di PBX multitenant la configurazione viene effettuata nel pannello PBX -> Gestione delle linee assegnate -> Linee assegnate.
Indipendentemente dallo scenario in cui ci troviamo l’assegnazione viene sempre fatta cliccando su “Aggiungi blacklist” ed aggiungendo tutte le blacklist necessarie.

È possibile disabilitare ogni singola associazione delle blacklist con la linea in ingresso in modo che le regole contenute non vengano valutate.
È possibile anche modificare l’ordinamento delle blacklist all’interno delle linee in ingresso, in modo da implementare sia meccanismi di blacklist che di whitelist.


Campagne di avviso
---------

.. note::
   Questo servizio è disponibile a partire dalla versione firmware 4.9.4 in poi.
   
Descrizione del servizio
+++++++
Il servizio “Campagne di avviso” presente sul Kalliope PBX, permette di effettuare una sessione di chiamate automatiche verso un gruppo di destinatari, riproducendo a ciascuno un messaggio audio e registrando la conferma di avvenuto ascolto da parte di ciascuno di essi.

A livello generale, il nuovo servizio consente la configurazione, tramite pannello WEB delle campagne di avviso, ciascuna caratterizzata da un insieme di parametri specifici:

- **lista dei partecipanti** (interni ed esterni al PBX)
- **messaggio da riprodurre**
- **numero massimo di chiamate esterne contemporanee**
- **necessità di acquisire o meno le conferme di risposta e di ascolto**
- **numero di tentativi di chiamata verso ciascun destinatario**

Un utente con gli adeguati diritti può operare sulle campagne configurate per comandarne l’avvio (istantaneo o ritardato), visualizzarne lo stato di esecuzione, comandarne la sospensione o l’interruzione.
Una campagna terminerà nel momento in cui per ciascuno dei destinatari configurati si verifichi una delle seguenti condizioni:

- il destinatario risponde alla chiamata e fornisce conferma di risposta e/o di ascolto (se richieste); questa condizione indica il “successo” nel contatto del destinatario
- viene raggiunto il numero massimo di tentativi di chiamata verso quel destinatario, senza che sia soddisfatta la condizione precedente.

Nel caso in cui tutti i destinatari (o il numero minimo richiesto per quella specifica campagna) siano stati contattati con successo, la campagna passa nello stato “Completata”; in caso contrario, al momento dell’esaurimento dei tentativi di chiamata verso tutti i destinatari, la campagna passa nello stato “Incompleta”. In quest’ultimo stato, l’utente può assegnare ulteriori tentativi di chiamata verso uno o più destinatari che non sono stati contattati con successo fino ad allora, oppure marcare come definitivamente chiusa la campagna, portandola nello stato “Terminata”.
Oltre alla gestione in tempo reale delle singole campagne di esecuzione delle campagne di avviso (con visualizzazione dello stato per ciascun destinatario) è possibile accedere ad un registro storico di esecuzione delle campagne concluse: nel registro di queste esecuzioni sono salvati sia agli eventi relativi all’esecuzione della campagna che tutti i parametri di configurazione di esecuzione della stessa, così da poterli consultare anche in caso di modifica della configurazione della campagna o la sua eventuale cancellazione.

Configurazione del servizio
+++++++

Il servizio delle Campagne di avviso viene configurato nel pannello **“Applicazioni PBX” -> “Campagne di avviso”**. La visibilità del pannello e dei relativi tab è condizionata ai permessi associati al ruolo dell’utente.
Il pannello delle Campagne di avviso prevede tre tab:

- **Lista Modelli e Lista Campagne** (associate all’abilitazione “Gestione delle Campagne di Avviso”)
- **Impostazioni generali** (associate all’abilitazione “Gestione delle Impostazioni generali delle Campagne di avviso”)

Nel pannello “Impostazioni generali” è possibile configurare i limiti globali del servizio, in termini di numero massimo di campagne attive simultaneamente, e di numero massimo di chiamate contemporanee (a interni, a esterni, e complessive) tra tutte le campagne attive ad un certo momento. I parametri di configurazione sono:

- **Numero massimo di campagne simultanee attive**: indica il numero massimo di campagne che possono essere contemporaneamente nello stato “Attiva”.
Il parallelismo riguarda l’effettiva esecuzione delle chiamate delle campagne, per cui ad esempio con grado di parallelismo 1 è possibile avviare una campagna anche in caso di una altra campagna già in esecuzione. Le campagne saranno ordinate in base all’attributo “priorità”, ed in caso di parità in base all’ora di avvio, e il sistema effettuerà le chiamate scegliendo i destinatari dalla campagna a priorità maggiore (entro i vincoli di contemporaneità di chiamata globali e di singola campagna). Il valore vuoto indica illimitato.
- **Contemporaneità massima chiamate totali/interne/esterne**: questi tre valori determinano il numero massimo di chiamate contemporanee che il sistema può effettuare tra tutte le campagne attive. Il valore vuoto indica nessun limite. **NOTA**: La somma dei limiti impostati per le chiamate interne ed esterne può eccedere il limite totale, ma comunque il numero di chiamate effettivamente in esecuzione non lo potrà superare (Es. con i valori 10/8/6, possono esserci al più 8 chiamate interne, 6 chiamate esterne, ma complessivamente non più di 10 chiamate; se quindi ad un dato momento sono in esecuzione 7 chiamate interne, potranno essere attive al massimo 3 chiamate esterne)

Ogni volta che una chiamata di una campagna termina (con successo o meno), oppure quando viene attivata una nuova campagna, lo scheduler delle chiamate (che si occupa di determinare se è possibile effettuare una nuova chiamata e verso quale destinatario tra tutti quelli possibili per le varie campagne) opera utilizzando il valore corrente di tali limiti.

Per poter avviare una Campagna, è necessario che prima venga definito un Modello di campagna, a cui sono associati un insieme di parametri che determinano il comportamento delle campagne attivate a partire da quel modello, e quindi venga avviata (o programmata ad una certa data/ora nel futuro) la Campagna a partire da quel modello. Da uno stesso modello possono essere avviate più campagne, in tempi diversi, modificando per ciascuna di esse un sottoinsieme dei parametri di configurazione ereditati dal modello, come il file audio da riprodurre o l’elenco dei destinatari.


La prima operazione da fare per attivare una Campagna è quindi creare un Modello, dal pannello “Lista Modelli”, cliccando sull’azione “Aggiungi nuovo modello di campagna”.
Il pannello di creazione (o modifica) di un Modello di Campagna permette la configurazione dei seguenti parametri:

- **Abilitato**: check-box che indica se il Modello è abilitato. Se un Modello è disabilitato non possono essere avviate o pianificate Campagne che lo utilizzano
- **Nome**: nome della Campagna. Ammette caratteri alfanumerici, spazi, trattini, underscore. Questo attributo viene utilizzato come Display-Name per le chiamate effettuate dalla Campagna verso i destinatari
- **Numero chiamante**: è il numero chiamante utilizzato dal sistema per effettuare le chiamate della campagna. Viene utilizzato sia per le chiamate ad altri interni che per le chiamate a numeri esterni. Nel caso di chiamate esterne il numero chiamante effettivo sarà derivato da questo in base alle regole di manipolazione configurate per la linea di uscita che sarà impegnata.
- **Classe di instradamento in uscita**: determina l’instradamento delle chiamate verso i destinatari esterni. Nel caso in cui la classe non permetta di chiamare uno o più dei destinatari configurati, le relative chiamate falliranno ma non viene effettuato un controllo preventivo.
- **Priorità**: questo valore viene utilizzato dallo scheduler di generazione delle chiamate nel momento in cui si libera lo spazio per una nuova chiamata se sono presenti 2 o più campagne attive.
- **File audio**: selezione del file audio da riprodurre a ciascun destinatario.
- **Soglia di completamento**: questo parametro indica il numero di destinatari che è sufficiente contattare con successo per considerare la campagna completa.
- **Numero di tentativi di chiamata**: questo parametro indica il numero massimo di tentativi di chiamata (senza successo) che possono essere effettuati verso il destinatario. Al raggiungimento di tale numero di chiamate senza che il destinatario abbia risposto e dato conferma (di risposta o ascolto, se richieste), il sistema non effettuerà più nuovi tentativi di chiamata verso questo destinatario, che risulterà quindi “non contattato” in modo definitivo. È facoltà dell’utente che gestisce la campagna di poter aggiungere nuovi tentativi di chiamata verso quei destinatari per i quali sia stato esaurito questo limite. Questo valore non può essere illimitato (default 5).
- **Timeout per chiamata**: il timeout di squillo (in secondi) per ciascuna chiamata effettuata dalla campagna
- **Richiedi conferma di risposta**: questa check-box indica se il sistema deve richiedere al destinatario la digitazione del tasto 1 per confermare che abbia effettivamente risposto, prima di effettuare la riproduzione del messaggio. Questa impostazione vale sia per i destinatari interni che esterni, ed assicura che la chiamata non sia andata ad un risponditore o casella vocale.
- **Richiesta conferma ascolto**: questa check-box indica se il sistema deve richiedere al destinatario la digitazione del tasto 9 al termine dell’ascolto del messaggio, a conferma dell’effettivo ascolto e comprensione di questo. La mancata conferma o la pressione di un tasto diverso da quello indicato causa la ripetizione del messaggio. Se la chiamata viene abbattuta senza conferma di ascolto, il sistema considererà il destinatario come “non contattato”, e se il destinatario ha ancora tentativi residui (perché non ha raggiunto il numero massimo di tentativi di chiamata configurati per la campagna) potrà essere nuovamente chiamato in seguito, in base alle politiche di scheduling del servizio.
- **Contemporaneità massima chiamate interne/esterne/totali**: questi 3 valori determinano il numero massimo di chiamate che questa campagna può effettuare complessivamente, verso destinatari interni e verso destinatari esterni. Un valore “null” indica nessun limite. La somma dei limiti impostati per le interne e le esterne può eccedere il limite totale, ma comunque il numero di chiamate effettivamente in esecuzione non lo potrà superare.
- **Elenco destinatari**: questo elenco viene popolato con destinatari interni o esterni. Nel caso di contatti inseriti manualmente, oltre al numero si possono specificare un nome ed un indirizzo mail (per l’invio del messaggio). L’elenco è ordinabile; lo scheduler delle chiamate utilizzerà tale ordinamento in fase di selezione della prossima chiamata da effettuare, a parità degli altri parametri.


Una volta creato il modello questo apparirà nel pannello “Lista Modelli”, da cui l’utente abilitato può effettuare le seguenti operazioni:

- **Creare un numero arbitrario di Modelli di Campagne**
- **Cancellare uno o più Modelli di Campagna esistenti** selezionando l’icona Cestino. Nel caso di un Modello da cui siano state avviate o programmate una o più Campagne, la cancellazione è permessa, in quanto tutti i parametri necessari all’esecuzione della campagna di avviso sono stati già copiati dal modello nella configurazione operativa di quella campagna. All’utente viene comunque indicata l’esistenza di campagne in corso o schedulate associate a tale Modello, mediante pop-up di conferma cancellazione.
- **Clonare un Modello esistente per crearne una nuova**, che ne eredita le impostazioni
- **Modificare la configurazione di un Modello di Campagna** precedentemente creata; nel caso di una Campagna per la quale esistano una o più istanze in esecuzione o schedulata, la modifica è comunque permessa a seguito dell’indicazione mediante il pop-up di conferma.
- **Visualizzare la lista dei destinatari** della Campagna.

Avvio e gestione di una campagna di avviso
++++++++
Dopo aver configurato un modello di campagna di avviso, l’utente può comandare l’avvio di una campagna, immediato o differito nel tempo.
La creazione della Campagna si effettua cliccando sull’icona “Avvia” nella colonna “Azioni” della Lista Modelli. Viene aperto un pannello intermedio “Avvio nuova campagna di avviso” in cui è possibile assegnare un nome alla specifica campagna, effettuare l’eventuale modifica (rispetto al modello di origine) del file audio da riprodurre e dell’elenco dei destinatari.
Infine, è possibile definire la programmazione della campagna secondo tre modalità:

- **Immediata**: la campagna viene avviata immediatamente alla pressione del pulsante “Avvia”
- **Ritardata**: selezionando il tempo (in minuti) dopo il quale la campagna viene avviata
- **Orario programmato**: specificando una data ed ora a cui la campagna verrà avviata


Alla conferma, selezionando premendo sul tasto “Avvia”, la nuova campagna (avviata o programmata) compare nel pannello “Lista Campagne”.
Questo pannello costituisce un registro delle campagne passate ed anche di quelle correnti, tramite il quale è possibile visualizzare lo stato istantaneo della campagna, il grado di avanzamento delle chiamate, oltre ad alcuni parametri di configurazione. La vista delle campagne mostra le seguenti informazioni:

- Come parametri di configurazione sono mostrati: Nome, Modello, numero chiamante, priorità, timeout di squillo, tentativi massimi per destinatario, valore della soglia di completamento, richiesta di risposta e conferma di ascolto, contemporaneità.
- Programmazione Avvio: l’ora prevista di inizio della campagna
- Destinatari totali: il numero totale dei destinatari della campagna
- Destinatari contattati con successo: Destinatari che hanno risposto alla campagna secondo le impostazioni della campagna stessa
- Chiamate in corso: numero delle chiamate attualmente in corso per quella campagna
- Stato: indica lo stato in cui si trova la campagna e può essere uno dei seguenti:
   - Programmata: al momento dell’attivazione. Da questo stato passa nello stato “In esecuzione” in caso di avvio immediato, o al momento previsto dalla schedulazione se avviata in modalità differita
   - In esecuzione (o Attiva): quando vengono eseguite le chiamate verso i destinatari di questa campagna.
   - Sospesa: attivabile dall’utente premendo il pulsante “Sospendi”. In questo stato non vengono generate nuove chiamate per i destinatari appartenenti a questa campagna; le chiamate in corso non vengono interrotte.
   - Bloccata: quando si eccede il grado di parallelismo previsto per le campagne
   - Incompleta: quando sono state eseguite tutte le chiamate possibili verso i destinatari ma almeno uno di questi non è stato contattato con successo. Nel caso in cui un destinatario passi dallo stato “Fallito” allo stato “Idle” (perché un utente gli ha assegnato nuovi tentativi di chiamata) allora la campagna torna in stato “Attiva” assegnando nuovi tentativi di chiamata per uno o più destinatari. In alternativa l’utente può chiuderla definitivamente portandola nello stato “Terminata” cliccando sull’icona “STOP”
   - Terminata: quando la campagna è finita, anche con alcuni destinatari non contattati in via definitiva, e non possono essere più eseguite chiamate verso i suoi destinatari. L’utente, per una campagna Incompleta, può mettere la campagna in questo stato usando il tasto corrispondente.
   - Completata: Si arriva in questo stato in modo automatico, nel momento in cui tutti i destinatari della campagna siano stati contattati con successo
   
   
Oltre a questo pannello di summary delle campagne presente un “Pannello di stato della campagna” che raccoglie tutte le informazioni relative allo stato ed allo storico della campagna.
In questo pannello (a cui si accede cliccando sull’icona della lente di ingrandimento) viene visualizzato anche l’elenco dei destinatari e per ciascuno di essi lo stato corrente: ultima volta che è stato chiamato, esito, numero di tentativi di chiamata, timestamp di ultima risposta e di ascolto, l’elenco dei tentativi di chiamata con i relativi eventi e timestamp. All’interno di questo pannello è possibile per l’utente comandare azioni relative alla campagna (sospendi e termina) e al destinatario (interrompi tentativi di chiamata, assegna ulteriori N tentativi, …).
Nel pannello sono visibili i cambi di stato di un destinatario, che sono pilotati dall’avvio e termine delle chiamate dirette ad esso, e possono causare il cambio di stato della campagna a cui appartengono:

- **Idle**: inattivo, disponibile ad essere chiamato (se la campagna si trova in stato “Attiva”)
- **Attivo**: è in corso una chiamata
- **Contattato**: è stato contattato con successo e sono state date le conferme richieste (risposta e ascolto, se previste)
- **Fallito**: è stato fatto un numero di tentativi di chiamata pari al massimo previsto, senza che sia stato contattato con successo. Da questo stato l’utente può assegnare altri tentativi di chiamata a quel destinatario, che torna quindi nuovamente nello stato “Idle”.


Logica di scheduling delle chiamate
++++++++
La logica con cui il sistema decide l’esecuzione di una nuova chiamata verso un destinatario appartenente ad una certa campagna dipende da numerosi parametri:

- Contemporaneità massima delle campagne
- Contemporaneità massima delle chiamate complessive (totali/interne/esterne)
- Contemporaneità massima delle chiamate per campagna (totali/interne/esterne)
- Priorità delle campagne
- Timestamp di avvio di ciascuna campagna
- Timestamp dell’ultimo tentativo di chiamata verso ciascun destinatario (con esito negativo)

Le campagne attive ad un dato momento vengono ordinate in base alla priorità, ed in caso di parità viene data precedenza alla campagna con timestamp di avvio precedente.
Partendo dalla campagna a massima priorità, il sistema genera tante chiamate fino al raggiungimento delle contemporaneità massime (della campagna e complessive). Vengono chiamati per primi i destinatari che non sono stati chiamati in precedenza, secondo l’ordine con cui sono elencati nella configurazione della campagna. Nel caso in cui si sia raggiunto un limite di contemporaneità, ad esempio per le interne, il sistema continuerà a selezionare destinatari da quella campagna, scegliendolo solo da quelli esterni. Quando si esauriscono i destinatari che non sono mai stati chiamati, se c’è ancora posto per ulteriori chiamate per quella stessa campagna, il sistema passa a richiamare i destinatari già chiamati in precedenza, partendo da quelli che sono stati chiamati più lontano nel tempo. Nel momento in cui non sia possibile selezionare un nuovo destinatario da questa campagna lo scheduler ripete la valutazione sulla seconda campagna (per priorità/tempo di avvio), e così via fino al raggiungimento dei limiti complessivi di chiamata o all’esaurimento di destinatari disponibili.
Ogni volta che una chiamata termina, oppure ogni volta che viene avviata una nuova campagna, oppure quando vengono modificati i limiti globali del servizio, viene eseguito di nuovo l’algoritmo di scheduling per determinare se è possibile effettuare una o più nuove chiamate.

Fast Transfer
-----

Descrizione Funzionale
+++++++
Il servizio di Fast Transfer consente ad un interno di trasferire la chiamata in corso ad un numero mobile precedentemente associato all’interno stesso. Questa funzione può essere utilizzata ad esempio per proseguire sul telefono cellulare una conversazione anche se si ha necessità di lasciare la propria postazione di lavoro.

Quando viene attivato questo servizio il KalliopePBX effettua una chiamata verso il numero cellulare impostato e una volta stabilita la comunicazione effettua il bridging della chiamata originale in ingresso con la nuova chiamata verso il cellulare. La comunicazione resta pertanto sempre ancorata sul centralino.

E’ quindi possibile anche ritornare in comunicazione sul proprio interno (analogamente al primo trasferimento il KalliopePBX contatta dapprima l’interno e quindi interconnette i canali di chiamata).

Operativamente l’utente che vuole trasferire la chiamata verso il proprio cellulare e viceversa deve semplicemente digitare il codice di trasferimento rapido (default **). Non appena l’utente risponde sul dispositivo destinatario del trasferimento la chiamata verso il dispositivo originale viene abbattuta e la comunicazione prosegue sul nuovo dispositivo.

Configurazione
++++++++
Per l’abilitazione globale del servizio di Fast Transfer è necessario attivare nel pannello Servizi in chiamata il Codice trasferimento rapido (da/verso mobile) ed eventualmente modificare il codice da utilizzare.

Per abilitare il servizio per lo specifico interno è invece sufficiente inserire il numero mobile nel pannello di definizione dell’interno.

Fork to Mobile
----

Descrizione Funzionale
++++++++
Il servizio Fork2Mobile consente di inoltrare la chiamata diretta ad un interno anche ad un numero mobile precedentemente associato all’interno stesso. Questa funzione può essere utilizzata per ricevere le chiamate anche quando si è lontani dalla propria postazione di lavoro. Il sevizio funziona per chiamate dirette e per le chiamate a gruppi ma non funziona per le chiamate alle code.

Quando viene attivato questo servizio il KalliopePBX inoltra la chiamata in ingresso non solo agli account associati all’interno ma anche verso un numero cellulare predefinito. Una volta stabilita la comunicazione verso l’utenza mobile il KalliopePBX richiede dapprima conferma che si tratti effettivamente della risposta di un utente (potrebbe trattarsi di un servizio di casella vocale o richiamata) e quindi effettua il bridging della chiamata originale in ingresso con la nuova chiamata verso il cellulare. Le chiamate verso gli altri dispositivi smettono di squillare non appena uno dei terminali risponde. La chiamata verso il numero mobile segue le regole di instradamento in uscita associate all’interno ed il numero presentato coinciderà sempre con quello che utilizza l’interno quando comunica verso la rete telefonica pubblica. La chiamata verso il mobile non contiene pertanto alcuna informazione in merito al chiamante originale.

Se però sul telefono è attiva e connessa l’applicazione KalliopeCTI Mobile, il KalliopePBX invia il numero chiamante originale all'applicazione che la notifica all'utente. In questo modo l’utente può decidere se rispondere dopo aver verificato chi lo sta contattando.

Le differenza tra questo servizio e il servizio di Inoltro Incondizionato su utenza mobile sono due:

- Nel servizio Fork2Mobile il numero di cellulare associato all’interno è preconfigurato e non può essere modificato in fase di attivazione del servizio
- Nel servizio Fork2Mobile tutti gli account dell'utente squillano contemporaneamente all'utenza mobile fino a quando uno dei terminali non risponde mentre nell'Inoltro Incondizionato la chiamata viene deviata esclusivamente al cellulare.

Operativamente l’attivazione/disattivazione del servizio Fork2Mobile può essere effettuata in 3 modalità:

- **Da telefono**: il servizio viene attivato digitando il codice di attivazione (default *501). Il KalliopePBX conferma l’attivazione del servizio riproducendo il file audio “Salvato”. Analogamente la disattivazione avviene digitando il codice relativo (default *500). In questo caso il KalliopePBX conferma la disattivazione con il messaggio “Grazie”. Esistono anche dei codici che consentono di commutare lo stato (default *50*) e verificare lo stato del servizio (default *509). Questi codici possono essere utilizzati esclusivamente da un dispositivo associato all’interno su cui deve essere effettuata l’attivazione / disattivazione.
- **Da KalliopeCTI Desktop (in tutte le modalità)**: se il servizio Fork2Mobile è attivo per l’interno, sotto la casella di composizione del numero appare l’icona Kcti *jpg*. Cliccando sull'icona il servizio viene attivato e l’icona diventa Kcti *jpg*. La disattivazione viene effettuata cliccando nuovamente sull'icona. Posizionando il puntatore del mouse sull'icona è anche possibile visualizzare il numero mobile utilizzato dal servizio.
- **Da KalliopeCTI Mobile**: l’attivazione viene effettuata cliccando sul simbolo della ruota dentata jpg* nell'angolo in basso a destra e quindi cliccando sull'icona Mobile jpg* che identifica il Servizio Fork2Mobile. Quando il servizio è attivo l’icona si modifica *jpg*. Per disattivare il servizio è sufficiente cliccare nuovamente sull'icona. Se il servizio è disattivato per l’interno cliccando sull'icona non cambierà lo stato dell’icona stessa.

Quando è attivo il servizio e l'utente risponde sul telefono cellulare, viene riprodotto al chiamato il seguente messaggio audio “premere 1 per accettare la chiamata”.

Se l'utente digita 1 viene messo in comunicazione con il chiamante e le altre chiamate vengono cancellate.

Se l'utente digita un altro numero la chiamata verso il cellulare viene conclusa e gli altri terminali continuano a squillare.

Nel caso in cui l'utente non digiti nulla (come nel caso in cui la chiamata sia trasferita alla casella vocale dell’operatore mobile) dopo un timeout di 15 secondi la chiamata viene riagganciata.

Configurazione del servizio
+++++++++

Il servizio Fork2Mobile è sempre attivo a livello globale. Per abilitare il servizio per lo specifico interno è però necessario inserire il numero mobile nel pannello dell’interno.

L’abilitazione dei codici di attivazione / disattivazione da telefono e l’eventuale modifica sono gestiti nel Piano di Numerazione.


Interoperabilità con dispositivi di terze parti
++++++++++
Quando l’attivazione / disattivazione del servizio viene effettuata da telefono può essere molto utile avere a disposizione un tasto (con campo lampade) che consenta di verificare lo stato del servizio ed eventualmente commutarne lo stato.

Per quanto riguarda il monitoraggio, il KalliopePBX invia dei messaggi SIP NOTIFY per comunicare i cambi di stato del servizio. Il telefono dovrà inviare una SIP SUBSCRIBE per richiedere l’invio delle informazioni di stato.

Questa operazione è normalmente effettuata configurando un tasto funzione di tipo BLF. L’oggetto da monitorare è forkm<interno>. Sullo stesso tasto viene anche automaticamente impostata la chiamata al codice di commutazione (default *50*) per attivare / disattivare il servizio.

Esempi di configurazione
++++++
**Su SNOM**

- Operando tramite la web gui di configurazione configurare Function keys con

.. code-block:: console

   Account: selezionare dalla tendina l’account che stiamo utilizzando (se c’è un solo account configurato sul telefono è il primo della lista)
   Type: BLF
   value: forkm<interno>
   
- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">blf sip:forkm<interno>@%%KPBX_IP_ADDRESS%%;user=phone</fkey>
   
Dove %%id%% è l’identificativo del tasto da configurare E %%line_id%% è l’identificativo dell’account associato (il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console

   <fkey idx="0" context="1" label="forking2mobile 105" perm="">blf sip:forkm105@192.168.23.112</fkey>
   
**Su YEALINK**

- Operando tramite la web gui di configurazione configurare DSS Key con:

.. code-block:: console
   
   Type BLF
   Value: forkm<interno>
   Line: La linea associata all’account che stiamo utilizzando (Line 1 se sul telefono è presente un solo account)

- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   memorykey.%%id%%.line=%%line_id%%>
   memorykey.%%id%%.value=forkm<interno>
   memorykey.%%id%%.type=16
   
Dove %%id%% è l’identificativo del tasto da configurare

e %%line_id%% è l’identificativo dell’account associato il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console

   memorykey.2.line = 1
   memorykey.2.value = forkm105
   memorykey.2.type = 16
   memorykey.2.pickup_value = %NULL%
   memorykey.2.xml_phonebook = %NULL%

Gruppi chiusi di interni
--------

.. note::
   Introdotto in Release: 4.5.5

Descrizione Funzionale
+++++
Questo servizio consente all’amministratore del PBX di restringere la possibilità di chiamare uno o più interni solamente ad un elenco di interni abilitati.
Se un interno appartiene ad un gruppo chiuso potrà essere contattato solamente dagli utenti autorizzati alla chiamata su quel gruppo.

Configurazione del servizio
+++++++++
La configurazione del servizio viene effettuata direttamente nel pannello di configurazione dell’interno nella sezione Gruppi Chiusi di Interni. In questa sezione è possibile impostare per l’interno l’appartenenza ad uno o più gruppi e l’autorizzazione ad effettuare chiamate su uno o più gruppi.

Esempio
++++++
Impostare per l’interno 101 l’appartenenza al gruppo 1 e l’autorizzazione alla chiamata per i gruppi 1 e 2.
Impostare invece per l’interno 102 l’appartenenza al gruppo 2 e l’autorizzazione alla chiamata solo per il gruppo 2.
Effettuando una chiamata da 101 a 102 questa viene correttamente instaurata.
Se invece si effettua la chiamata da 102 a 101 la chiamata non viene instaurata poichè 102 non è autorizzato alla chiamata su un gruppo di interni a cui appartiene 101.


Hot desking
--------


Descrizione del servizio
+++++++++
Il servizio di Hot Desking consente di associare l'identità telefonica di un utente configurato sul KalliopePBX ad un qualsiasi dispositivo abilitato al servizio.
In questo modo l'utente potrà ricevere le chiamate dirette alla propria extension, mantenere le proprietà telefoniche (ad es. numero chiamante, regole di instradamento, politiche di trabocco) ed un unico registro chiamate indipendentemente dal terminale utilizzato.
L'accesso al servizio avviene tramite una procedura di login autenticata dal PIN dei servizi dell'utente.
Nel caso in cui l'utente risulti già loggato in Hot Desking su un altro terminale questo viene immediatamente scollegato mentre tutti i terminali associati staticamente all'utente mantengono invece il proprio stato di registrazione.
Le chiamate in ingresso saranno pertanto presentate contemporaneamente a tutti i terminali statici e ad un unico terminale di Hot Desking.
Il livello di occupato e il numero di chiamate contemporanee per ogni utente è definito nel pannello Interni nel quale vengono specificate le proprietà telefoniche dell'utente.
Operativamente l'attivazione del servizio di Hot Desking avviene effettuando una chiamata al proprio numero di interno da un terminale a cui non è associato alcun interno.
Il KalliopePBX richiede quindi tramite prompt vocale la "Password". L'utente deve quindi inserire il proprio PIN dei servizi seguito dal tasto # (se il tasto # non viene premuto il sistema invia comunque il comando dopo 5 secondi dalla digitazione dell'ultimo tasto). Il sistema conferma l'accesso riproducendo il file audio "Login effettuato". Al termine di questa operazione viene effettuata la riconfigurazione dinamica del telefono e sul display del telefono compaiono i dati dell’utente.
La disattivazione del servizio avviene digitando il codice di Logout del servizio di Hot Desking (default *400).

Requisiti per l’attivazione del servizio
++++++++
Per attivare il servizio di Hot Desking su un terminale è necessario che la configurazione sia interamente gestita mediante Auto-Provisioning e che il terminale supporti il meccanismo di aggiornamento della configurazione tramite SIP NOTIFY.
Questo meccanismo è messo a disposizione da diversi produttori di telefoni (Snom, Yealink, Gigaset, Polycom, etc.).
Per l'elenco completo dei telefoni certificati e delle relative versioni firmware consultare la sezione Interoperabilità con dispositivi di terze parti.

Configurazione del servizio
+++++++++
La configurazione del servizio Hot Desking interessa vari punti dell’interfaccia web di KalliopePBX.
La configurazione principale si effettua tramite il pannello omonimo, raggiungibile dal menu “Applicazioni PBX”, ma sono interessati anche i pannelli di configurazione degli interni (e dei template) ed il piano di numerazione
Prima di configurare il servizio è necessario, come operazione preliminare, andare a inserire i device (comprensivi di modello, indirizzo MAC e indirizzamento IP) nel pannello di provisioning, senza assegnargli un account SIP. Può essere omesso anche il template da assegnare perché verrà configurato nel pannello Hot Desking.
Dal pannello Hot Desking si assegna ai dispositivi desiderati (scelti tra quelli definiti nel pannello provisioning ma per i quali non sia associato un SIP account) la modalità di utilizzo Hot Desking. Il sistema genera in automatico un account SIP dedicato allo specifico terminale (hotdesk-<mac>), utilizzato nella configurazione “a vuoto” del terminale per permettere l’esecuzione della chiamata per il login.
A ciascun interno abilitato all’utilizzo del servizio Hot Desking deve essere abilitato il corrispondente flag di configurazione (eventualmente via template); in questo modo viene generato in automatico un SIP account dedicato (hotdesk-<interno>) che sarà utilizzato per generare la configurazione del terminale da usare in seguito al login. A questo account deve essere associato anche un template di SIP account.
NOTA: Il flag di abilitazione Hot Desking ed il template di SIP account sono parametri di configurazione presenti nel template dell’interno e sovrascrivibili.


Descrizione pannello Hot Desking
.........
I parametri di configurazione per l’abilitazione dei dispositivi al servizio di Hot Desking sono:

- **Il dispositivo di provisioning**: il terminale definito nel pannello di provisioning per il quale si vuole abilitare il servizio di Hot Desking
- **Il template di provisioning**: il template da utilizzare per generare il file di provisioning del terminale
- **Il template dell'account SIP**: il template SIP da utilizzare per l’account SIP generato automaticamente ed utilizzato nella configurazione “a vuoto” del terminale.

Abilitazione degli interni
..........
L’abilitazione degli interni all’utilizzo del servizio di Hot Desking può essere configurata sui template degli interni (quindi ereditata da tutti gli interni che fanno uso del template), oppure sui singoli interni tramite il meccanismo di override dei valori del template assegnato.
I parametri di configurazione per l’abilitazione all’utilizzo dell’Hot Desking nel pannello dei template degli interni sono:

- **Il flag abilita all'utilizzo dell'hot desking**: autoesplicativo
- **Il template SIP da assegnare all'account hot desk**: il template SIP da utilizzare per l’account SIP generato automaticamente ed utilizzato in seguito al login dell’utente sul terminale di Hot Desking.
Gli stessi due parametri sono presenti nel pannello degli interni con i relativi flag di override rispetto a quanto configurato nel template.

Abilitazione del servizio
.........
Per poter utilizzare la funzionalità è necessario abilitare il servizio Hot Desking dal pannello Piano di numerazione.

Interoperabilità con dispositivi di terze parti
++++++++
Il servizio è stato testato con terminali SNOM e Yealink secondo la seguente tabella di compatibilità:

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1
   
   * - Marca
     - Serie/Modello
     - Firmware
   * - Snom
     - D3x5
     - 8.9.3.40
   * - Snom
     - D745
     - 8.9.3.40
   * - Snom
     - D765 / D725 / D715 / D710
     - 8.7.5.35
   * - Snom
     - 3xx
     - 8.7.5.35
   * - Snom
     - 7xx
     - 8.7.5.35
   * - Snom
     - 8xx
     - 8.7.5.35
   * - Yealink
     - T19P / T20P / T21P / T22P / T26P / T28P / T32G / T38G / VP530
     - v70
   * - Yealink
     - T19P E2 / T21P E2 / T23P / T23G / T27P / T29G / T40P / T41P / T42G / T46G / T48G / VP-T49G
     - v80


Altri modelli sono in fase di testing e qualora risultassero compatibili verranno aggiunti alla tabella precedente.
Per i telefoni Yealink, al fine di evitare il reboot del telefono al momento della riprogrammazione, è necessario aggiungere la seguente riga di configurazione al template:

.. code-block:: console

   sip.notify_reboot_enable = 0
   
Instradamento avanzato (ACR)
-------

In questa sezione sono raccolte tutte le configurazioni necessarie a definire le modalità con cui vengono effettuate le chiamate verso numerazioni esterne al PBX.

Classi di instradamento in uscita
++++++

Una classe di instradamento in uscita consiste in un insieme di regole di instradamento in uscita da verificare per stabilire la politica di instradamento da applicare alla chiamata effettuata da un interno e diretta a numerazioni esterne al PBX. Il match delle regole viene eseguito nell'ordine in cui sono visualizzate sulla WEB GUI (dall'alto verso il basso).

Se il match è valido la corrispondente azione viene eseguita e non vengono esaminate ulteriori regole. Per questo motivo è fondamentale che le regole siano disposte dalla più particolare alla più generale. Sarebbe quindi errato disporre per prima una regola generale che, ad esempio, permette di chiamare tutti i numeri senza distinzioni, poiché questo porterebbe all’annullamento di tutte le altre che potenzialmente contengono particolari caratteristiche di differenziazione.

E' possibile riordinare le regole una volta definite semplicemente portandosi sull'icona (aggiungere figura) e spostandosi mantenendo premuto il tasto sinistro del mouse.

Nella tabella seguente sono illustrati i parametri che è possibile definire per ogni classe di instradamento in uscita.

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Abilitato
     - Consente di disabilitare una classe di instradamento in uscita senza perderne la configurazione
     - Si / No
   * - Nome
     - Identificativo della classe di instradamento in uscita
     - Alfa-numerico

**Regole della classe di instradamento in uscita**

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Aggiungi regola
     - Consente di selezionare le regole di instradamento in uscita configurate ed inserirle nell'ordine in cui devono essere riscontrate dal PBX
     - Regola di instradamento in uscita
     
     
Regole di instradamento in uscita
++++++++

Una regola di instradamento in uscita consiste di due componenti:

- un insieme di condizioni da verificare sul numero chiamato. La verifica può essere fatta su un numero telefonico specifico (Selezione Esatta) su un prefisso telefonico (Prefisso) oppure la regola può essere convalidata per qualsiasi numero chiamato (Qualsiasi)
- una lista di linee di uscita che costituiscono la sequenza con cui il PBX prova ad instradare la chiamata. Nel caso di errore su una linea di uscita, il PBX tenta automaticamente di instradare la chiamata sulla successiva. Le condizioni di errore corrispondono a messaggi SIP di tipo 5xx o 6xx oppure alla scadenza del timeout SIP (di default 32 secondi). Quindi se ad es. il PBX riceve il SIP Message 486 Busy Here non effettua alcun tentativo ulteriore di instradamento della chiamata.

Nella tabella seguente sono illustrati i parametri che è possibile definire per ogni regola di instradamento in uscita.

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Abilitato
     - Consente di disabilitare una regola di instradamento in uscita senza perderne la configurazione
     - Si / No
   * - Nome
     - Identificativo della regola di instradamento in uscita
     - Alfa-numerico
   
**Selezioni delle regole di instradamento in uscita**

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Aggiungi selezione
     - Definisce la modalità con cui viene effettuato il match del numero chiamato	  
     - Prefisso / Esatta / Qualsiasi
     
 **Risoluzione ENUM**    

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Abilita risoluzione ENUM
     - Consente di abilitare la risoluzione ENUM per la specifica regola
     - Si / No
   * - Aggiungi impostazione ENUM
     - Consente di definire quali domini di ricerca (definiti nelle impostazioni ENUM) devono essere verificati
     - Impostazioni ENUM
     
**Linee di uscita**    

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore    
   * - Aggiungi linea in uscita
     - Consente di creare la lista di linee da utilizzare in sequenza per le selezioni verificate.
     - Linee uscenti
     
     
Impostazioni ENUM
+++++++++
Una impostazione ENUM si compone di due componenti:

- un insieme di domini di ricerca su cui vengono effettuate le query DNS
- una lista di regole da applicare nel caso in cui il server ENUM risponda positivamente. Il comportamento potrà essere diverso in base all'hostname restituito nella SIP URI.

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore    
   * - Abilitato
     - Consente di disabilitare una impostazione ENUM senza perderne la configurazione
     - Si / No
   * - Nome
     - Identificativo della impostazione ENUM
     - Alfa-numerico

**Domini di ricerca**

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore  
   * - Aggiungi dominio di ricerca
     - Consente di definire quali domini di ricerca devono essere verificati per questa impostazione
     - Nome di dominio
     
**Regole ENUM**

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore   
   * - regola ENUM
     - Consente di definire la regola da utilizzare per instradare la chiamata in uscita nel caso in cui la query DNS su un dominio di ricerca abbia esito positivo. La linea di uscita può coincidere con il dominio ritornato dalla query (chiamata diretta al dominio) oppure è possibile forzare comunque una specifica linea di uscita per l’instradamento on-net (ad esempio nel caso in cui sia necessario utilizzare delle credenziali di autenticazione).
     - Hostname + Linea di uscita / chiamata diretta al dominio.
     
Instradamento dinamico
---------

Questo servizio permette di effettuare l’instradamento di una chiamata in ingresso in base alla risposta ad una API HTTP invocata su un WEB server esterno o al riscontro di uno o più parametri definiti in un file caricato sul PBX.
La richiesta al server web o il riscontro del file possono essere effettuate passando una serie di parametri numerici da richiedere al chiamante tramite prompt vocali pre-registrati.
Per un approfondimento sul funzionamento del servizio Instradamento dinamico si può fare riferimento al video tutorial riportato qui a fianco (a partire dal minuto 37:27).

Configurazione del servizio
++++++++++

La configurazione del servizio viene effettuata nel pannello Applicazioni PBX -> Instradamento dinamico.
In fase di configurazione è necessario specificare i seguenti valori:

- Nome: identificativo dell’instradamento.
- Tipo: richiesta HTTP (Richiesta a WEB server esterno) / (Riscontro su file locale)
- Controllo Orario: indica il controllo orario da verificare prima di eseguire l’instradamento. Il trabocco in caso si voglia eseguire l’instradamento dinamico deve essere impostato a “Ritorna al livello superiore”.
- Parametri: per ciascun parametro (numerico) da richiedere al chiamante, è possibile inserire un messaggio vocale (ad esempio con la richiesta di inserimento) e, opzionalmente, è possibile specificare il massimo numero di cifre inseribili.

Se non viene specificato tale valore, il sistema assume che l’utente abbia terminato l’inserimento del parametro dopo un timeout di 5 secondi, o alla pressione del tasto “#”. In caso di mancata digitazione di una qualsiasi cifra, è prevista la ripetizione della richiesta per un massimo di 3 volte. Il massimo numero di parametri in ingresso è 5.
È infine possibile abilitare la richiesta di conferma, mediante l’apposita checkbox; se abilitata, il sistema ripete all'utente le cifre inserite e chiede di confermare la correttezza dell’inserimento mediante la digitazione del tasto “1”. In caso di assenza di conferma, viene ripetuta la richiesta di inserimento del parametro.

Impostazioni della richiesta
++++++++++

**Richiesta HTTP**
Nel caso in cui la richiesta sia di tipo HTTP devono essere specificate le seguenti impostazioni:

- URL: URL a cui deve essere effettuata la richiesta (è supportato sia il protocollo HTTP che HTTPS).
- Tipo Auth: identifica il tipo di autenticazione utilizzato dal web server, e può assumere uno di questi 3 valori:
   - NONE: nessuna autenticazione
   - BASIC: Basic HTTP Authentication; in questo caso è necessario specificare le credenziali di autenticazione (username e password).
   - Certificato client integrato del PBX (disponibile a partire dal firmware 4.5.9): l'autenticazione della richiesta è effettuata riscontrando l'identità del richiedente mediante certificato client univoco. Tale certificato, integrato in ciascun KalliopePBX, è firmato dalla CA Kalliope ed ha come CN il serial number del PBX (es. CN=KPBX40412345)
- Tipo Request: indica il metodo della richiesta (sono supportati GET e POST).

Nel caso in cui si utilizzi il metodo POST è possibile specificare il formato del corpo della richiesta ed il relativo Content-Type.
Il passaggio dei parametri all’API avviene tramite dei placeholder inseriti nell’URL o nel contenuto del POST; i placeholder riconosciuti sono:

- %CALLER_NUM%: indica il numero chiamante
- %DNID%: indica il numero chiamato
- %PARAM1%, …, %PARAM5%: indica i 5 parametri richiesti al chiamante tramite un menù vocale interattivo.
- %UNIQUE_ID%: indica il codice identificativo univoco della chiamata. Tramite tale identificativo è possibile rintracciare la chiamata sul CDR.

A titolo di esempio, nel caso di richiesta GET l’URL potrebbe essere costruito come:
http://www.myserver.com/api?arg1=%CALLER_NUM%&arg2=%PARAM1%&arg3=%PARAM2%

Nel caso di richiesta di tipo POST, il corpo potrebbe essere:

.. code-block:: console

   <?xml version="1.0"?>
    <parameters>
        <caller>%CALLER_NUM%</caller>
        <param_01>%PARAM1</param_01>
        <param_02>%PARAM2</param_02>
    </parameters>
    
Interno
...........

Nel caso in cui la richiesta sia di tipo interno il file da utilizzare deve essere caricato nella cartella Accesso TFTP tramite il Gestore File.
Il file può avere estensione .xls/.xlsx/.ods/.csv e contenere o meno le intestazioni di colonna. Nel caso negativo deve essere specificato il mappaggio delle colonne, indicando per ciascun campo l’esatta posizione nel file. A tal scopo è importante ricordare che la numerazione delle colonne parte da 0.
Il file sorgente deve essere conforme al seguente template:

.. code-block:: console

   | callerNum | calledNum | param1 | param2 | param3 | param4 | param5 | response | newCallerNameFull | newCallerNamePrefix | newCallerNum|} 
   
Azioni
+++++
In questa sezione si configurano le regole di instradamento da attuare in base alla risposta ottenuta dal Web Server esterno o all'esito del riscontro su file.

Richiesta HTTP
......

Nel caso in cui la richiesta si di tipo HTTP il sistema si aspetta dal server web una risposta di tipo “200 OK”, il cui corpo deve contenere un testo XML come segue:

.. code-block:: console

   <?xml version="1.0"?>
    <response>
        <message>
            <elem>digit:1</elem>
            <elem>number:200</elem>
            <elem>alpha:c234</elem>
            <elem>audio:custom/%TENANT_UUID%/sounds/misc/pluto</elem>
            <elem>number:201</elem>
            <elem>digit:123</elem>
            <elem>audio:custom/misc/pippo</elem>
        </message>
        <displayprefix>testo</displayprefix>
        <value>105</value>
    </response>
    
.. note::
   La stringa %TENANT_UUID% deve essere sostituita con l'attuale valore del UUID specificato nel widget "Informazioni" sulla Dashboard

I tag <message> e <displayprefix> (disponibile a partire dal firmware 4.3.5) sono opzionali; il tag <message> specifica la componente dinamica del prompt audio eventualmente riprodotto all'interlocutore, mentre il tag <displayprefix> permette di modificare il Display Name della chiamata anteponendo a quello corrente un prefisso costituito dalla stringa specificata all'interno del tag stesso.
Il tag <value> è invece obbligatorio ed indica la risposta dell’API in base alla quale vengono definite le azioni di instradamento da compiere.

Ciascuna azione di inoltro (quella di default, quella di errore e quelle associate a specifici valori di risposta) è composta da 3 azioni seuqenziali:

- Riproduzione di un file audio statico caricato sul sistema
- Riproduzione di un contenuto dinamico.
- Inoltro della chiamata ad una nuova destinazione (o riaggancio)

Il contenuto dinamico da riprodurre è descritto dai tag <elem> contenuti all'interno del tag <message> della risposta. Di seguito si riporta la descrizione del formato dei tag <elem> ammessi ed il relativo contributo al contenuto dinamico: 


.. list-table::  
   :widths: 25 25 25 25 25
   :header-rows: 1
   
   * - <elem>...</elem>
     - Esempio
     - Firmware
     - Descrizione
     - Esempio di output
   * - digit:{digit_sequence}
     - digit:1234
     - 
     - Riproduce i singoli digit (numerici, da 0 a 9) che compongono la sequenza {digit_sequence}
     - Riproduce il messaggio audio "Uno due tre quattro"
   * - number:{number}
     - number:1234
     - 
     - Riproduce il numero indicato in {number}
     - Riproduce il messaggio audio "Milleduecentotrentaquattro"
   * - alpha:{alphanumeric_sequence}
     - alpha:1a2b3c4d
     - 
     - Riproduce i singoli caratteri (alfanumerici) che compongono la stringa {alphanumeric_sequence}
     - Riproduce il messaggio audio "Uno a due b tre c quattro d"
   * - audio:{audio_file}
     - audio:custom/misc/test
     - 
     - Riproduce il file audio, presente sul KalliopePBX, identificato dal nome {audio_file} (comprensivo di percorso, come riportato all'interno del pannello "Suoni"->"File audio")
     - Riproduce il file audio custom/misc/test
   * - dtmf:{dtmf_sequence},{intertone_pause},{duration}
     - dtmf:123w*,200,350
     - 4.5.12+
     - Riproduce i toni DTMF (in accordo alla modalità specificata per il canale da cui proviene la chiamata) specificati nella sequenza {dtmf_sequence}; ciascun tono ha durata pari a {duration} millisecondi (espresso come numero intero) e intervallati da una pausa di {intertone_pause} (anch'esso espresso in millisecondi). I caratteri ammessi sono i digit DTMF validi (0-9,*#,a-d,A-D) più "w" e "W" per indicare una pausa di 500 o 1000 millisecondi. **NOTA BENE**: la pausa inter-digit viene inserita anche in caso di riproduzione dei silenzi (caratteri "w" e "W").
     - Invia all'interlocutore una sequenza di toni DTMF (ciascuno di durata 350 millisecondi) così composta: "1", pausa di 200 ms, "2", pausa di 200 ms, "3", pausa di 200 + 500 + 200 ms, "*"
   * - pause:{duration}
     - pause:450
     - 4.5.12+
     - Inserisce una pausa di durata {duration} millisecondi
     - Inserisce una pausa di 450 millisecondi
     
Regola di instradamento
........
In questo punto viene definita l’azione di inoltro da eseguire. In aggiunta alle normali azioni di uscita è prevista anche la possibilità di inoltrare la chiamata al Piano di numerazione, utilizzando come selezione il valore contenuto nella risposta.     

Interno
++++++

Nel caso in cui la richiesta sia di tipo interno il sistema verifica le corrispondenze di numero chiamante, numero chiamato e parametri sul file e restituisce il valore della colonna response che sarà utilizzato per stabilire le azioni da compiere.
Nel caso in cui ci siano più righe che riscontrino i dati di ingresso viene selezionata l’azione corrispondente alla riga con più riscontri effettuati (best match).
In questo caso non è prevista la riproduzione di un contenuto dinamico e pertanto le azioni da compiere sono costruite come segue:

- Riproduzione di un file audio statico caricato sul sistema
- Regola di instradamento
In questo punto viene definita l’azione di inoltro da eseguire. In aggiunta alle normali azioni di uscita è prevista anche la possibilità di inoltrare la chiamata al Piano di numerazione, utilizzando come selezione il valore contenuto nella risposta.
Nei casi negativi in cui i parametri non siano corretti, o la chiamata provenga da un numero non specificato nel file o non sia specificato il valore delle response, verrà sempre eseguita l’azione di gestione errori.
E’ inoltre possibile inserendo dei valori nei campi newCallerNameFull, newCallerNamePrefix, newCallerNum modificare il nome e numero chiamante che verranno mostrati sul display del telefono chiamato.
In particolare se inserisco il newCallerNameFull il nome del chiamante verrà sostituito con questo valore, se inserisco il newCallerNamePrefix questo valore viene anteposto al nome chiamante mentre se inserisco newCallerNum viene sostituito il numero chiamante.

- Gestione errori: Nel caso in cui la richiesta al server WEB restituisca un errore oppure il riscontro sul file non vada a buon fine la chiamata viene gestita come indicato in questa sessione.


Esempio instradamento dinamico interno
+++++++++

.. list-table::  
   :widths: 25 25 25 25 25 25 25 25 25 25 25
   :header-rows: 1
   
   * - callerNum
     - calledNum
     - param1
     - param2
     - param3
     - param4
     - param5
     - response
     - newCallerNameFull
     - newCallerNamePrefix
     - newCallerNum
   * - 102
     -
     - 
     - 
     - 
     - 
     - 
     - 
     - 
     - simona
     - 111
   * - 103
     -
     - 111
     - 22
     -
     -
     -
     - 100
     -
     -
     -
   * -
     -
     - 123
     - 123
     - 333
     - 123
     - 123
     - 100
     -
     -
     - 321

Dopo aver creato sul Piano di numerazione l’esatta selezione per l’instradamento dinamico, da uno degli interni si effettua la chiamata a tale numero.
Se la chiamata proviene dal numero 102, il sistema invierà la risposta 200 e verrà eseguita l’azione associata a quella response.
Se la chiamata proviene dal 103, verranno richiesti tramite un messaggio vocale, i valori dei parametri; se i parametri inseriti sono corretti il sistema invierà la risposta 100 e verrà eseguita l’azione associata a quella response.
Se la chiamata proviene da altro interno non specificato nel file, verranno richiesti i valori dei parametri e se i parametri inseriti sono corretti il sistema invierà la risposta 100 e verrà eseguita l’azione associata a quella response.
In tutti gli altri casi viene seguita l’azione definita nella gestione errori.

Menu IVR multilivello
---------

Descrizione del Servizio
+++++++
Il Risponditore Automatico Vocale Interattivo consente al chiamante, in base alla digitazione di selezione di DTMF, di essere instradato verso un determinato servizio.

Configurazione del servizio
++++++++
Al sottomenu Menu IVR vi si accede tramite il menu Applicazioni PBX.

*jpg*
È possibile creare un numero arbitrario di menu IVR che possono essere in cascata o indipendenti.

*jpg*

- La casella **Nome** può essere riempita semplicemente con il nome del Menu IVR che preferiamo.
- Nel caso in cui si vogliano creare più menu IVR in cascata si può scegliere di visualizzare l’albero IVR con il menu che configuriamo come radice dell’albero stesso, per farlo basta spuntare la casella **Visualizza un albero IVR con questo menu come radice**.
- La funzionalità **Riproduci i messaggi “in progress”** permette di eseguire il messaggio audio gratuito (innescato dal messaggio SIP 183 Session Progress) che precede l’invio del SIP message 200 OK, il quale a sua volta innesca l’inizio della chiamata e la fatturazione. Questa funzionalità è consigliata soprattutto per le aziende in possesso di un numero verde associato al risponditore automatico poiché l’azienda stessa paga il costo di chiamata ed in questo modo può risparmiare dei preziosi secondi per ogni telefonata ricevuta. La disponibilità ad accettare il messaggio Session Progress SIP 183 dipende dall’operatore a cui è agganciata la centrale e normalmente ha una durata massima di 59 secondi.
- La voce **File audio** permette di selezionare la traccia preregistrata contenente le opzioni che il cliente può scegliere tramite il tastierino numerico.
- in **Ripetizioni** possiamo scegliere il numero di volte in cui il file audio verrà eseguito, non è possibile scegliere 0 perché vorrebbe dire non eseguire il file audio di descrizione del menu.
- **Timeout (sec.)** indica l’attesa di selezione al termine del messaggio audio. Il sistema resta quindi in attesa per il numero di secondi indicati prima di effettuare una seconda ripetizione (se esiste) oppure scatenare l’azione predefinita (campo sottostante).

Azione predefinita
+++++++
L’azione predefinita è preimpostata come Inoltra a: riaggancia, ma esiste un’ampia scelta nel menu a tendina. Questa azione è utile all’utente che per qualche motivo non ha selezionato alcuna voce, di conseguenza possiamo scegliere se far riprodurre un file audio in cui si fa presente la mancata selezione del menu e si può inoltrare ad una delle voci presenti nella lista in cascata.

Selezioni
++++++++
Nella voce Selezioni si può associare al numero che verrà selezionato dall’utente tramite tastierino numerico, l’inoltro ad una specifica voce presente nel menu a tendina. Esempi:

- **Riaggancia**: la chiamata, dopo le ripetizioni dell’audio, viene terminata.
- **Numero esterno**: la chiamata viene indirizzata ad un numero esterno che può essere un cellulare o un numero comunque non appartenente all’interno del centralino.

Si può scegliere la classe d’uscita/CLID che serve per identificare il numero di telefono dell’utente chiamante.

- **Interno**: la chiamata viene trasferita ad un numero interno che si può scegliere tramite la casella a destra.
- **Gruppo di chiamata**: permette di distribuire la chiamata a più di interno, quindi consente di ricercare un interno disponibile per rispondere ad una chiamata in ingresso. Vedi la pagina Gruppi di chiamata.
- **Gruppo di chiamata (salta controllo orario)**: il controllo orario sul gruppo di chiamata può essere semplicemente ignorato tramite questa opzione.
- **Coda**: le chiamate in arrivo non vanno ad impegnare direttamente una o più destinazioni, ma vengono inserite in una coda di attesa. La chiamata viene tolta dalla coda quando ci sono operatori disponibili per servire il cliente. Vedi la pagina Code di attesa.
- **Coda (salta controllo orario)**: il controllo orario sulle code può essere semplicemente ignorato tramite questa opzione.
- **Controllo orario**: meccanismo che serve per gestire l’instradamento delle chiamate su base temporale e/o manuale. La procedura su base temporale consiste nel definire delle fasce orarie che vengono riscontrate in ordine: se la data e l’ora corrente cadono all’interno di una di queste, viene eseguita l’azione di inoltro corrispondente, altrimenti viene eseguita un’azione generale che vale per gli altri periodi della giornata. La modalità manuale fa sì che si abbiano degli interruttori (acceso o spento) comandabili tramite codice digitabile da telefono e/o tasto BLF. Vedi la pagina Controllo orario.
- **Menu IVR**: permette di selezionare un Menu IVR precedentemente creato per collegarlo a quello attuale e creare così un menu a cascata.
- **Casella vocale**: consente ad un utente di ricevere messaggi vocali anche quando non è in grado di rispondere ad una chiamata (per esempio se occupato o non disponibile). Vedi la pagina Casella Vocale.
- **Servizio audio conferenza**: è possibile accedere ad un servizio di audio conferenza in cui possono essere collegate persone interne o esterne all’azienda. Si può scegliere se richiedere il numero della stanza (PIN) oppure indirizzare direttamente verso la stanza desiderata.
- **Instradamento dinamico**: permette di effettuare la gestione della chiamata sia tramite invocazione di un web service esterno (come l'applicazione originaria) che riscontrando i parametri su un file XLS/CSV caricato sul PBX. Vedi la pagina Instradamento Dinamico.
- **Istanza FAX**: permette di selezionare un’istanza FAX che corrisponde concettualmente ad un fax fisico al quale possono accedere uno o più utenti. Vedi la pagina Fax.
- **Piano di numerazione – selezione personalizzata** permette di inserire una selezione che è già stata configurata in precedenza nel piano di numerazione.
- **Piano di numerazione – chiedi selezione** permette di far scegliere al chiamante quale interno raggiungere, in questo modo verrà riprodotto un file audio in cui si richiederà al chiamante di digitare il numero di selezione desiderato.
- **Permetti digitazione del numero di selezione**: permette al chiamante di digitare un numero del piano di numerazione qualora lo sapesse già, senza dover ascoltare le varie possibilità offerte dal menu. La digitazione del numero di selezione in questo caso prevederà più cifre e di conseguenza il servizio IVR rimarrà in attesa del completamento della composizione per evitare di indirizzare il cliente alla selezione sbagliata.

Sottomenu IVR (in cascata)
+++++++
Per creare un menu IVR in cascata bisogna necessariamente creare un altro menu procedendo nello stesso modo. Prima di farlo, si salva il menu IVR precedentemente creato tramite il pulsante Salva in basso, in questo modo ci si troverà nella schermata principale. Per aggiungere un altro menu, premere su Aggiungi menu IVR.


Dopo aver configurato e salvato il secondo menu si possono trovare entrambi nella schermata principale.


Per procedere a creare un menu in cascata, modificando il Menu principale si seleziona l’opzione inoltra a: Menu IVR e si sceglie nell’ultima casella a destra, il menu secondario.

Tornando nella pagina principale si può vedere graficamente il collegamento tra i due menu selezionando la Vista ad albero.


Lucchetto elettronico
-------

Descrizione del servizio
+++++++

Il servizio Lucchetto Elettronico consente di bloccare le chiamate effettuate da un dispositivo verso specifiche numerazioni esterne. Le chiamate verso altri interni (anche remoti) o servizi del PBX sono sempre accessibili anche da interni con lucchetto bloccato.

Quando il lucchetto è bloccato possono essere effettuate solo le chiamate abilitate nella classe di instradamento definita “ristretta” mentre nello stato di sblocco l’interno può effettuare tutte le chiamate previste dalla classe di instradamento “standard”.

Lo sblocco del lucchetto può essere effettuato con diverse modalità e la durata dello sblocco dipende dalla politica prescelta.

La configurazione del servizio di Lucchetto Elettronico viene effettuata per interno quindi tutti gli account (dispositivi) associati all'utente condividono lo stato del Lucchetto Elettronico.

Le modalità di sblocco previste sono le seguenti:

- **Aperto**: lo stato del lucchetto è sempre sbloccato e quindi viene sempre applicata la classe di instradamento standard
- **Codice**: lo sblocco viene effettuato utilizzando il codice sblocco lucchetto elettronico definito nel Piano di Numerazione (default 850). Il blocco viene effettuato utilizzando il codice blocco lucchetto elettronico definito nel Piano di Numerazione (default 851)
- **Password**: lo sblocco viene effettuato utilizzando il codice sblocco lucchetto elettronico definito nel Piano di Numerazione (default 850) e il PIN dell’interno associato al dispositivo da cui si sta effettuando la chiamata. Il blocco viene effettuato utilizzando il codice blocco lucchetto elettronico definito nel Piano di Numerazione (default 851) e inserendo dopo il prompt vocale il PIN dell’interno associato al dispositivo da cui si sta effettuando la chiamata.

Le politiche di sblocco previste sono le seguenti:

- **Per chiamata** – Il lucchetto deve essere sbloccato prima di effettuare ogni chiamata
- **Blocca automaticamente dopo il numero di minuti sottoindicato** – Il lucchetto viene bloccato automaticamente allo scadere dell’intervallo indicato
- **Sbloccato finché l’utente lo blocca nuovamente** – Il lucchetto una volta sbloccato deve essere bloccato esplicitamente dall'utente

Operativamente l’utente che deve effettuare una chiamata su un dispositivo associato ad un interno bloccato effettua le seguenti operazioni:

1. Chiama il servizio di sblocco lucchetto elettronico (default 850)
2. Nel caso in cui la modalità sia password il PBX richiede l’inserimento del PIN dell’interno tramite prompt vocale “Password”
3. L’utente digita il proprio PIN seguito dal tasto#
4. Il PBX conferma lo sblocco con il messaggio audio “Salvato”
5. In caso di errore il PBX risponde con il messaggio audio “Login Errato” e riaggancia

Per bloccare nuovamente l’interno (nel caso la politica non preveda una chiusura automatica) l’utente effettua le seguenti operazioni:

1. Chiama il servizio di blocco lucchetto elettronico (default 851)
2. Il PBX conferma lo sblocco con il messaggio audio “Grazie”

Configurazione del servizio
++++++

Per la configurazione del lucchetto elettronico è necessario definire preventivamente le classi di instradamento in uscita che devono essere applicate in condizioni di lucchetto bloccato e sbloccato.

Successivamente nel pannello Interni devono essere configurati i seguenti parametri :

- Classe di instradamento in uscita standard
- Classe di instradamento in uscita ristretta
- Modalità di sblocco
- Politica di sblocco
- Durata dello sblocco (sec)


Esempi
++++

- Chiamate internazionali solo con PIN (da abilitare per chiamata): in questo caso viene definita una classe ristretta che consente di effettuare tutte le chiamate tranne le internazionali ed una classe standard che consente anche le chiamate con prefisso internazionale. La modalità di sblocco è password e la politica per chiamata.
- Chiamate da telefoni non presidiati solo con codice (sblocco 30 min): in questo caso viene definita una classe ristretta che consente di effettuare solo chiamate di emergenza ed una classe standard che consente di effettuare tutte le chiamate. La modalità di sblocco è codice e la politica blocca automaticamente dopo 30 sec.


Prenotazione su occupato (CCBS)
---------

Descrizione funzionale
++++++++++
Questo servizio consente di prenotare la richiamata ad un interno che l'utente ha provato a contattare ma è risultato occupato.
Il servizio funziona esclusivamente quando sia chiamante che chiamato sono un interno.

Operativamente l'utente che vuole prenotare la richiamata digita il codice di prenotazione richiamata su occupato (default disabilitato) entro 20 secondi dal termine della chiamata verso l'utente occupato.
Il KPBX conferma la prenotazione riproducendo il prompt vocale "Salvato".
Quando l'utente occupato si libera il KalliopePBX chiama l'utente che ha fatto la prenotazione (sul display del telefono chiamante viene visualizzata l'etichetta c2c seguita dall'interno su ci è stata prenita la chiamata) e non appena questo risponde fa partire la chiamata verso l'altro utente.

Nel caso in cui l'utente voglia annullare la prenotazione digita il codice di annullamento prenotazione richiamata su occupato (default disabilitato).
Anche in questo caso il KPBX conferma l'annullamento della prenotazione riproducendo il prompt vocale "Salvato".

La prenotazione di richiamata ha una validità di 1 ora.
Nel caso in cui venga effettuata una nuova prenotazione prima della scadenza della precedente, la vecchia viene automaticamente annullata (è possibile mantenere una sola prenotazione attiva per interno).


Configurazione
++++++++
Il servizio può essere abilitato / disabilitato nel pannello PBX -> Piano di numerazione
Il codice del servizio può essere modificato nel pannello PBX -> Piano di numerazione

Interoperabilità
++++++++
Quando si utilizza il servizio CCBS può essere utile avere a disposizione un tasto che consenta di effettuare la prenotazione e uno che consenta di annullarla.
Questa operazione è normalmente effettuata configurando due tasti funzione di tipo Speed Dial con valore pari rispettivamente al codice di prenotazione e annullamento prenotazione.

Servizio Direttore-Segretaria
++++++++++

Descrizione del servizio
++++++++++
Questo servizio consente ad una o più utenze (segretarie) di intercettare le chiamate dirette ad un altro interno (direttore). Solamente le segretarie (ed opzionalmente i direttori configurati in altri gruppi) potranno contattare direttamente il direttore sul proprio interno.

Le segretarie avranno quindi il compito di rispondere alle chiamate dirette all’interno del direttore, verificare la disponibilità del direttore ed eventualmente trasferire la chiamata.

Il servizio può essere abilitato / disabilitato sia a livello di gruppo (su tutte le segretarie) che per la specifica segretaria. Nella pratica di solito il direttore quando attiva il servizio lo imposta per tutte le segretarie, mentre la singola segretaria può decidere di entrare o uscire dal servizio. Anche se il direttore non ha attivato il servizio, la segretaria può attivarlo per il proprio interno.

Operativamente l’attivazione/disattivazione del servizio Direttore-Segretaria può essere effettuata mediante digitazione di codici da telefono. Il servizio viene attivato a livello di gruppo digitando il codice di attivazione (default *521) seguito dall'interno del direttore. Il KalliopePBX conferma l’attivazione del servizio riproducendo il file audio “Salvato”. L’attivazione per la specifica segretaria viene invece effettuata aggiungendo al codice globale * seguito dall'interno della segretaria. Anche in questo caso il KalliopePBX conferma l’attivazione riproducendo il file audio “Salvato”.

Analogamente la disattivazione a livello di gruppo avviene digitando il codice relativo (default *520) seguito dall'interno del direttore. Il KalliopePBX conferma la disattivazione riproducendo il file audio “Salvato”. La disattivazione per la specifica segretaria viene invece effettuata aggiungendo al codice globale * seguito dall'interno della segretaria. Anche in questo caso il KalliopePBX conferma la disattivazione riproducendo il file audio “Salvato”.

Esiste anche un codice di commutazione dello stato del servizio (default *52*). Analogamente al caso di attivazione / disattivazione il codice deve essere seguito dall'interno del direttore per la commutazione dello stato del servizio per tutto il gruppo. La commutazione dello stato del servizio per la specifica segretaria viene invece effettuata aggiungendo al codice globale * seguito dall'interno della segretaria. In entrambi i casi il KalliopePBX conferma la commutazione riproducendo il file audio “Salvato”.

Questi codici possono essere utilizzati esclusivamente da un dispositivo associato ad un interno che appartiene al Gruppo Direttore-Segretaria.

Configurazione del servizio
++++++++++
L'abilitazione globale del servizio e la scelta del codice di servizio associato viene effettuata nel pannello PBX-> Piano di numerazione ed eventualmente modificare il codice da utilizzare.

La configurazione dei gruppi Direttori-Segretaria viene effettuata nel pannello Gruppi Direttore-Segretaria. I parametri da configurare per i gruppi sono i seguenti:

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Abilitato
     - Consente di disabilitare un gruppo direttore/segretaria senza perderne la configurazione	
     - Si / No
   * - Nome
     - Identificativo del gruppo direttore / segretaria
     - Alfa-numerico
   * - Permetti chiamate da altri direttori
     - Se questa opzione è abilitata gli interni dichiarati come direttori in altri gruppi direttore-segretaria possono contattare direttamente il direttore evitando il filtro delle segretarie
     - Si / No
   * - Seleziona il direttore
     - Interno le cui chiamate verranno deviate sulle segretarie
     - Interno
   * - Aggiungi segretaria
     - Consente di definire la lista degli interni su cui verranno deviate le chiamate del direttore.
     - Interno
     
Trabocchi
++++++++
Qui sono definite le azioni di failover nel caso in cui per le chiamate deviate sulle segretarie si verifichi una delle cause di trabocco. Per questo servizio è prevista l’azione di failover supplementare “Inoltra al direttore”.

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Interno
     - Azione di trabocco su chiamate provenienti da un interno (anche remoto)
     - 
   * - Esterno
     - Azione di trabocco sulle chiamate provenienti dall'esterno
     - 
   * - Trasferimento
     - Azione di trabocco sui trasferimenti di chiamata
     - 
   * - Timeout (sec.)
     - Tempo alla scadenza del quale viene eseguita l’azione di trabocco configurata in caso di nessuna risposta (nessuna segretaria risponde entro il timeout)
     - Numerico
   * - Nessuna risposta
     - La chiamata è considerata senza risposta alla scadenza del timeout
     - Inoltra al direttore / Riaggancia / Selezione personalizzata / Chiedi selezione / Numero esterno / Interno / Gruppo / Coda / Controllo orario / IVR / Casella vocale / Stanza MeetMe
   * - Occupato
     - Tutti gli interni delle segretarie risultano occupati. L’interno è considerato occupato se è stato raggiunto il Busy Level impostato per l’interno oppure se il terminale invia il SIP Response 486 Busy Here
     - Inoltra al direttore / Riaggancia / Selezione personalizzata / Chiedi selezione / Numero esterno / Interno / Gruppo / Coda / Controllo orario / IVR / Casella vocale / Stanza MeetMe
   * - Non Disponibile
     - Tutti gli interni delle segretarie risultano non disponibili. L’interno è considerato non disponibile se il terminale non è registrato o non è raggiungibile a livello IP oppure se il terminale invia il SIP Response 480 Temporarily Unavailable
     - Inoltra al direttore / Riaggancia / Selezione personalizzata / Chiedi selezione / Numero esterno / Interno / Gruppo / Coda / Controllo orario / IVR / Casella vocale / Stanza MeetMe


Interoperabilità con dispositivi di terze parti
++++++++++++

Quando l’attivazione / disattivazione del servizio viene effettuata da telefono può essere molto utile avere a disposizione un tasto (con campo lampade) che consenta di verificare lo stato del servizio.

Per quanto riguarda il monitoraggio, il KalliopePBX invia dei messaggi SIP NOTIFY per comunicare i cambi di stato del servizio. Il telefono dovrà inviare una SIP SUBSCRIBE per richiedere l’invio delle informazioni di stato.

Questa operazione è normalmente effettuata configurando un tasto funzione di tipo BLF.

L’oggetto da monitorare è *bs<interno_direttore>* se vogliamo monitorare lo stato a livello di gruppo e **bs<interno_direttore>*<interno_segretaria>** per monitorare lo stato del servizio per la segretaria sullo specifico gruppo. Lo stato a livello di gruppo risulta attivo nel caso in cui il servizio sia attivo per almeno una segretaria.

Oltre a monitorare lo stato del servizio è possibile effettuarne la commutazione cliccando sul tasto funzione corrispondente.

Tipicamente il tasto con il controllo a livello di gruppo viene abilitato sul telefono del direttore mentre i tasti con il controllo specifico per interno sul telefono della segretaria corrispondente.

In ogni caso i tasti sono configurabili su tutti i membri del gruppo per soddisfare esigenze specifiche (ad es. il direttore potrebbe richiedere di voler impostare lo stato del servizio delle specifiche segretarie oppure lo stato a livello di gruppo può essere impostato da una segretaria).

Esempi di configurazione
++++++++

**Su SNOM**

- Operando tramite la web gui di configurazione configurare Function keys con

.. code-block:: console

   Account: selezionare dalla tendina l’account che stiamo utilizzando (se c’è un solo account configurato sul telefono è il primo della lista)
   Type: BLF
   value: bs<interno_direttore> / bs<interno_direttore>*<interno_segretaria>
   
- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">blf sip:bs<interno_direttore>@%%KPBX_IP_ADDRESS%%;user=phone</fkey>

oppure

.. code-block:: console

   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">blf sip:bs<interno_direttore>*<interno_segretaria>@%%KPBX_IP_ADDRESS%%;user=phone</fkey>
   
Dove %%id%% è l’identificativo del tasto da configurare E %%line_id%% è l’identificativo dell’account associato (il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console

   <fkey idx="0" context="1" label="DirSeg 109" perm="">blf sip:bs109*105@192.168.23.112</fkey>
   
**Su YEALINK**

- Operando tramite la web gui di configurazione configurare DSS Key con:

.. code-block:: console
   
   Type BLF
   Value: bs<interno_direttore> / bs<interno_direttore>*<interno_segretaria>
   Line: La linea associata all’account che stiamo utilizzando (Line 1 se sul telefono è presente un solo account)

- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   memorykey.%%id%%.line=%%line_id%%>
   memorykey.%%id%%.value=bs<interno_direttore> / bs<interno_direttore>*<interno_segretaria>
   memorykey.%%id%%.type=16
   
Dove %%id%% è l’identificativo del tasto da configurare

e %%line_id%% è l’identificativo dell’account associato il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console

   memorykey.1.line = 1
   memorykey.1.value = bs109*105
   memorykey.1.type = 16
   memorykey.1.pickup_value = %NULL%


Servizio paging
-------

.. note::
   Introdotto in Release: 4.3.1
   
Descrizione del servizio
+++++++++

Il servizio Paging permette di inviare un messaggio audio dal vivo o preregistrato a più destinazioni contemporaneamente, eventualmente specificando ai terminali di destinazione di rispondere in modo automatico. Questo servizio è comunemente utilizzato per effettuare annunci informativi o di emergenza.

Il servizio Paging disponibile in KalliopePBX permette di definire un numero arbitrario di "Gruppi di paging". Ciascuno di essi è indipendente dagli altri, ed è completamente configurabile in termini di autorizzazioni, scelta delle destinazioni, della modalità operativa e dei messaggi da riprodurre.

Operativamente, un interno effettua una chiamata ad una selezione costituita da un prefisso associato al servizio Paging (definito insieme all'abilitazione del servizio stesso nel Piano di Numerazione, impostato per default a *53) seguito dal numero specifico del gruppo di Paging (definito nel pannello di configurazione del gruppo stesso). In caso sia necessaria autenticazione, il PBX riproduce un prompt vocale ("Password") all'utente, che deve inserire un PIN numerico, seguito dal tasto #. In caso di autenticazione avvenuta con successo (in base al PIN specificato nella configurazione del gruppo per quell'interno chiamante) viene avviato il gruppo di Paging, in accordo alla modalità configurata, come dettagliato nella sezione seguente.

Configurazione del servizio
++++++++
L'aggiunta o la modifica di un Gruppo di Paging viene effettuata dal pannello omonimo, raggiungibile dal menu "Applicazioni PBX".

Nella seguente tabella sono descritti i parametri di configurazione di ciascun gruppo sono:

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Nome
     - Identificativo assegnato al gruppo di Paging
     - Alfanumerico
   * - Numero
     - Selezione del servizio di Paging
     - Numerico
   * - Identificativo chiamante
     - Display Name per le chiamate verso i terminali di destinazione
     - Alfanumerico
   * - Modalità
     - Modalità di funzionamento del gruppo di Paging
     - Live/Unattended
   * - File audio
     - File audio contenente un messaggio preregistrato che viene riprodotto ai terminali di destinazione del gruppo. Viene utilizzato in modo differente nel caso di modalità Live o Unattended
     - 
   * - Numero di ripetizioni
     - Numero di volte che il messaggio preregistrato deve essere riprodotto prima che il PBX termini automaticamente la chiamata(configurabile solo nella modalità "Unattended")
     - Numerico(0 indica che il messaggio deve essere riprodotto in ciclo continuo)
   * - Metodo di risposta automatica
     - Header da aggiungere alle chiamate effettuate verso i terminali di destinazione al fine di specificare la richiesta di risposta automatica
     - Configurazione manuale/Call-Info/Header Alert-Info
     
**Account**     

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore
   * - Interno
     - Terminali di destinazione del Paging	
     - 
   * - Account
     - Account SIP associato all'interno
     - 
     
**Controllo di accesso**     

.. list-table::  
   :widths: 25 25 25
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore 
   * - Interno
     - Interno chiamante
     - "Qualsiasi interno"/Interno
   * - Tipo di PIN
     - Modalità di autenticazione richiesta
     - Nessuno/Personalizzato/ PIN dei servizi proprio di ciascun interno abilitato.
   * - Valore del Pin
     - 
     - Alfanumerico
  
