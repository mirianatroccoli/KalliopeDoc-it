Monitoring
======

Descrizione del servizio
-----------
Monitorare le infrastrutture IT della propria azienda è essenziale per assicurare un corretto funzionamento delle stesse e per rilevare eventuali malfunzionamenti. Tramite la verifica costante dei problemi che vengono rilevati, l’apertura di ticket all’occorrenza e il conseguente invio di notifiche alle aree ed ai referenti interessati, è possibile avere un controllo totale dei processi. Tutti i problemi che si verificano sono memorizzati e visualizzati in un’unica sezione con un relativo livello di gravità. Questo livello può essere completamente personalizzato tramite l’apposita sezione, indicando a quale tipo di problema, o gruppo di problemi, dovrà essere associata una determinata gravità. Il modulo di Monitoraggio offre quindi uno strumento per gestire velocemente e al meglio tutti i problemi rilevati sugli asset presenti nella propria azienda, permettendo di risparmiare tempo e denaro.

Per raggiungerlo, è necessario premere su “Monitoring” nel menu a sinistra.

Struttura e configurazione
------------
Il modulo si suddivide in diverse sezioni, ma le principali – dove vengono riportate le informazioni fondamentali del monitoraggio – si possono trovare nei moduli Host e Problems. Di fondamentale importanza è anche la sezione delle Classi Dinamiche, la cui struttura e configurazione segue le due sezioni principali.

HOST
++++++++++
Nella sezione Supporto > Asset, creando un asset e spuntandolo come "da monitorare", verrà creato automaticamente un host con le necessarie informazioni per essere monitorato.

Nell'elenco degli host (raggiungibile tramite Monitoring > Host) è possibile visualizzare per ogni host:

- Nome dell'host
- Id dell’host
- Categoria
- Account
- Final customer
- Utente referente
- Last problem: data di rilevamento dell'ultimo problema
Elenco host.png

Grazie alla configurazione delle classi nella sezione "classe dinamica" è possibile definire degli orari per i quali il controllo dell'asset deve essere attivo: se alcuni apparati in determinati momenti vengono spenti, il monitoraggio non segnala gli errori.

Dettaglio host
..............
Selezionando un host presente nell'elenco (cliccando sul nome) è possibile entrare nella maschera di dettaglio host, dove sarà possibile visualizzare i dettagli di monitoraggio dell'apparato e i dati dell'ASSET. Per modificare le informazioni di un host, bisogna modificare quelle del relativo asset collegato. All'interno della maschera di dettaglio è presente la prima sezione suddivisa in due tab. Nella prima, con il nome dell'host, sono riportate alcune delle informazioni essenziali di quest'ultimo. Nel secondo, chiamato "Host Inventory", sono riportate tutte le informazioni dettagliate sull'host.

Dettaglio host.png

Sotto questi due tab è visibile un elenco di tutti i problems rilevati dal sistema e per ognuno sarà possibile aprire dei ticket tramite apposito tasto (new ticket) che, se indicato, porterà all'invio di specifiche notifiche di apertura ticket ai vari referenti. La mail di notifica è strutturata con un template personalizzabile che riporterà tutti i dati dell'asset necessari all'individuazione univoca dell'apparato per una celere risoluzione del guasto:

- Host id: codice indentificativo dell'host
- Eventid
- Lastchange: data dell'utima variazione del problem dell'host
- Name: nome del problem
- Classe: indica la gravità del problema (inserita tramite classi dinamiche)
Oltre alla possibilità di creare ticket, è anche possibile eseguire una chiusura forzata del problema, in maniera che non risulti più come tale e non sia visibile nell'elenco dei problems. Eventuali modifiche al ticket saranno notificate ai vari referenti. La chiusura forzata del problema evita che questo compaia ulteriormente sulla piattaforma.

Elenco problems1.jpg

Nella sezione Graph, è possibile selezionare il tipo di grafico desiderato e il periodo da prendere in considerazione per visualizzare il grafico temporale dell'utilizzo delle risorse monitorate per quello specifico host (es. andamento download o upload per specifico router).

Grafico host.png


Filtri Host
..........
È possibile filtrare i dati presenti nell'elenco tramite il pulsante “Ricerca” in alto a destra ed inserire:

- Account
- Final Customer
- Host id: codice identificativo dell'host
- Host (nome)
- Categoria dell'host da monitorare
- Classe: identifica la priorità del malfunzionamento rilevato
- Problem data from: data di inzizio per la ricerca di problems
- Problem data to: data finale dell'intervallo di tempo in cui viene effettuata la ricerca dei problems
- Solo host con problemi non risolti (si o no)
- Host con problemi senza ticket (si o no)
- Gruppo
- Tamplate
- Raggruppamento (CAP, Comune, Provincia, Identificativo)

Problems
++++++++++++
In questa sezione (raggiungibile tramite Monitoring > Problems) vengono esaminati tutti i problemi che sono stati rilevati, con le relative gravità personalizzabili nell'apposito modulo. Può succedere che alcuni problemi si risolvano autonomamente, in questo caso nella tabella sarà presente una spunta, altrimenti – in caso negativo – una croce.

I problems presenti nell’elenco sono classificati per classi che identificano la priorità del malfunzionamento rilevato.

Le informazioni sui problems riportati nella tabella comprendono:

- host name: il nome dell'host
- account
- final customer
- firstchange e lastchange: data della prima e ultima variazione rilevata
- resolution time: tempo di risoluzione del problema
- name: nome del problem
- classe: valutazione della severity del problem
- hide: indica se il problema è stato risolto (si) o se è ancora in attesa (vuoto)
- data chiusura forzata (se avvenuta)
- ticket.numerazione: numero del ticket collegato al problem
- ticket.titolo: titolo del ticket collegato al problem
- ticket.stato: stato del ticket collegato al problem
- intermittente: se il problems è intermittente o meno
Elenco problems 2.jpg

Cliccando sul nome dell'host si entra nella sezione "dettaglio host" (vedi sopra).

Filtri Problems
...........
Cliccando sulla lente d'ingrandimento "ricerca" sarà possibile filtrare i problemi per:

- Account
- Final customer
- Host id: codice identificativo host
- Host name: nome associato all'host
- Ticket: possibilità di ricerca tramite il titolo del ticket o la descrizione
- Problem descrizione
- Categoria
- Classe: valutazione in priorità del malfunzionamento
- Problem data from: data di inzizio per la ricerca di problems
- Problem data to: data finale dell'intervallo di tempo in cui viene effettuata la ricerca dei problems
- Solo problemi non risolti (visualizzazione si o no)
- Solo problemi risolti ma con ticket aperti (visualizzazione si o no)
- Solo problemi senza classe (visualizzazione si o no)
- Problemi risolti con tempo di risoluzione (indicando il tempo)
- Gruppo
- Template

Classi dinamiche
+++++++++
È possibile associare ogni problem di ogni host ad una specifica classe. Le classi sono necessarie per assegnare il livello di severity ad ogni problem, in modo da gestire le segnalazioni con le corrette priorità.

La classe è identificata da un numero e di default da -1 a 9, dove -1 indica i problem fuori orario e 0 viene assegnato ai problems che non si vogliono monitorare e per i quali il sistema (sebbene li registri nel database) non segnala malfunzionamenti. Nella personalizzazione della sezione, è possibile configurare i destinatari delle notifiche via mail, specificando Oggetto e corpo della e-mail.

Classi dinamiche.png

La piattaforma assegna una classe ad un problem in base a specifiche logiche, tenendo conto che nella macchina di monitoraggio le severity registrate vanno da un minimo di 0 e un massimo di 5. È comunque possibile configurare nuove classi associandole a dei problems, tramite il tasto "+ Nuova classe".

Classi dinamiche 2.png

La classificazione si basa su filtri attivati che lavorano sul nome dell'host e sulla descrizione del messaggio di errore. È possibile utilizzare il placeholder "_REPLACE_" per perfezionare la ricerca degli 'host' e dei 'regex' per la successiva assegnazione della classe al problems. Esempi:

- Inserendo ESO-CPI-ROU-001 nel campo 'host' il sistema matcha solo gli host con questo nome
- Inserendo ESO-CPI-ROU_REPLACE_ nel campo 'host' il sistema matcha tutti gli host che iniziano con ESO-CPI-ROU
- Inserendo _REPLACE_ROU_REPLACE_ nel campo 'host' il sistema matcha tutti gli host che contengono ROU
La stessa logica può essere applicata al campo "regex", ossia la descrizione dell'errore che genera il problem. Ogni classe dinamica che viene creata prevede una sezione di dettaglio nella quale possono essere aggiunte delle specifiche che serviranno a precisare i casi per cui un problema avrà una classe specifica al posto di un'altra.

- host collegati
- orari
- ticket
- problem intermittenti
Premendo sul primo pulsante, "host collegati", verrà aperta una maschera di configurazione con i campi "host" e "problem" con un "+" sulla destra. Questo è necessariob per aggiungere dei vincoli sulla classificazione principale, ovvero una determinata classe verrà assegnata solo se è presente un problema negli host collegatti, tra quelli inseriti. Potrà essere inserito solamente il nome di un host e la descrizione dell'errore, oppure entrambi collegati.

Dettaglio classi.png

Il secondo pulsante, "orari”, mostra una griglia divisa per giorni e fasce orarie dove sarà possibile inserire degli orari specifici in cui un host dovrà essere monitorato. Per indicare questo periodo di tempo, basta selezionare il flag che interseca giorno e fascia oraria interessata. Normalmente i giorni festivi non vengono contati, ma è possibile cambiare questa opzione selezionando il flag "includi anche i giorni festivi" in alto a sinistra. Invece, per selezionare tutti i giorni, spuntare il flag "seleziona tutto".

Dettaglio date.png

Cliccando su "ticket", la maschera visualizzata permette programmare l'apertura di un ticket per un problem. Il problem per cui verrà aperto il ticket è quello indicato nel box principale per cui si sta creando il dettaglio. In questa maschera dovranno essere indicati alcuni parametri del ticket:

- tipologia
- priorità
- titolo
- descrizione
Sulla sinistra sono presenti 3 flags, "open ticket", "notifica azienda" e “external”, che serviranno rispettivamente per: aprire il ticket al rilevamento del problem, notificare l'azienda per cui viene aperto il ticket e indicare il ticket aperto come ticket in external, ovvero riferito ai fornitori.

Dettaglio ticket.png

L'ultimo pulsante, "problem intermittenti", permette di aprire ticket anche per problems intermittenti. Essi sono dei problemi rilevati che si risolvono in autonomia in un certo intervallo di tempo, alcuni di questi possono però provocare dei disservizi. Per gestire questa tipologia di problems, si possono creare ticket specifici. Es. Se sappiamo che un determinato problema viene creato ogni intervallo di tempo (minuti, ore), per evitare che un ticket venga creato tot volte, è conveniente compilare la seguente sezione.

Dopo aver cliccato sul pulsante verrà mostrata una maschera in cui andranno inseriti:

- tipologia del ticket
- priorità
- se notificare l'azienda dell'apertura del ticket
- se si tratta di un ticket per fornitori (external)
- titolo del ticket
- descrizione
L'intervallo di tempo e i criteri per cui un problem è definito intermittente, sono personalizzabili tramite 3 celle:

- n. problems: numero di problems verificatisi in un certo intervallo di tempo
- intervallo di tempo: numero che rappresenta un intervallo per l’esecuzione del check per l'intermittenza di un determinato problema
- intervallo di tempo in: unità di misura usata per indicare l'intervallo di tempo (minuti, ore, giorni).
Dettaglio problems intermittenti.png

Template --> possibilità di caricare o aggiornare dei template tramite file.

Template repository --> indicare / creare come se fosse un repository, si salvano i template per poi essere indicati all’interno della sezione template.

Report
++++++++
Nella sezione “Monitoring” sono messi a disposizione quattro principali report che permettono di capire intuitivamente qual è lo stato dei vari problemi rilevati. I report sono divisi per categoria e per sede, è inoltre presente un report riservato all'analisi dettagliata dei dati. I quattro report sono utili per avere una panoramica al livello generalizzato di quella che è la situazione dei vari problemi che vengono rilevati. I quattro report si dividono in:

- Report: la seguente sezione è una sezione generale nel quale sono visualizzabili due grafici, uno a torta ed un istogramma, che riportano il rapporto tra errori risolti (DONE) e quelli che risultano ancora aperti (ERRORS)
Report 1.png

- Report Analisi: in questa sezione si può trovare una dashboard dove vengono riportati il numero di problems con la loro situazione (non risolti, ancora aperti) e il tempo medio per i problems non risolti.
Report analisi.png

Sono presenti anche grafici che rappresentano l'andamento dei problems:

- il primo rappresenta i problems aperti suddivisi per data e per stato (risolti/non risolti)
Report analisi 1.png

- il secondo e terzo grafico rappresentano rispettivamente i problems aperti suddivisi per gruppo e ripartiti per data, e i problems non risolti, anche questi suddivisi per gruppi e ripartiti per data
Report analisi 3.png

- il quarto e quinto grafico rappresentano i problems aperti o non risolti, sempre per data, ma suddivisi per classe
Report analisi 4.png

- Il sesto grafico consiste nella rappresentazione totale dei problems per data, con la possibilità di visualizzare:
  - problems aperti
  - problems risolti
  - media di problems aperti e chiusi
  - trend dei problems aperti
  - trend dei problems risolti
  - trend dei problems aperti e risolti

Report analisi 5.png

- Gli ultimi grafici sono quattro grafici a torta che rappresentano:
  - I problems totali suddivisi per gruppo
  - I problems non ancora risolti suddivisi per gruppo
  - I problems totali suddivisi per classe
  - I problems non ancora risolti suddivisi per classe
Come in tutti i grafici presenti sulla piattaforma, è possibile togliere o aggiungere alla visualizzazione alcuni dati tramite legenda e visualizzare le quantità scorrendo con il mouse sul grafico.

Report analisi 6.png


Report data – ora per categoria
+++++++++
In questa sezione si può osservare l'andamento dei problems in un arco di tempo indicato tramite i filtri (attivabili grazie al tasto "ricerca") in date suddivise a loro volta per fasce orarie. Sempre tramite i filtri, si può scegliere quale categoria di problems includere nel grafico. Sono visualizzati gli stati (problems aperti e risolti) e le categorie, descritti anche nella legenda.

Report-categoria.png

Report data – ora per sede
+++++++++
Come nella sezione precedente, anche in questa è possibile osservare l'andamento dei problems con una ripartizione giornaliera e oraria (dove ogni giorno ha una sua ripartizione oraria), ma con l'unica differenza che ad essere visualizzate non sono le categorie, ma le sedi. Sempre tramite filtri (tasto "ricerca") è possibile includere la sede di cui si vogliono visualizzare i dati, visibili anche nella legenda.
