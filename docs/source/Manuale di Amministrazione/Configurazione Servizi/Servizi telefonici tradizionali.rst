Servizi telefonici tradizionali
=====

Call Hold and Music on Hold
----------

Per mettere la chiamata corrente in attesa, si opera sul corrispondente tasto funzione presente sul terminale telefonico; in base al modello specifico il tasto può essere un tasto fisico dedicato (normalmente indicato con “Hold”) oppure essere uno dei tasti dinamici.


Call Pickup (esplicito e con invito)
-------

Descrizione del servizio
+++++
Questo servizio consente ad un utente del centralino di prelevare la chiamata diretta ad un altro interno.
Nel caso in cui stia squillando un determinato interno, ma l’utente chiamato non può o non vuole rispondere alla chiamata, un altro utente può, dal proprio telefono, rispondere alla chiamata piuttosto che recarsi fisicamente a rispondere presso il telefono che sta squillando.
Il prelievo di chiamata diretto si applica a tutte le chiamate destinate all'interno, anche quelle ricevute in quanto membro di un gruppo di chiamata o di una coda.

Il KalliopePBX mette a disposizione due modalità di prelievo:

- diretto: l'utente che effettua il prelievo non ha alcuna informazione sul chiamante originale
- con invito: l'utente che effettua il prelievo verifica il chiamante originale prima di decidere se completare o meno il trasferimento

Operativamente il prelievo diretto viene effettuato digitando il codice di prelievo di chiamata diretto (default **) seguito dal numero di interno del destinatario originale della chiamata.
L'utente che ha effettuato il prelievo viene messo direttamente in comunicazione con il chiamante originale.

Nel caso di prelievo con invito invece il prelievo avviene digitando il codice di prelievo di chiamata diretto (default #*) seguito dal numero di interno del destinatario originale della chiamata.
L'utente che sta effettuando il prelievo riceve prima un segnale di riaggancio e successivamente una chiamata in ingresso che mostra come chiamante il chiamante della chiamata che si intende prelevare.
A questo punto l'utente che sta effettuando il prelievo può decidere se completare il trasferimento (rispondendo alla chiamata) o meno (rifiutando la chiamata).
Solo nel momento in cui il trasferimento viene completato il destinatario originale smette di squillare.


Configurazione del servizio
+++++
Il servizio può essere abilitato / disabilitato nel pannello PBX -> Piano di numerazione
Il codice del servizio può essere modificato nel pannello PBX -> Piano di numerazione

Interoperabilità con dispositivi di terze parti
+++++++
Nel caso in cui si voglia utilizzare questo servizio può essere molto utile avere a disposizione un tasto (con campo lampade) che consenta di verificare lo stato dell'interno su cui vogliamo effettuare il prelievo.
Per quanto riguarda il monitoraggio, il KalliopePBX invia dei messaggi SIP NOTIFY per comunicare i cambi di stato dell'interno. Il telefono dovrà inviare una SIP SUBSCRIBE per richiedere l’invio delle informazioni di stato. Questa operazione è normalmente effettuata configurando un tasto funzione di tipo BLF.
Oltre a monitorare lo stato dell'interno molti telefoni consentono con lo stesso tasto di effettuare anche il prelievo di chiamata sull'interno. In questo caso nella configurazione del tasto deve essere indicato il codice di prelievo chiamata

Esempi di configurazione
+++++

**Su SNOM** -> Operando tramite la web gui di configurazione configurare Function keys con:

.. code-block:: console

   Account: selezionare dalla tendina l’account che stiamo utilizzando (se c’è un solo account configurato sul telefono è il primo della lista)
   Type: BLF
   Value: <interno>|**
  
In alternativa modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">blf sip:<interno>@%%KPBX_IP_ADDRESS%%;user=phone|**</fkey>

dove %%id%% è l’identificativo del tasto da configurare e %%line_id%% è l’identificativo dell’account associato (il valore è 1 se sul telefono è presente un solo account).

Esempio:

.. code-block:: console

   <fkey idx="0" context="1" label="INTERNO103" perm="">blf sip:103@192.168.23.190;user=phone|**</fkey>
   
**Su YEALINK** -> Operando tramite la web gui di configurazione configurare DSS Key con: 

.. code-block:: console

   Type: BLF
   Value: <interno>
   Line: La linea associata all’account che stiamo utilizzando (Line 1 se sul telefono è presente un solo account)
   Extension: **
   
Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   memorykey.%%id%%.line=%%line_id%%
   memorykey.%%id%%.value=<interno>
   memorykey.%%id%%.type=16
   memorykey.%%id%%.pickup_value=**

Dove %%id%% è l’identificativo del tasto da configurare e %%line_id%% è l’identificativo dell’account associato il valore è 1 se sul telefono è presente un solo account).

Esempio:

.. code-block:: console

   memorykey.1.line = 1
   memorykey.1.value = 103
   memorykey.1.type = 16
   memorykey.1.pickup_value=**

Nel caso si intenda configurare il prelievo con invito è necessario sostituire il codice di prelievo diretto (**) con quello di prelievo con invito (#*).


Calling Line Identification Restriction (CLIR)
----

Descrizione del servizio
+++++++
Questo servizio consente ad un utente di nascondere la propria identità telefonica quando effettua una chiamata.
In questo modo anche se il chiamato ha un terminale abilitato al servizio CLIP (Calling Line Identification Presentation) non sarà in grado di risalire al numero telefonico del chiamante.

L'oscuramento del numero chiamante non è sempre possibile ed è comunque soggetto a restrizioni normative.
Le chiamate verso i servizi di emergenza ignorano l'abilitazione del CLIR (attraverso il servizio Calling Line Identification Restriction Override (CLIRO) e per alcune tipologie di chiamate (ad es. marketing / commerciale) non è consentito nascondere l'identità chiamante.

Questo servizio si applica sia alle chiamate tra interni che per le chiamate in uscita.
Nel caso di chiamate in uscita per il corretto funzionamento deve essere verificata la corretta configurazione del gateway di uscita e/o la modalità con cui il VoIP provider supporta il servizo CLIR.

Il servizio è attivabile/disattivabile per chiamata ed è possibile definire il comportamento di default di ogni interno.
Operativamente l'oscuramento del proprio numero chiamante avviene digitando il codice "Imposta" del servizio CLIR (default *671) seguito dal numero chiamato.
Nel caso in cui invece si voglia mostrare il proprio numero chiamante è necessario digitare il codice "Rimuovi" del servizio CLIR (default *670) seguito dal numero chiamato.

Configurazione del servizio
++++
Per utilizzare il servizio è necessario abilitarlo nel Piano di numerazione ed eventualmente modificare il codice da utilizzare.
L'abilitazione all'utilizzo del servizio e il comportamento di default deve essere specificato per ogni interno (anche tramite template interni).
Le configurazioni per interno oltre al comportamento di default nel caso di chiamate tra interni e verso l'esterno includono anche la possibilità di nascondere l'identità chiamante nel caso in cui il dispositivo chiamante invii il SIP Header Privacy: id.

Interoperabilità
++++
Quando viene abilitato il servizio CLIR la segnalazione SIP viene modificata come segue:

- viene sostituito la user part del From URI con anonymous (ad es. sip:anonymous@<ip_address_telefono>:<porta_telefono>)
- viene sostituito la user part del Contact Header con anonymous (ad es. sip:anonymous@<ip_address_registrar>:<porta_registrar>)
- viene aggiunto l'header SIP Privacy: id

Per le chiamate tra interni non sono necessarie ulteriori configurazioni mentre per le chiamate in uscita possono esere necessarie alcune modifiche in base alla tipologia di linea di uscita.

- VoIP Provider


Nel caso in cui il servizio CLIR sia abilitato è necessario comunque inviare al provider l'identità del numero chiamante.
Se questo non avviene di norma il provider rifiuterà la chiamata in uscita.
Questa informazione può essere inviata tramite P-Asserted-Identity Header o Remote-Party Header.
L'invio di questi header deve essere abilitato nella configurazione del trunk di uscita (Gateway e Domini VoIP -> Trunk).
Il formato accettato per gli header è normalmente quello suggerito nel pannello di configurazione.
Nel caso di problemi è necessario verificare con il proprio provider la configurazione richiesta.
Per evitare che questi header vengano sovrascritti è inoltre necessario impostare la modalità invio COLP a disabilitato (sempre nella configurazione del trunk di uscita).

Call Pickup di Gruppo (esplicito e con invito)
----

Descrizione del servizio
++++++
Questo servizio consente ad un utente del centralino di prelevare la chiamata diretta ad un qualsiasi interno appartenenente ad un gruppo di prelievo su cui è autorizzato.
Per ogni utente è possibile definire sia i gruppi a cui appartiene sia su quali gruppi può effettuare il prelievo.
Nel caso in cui ci siano più chiamate in ingresso il prelievo viene effettuato sull'ultima chiamata ricevuta da uno qualsiasi dei gruppi su cui l'utente è autorizzato al prelievo.
Il prelievo di chiamata di gruppo si applica a tutte le chiamate destinate all'interno, anche quelle ricevute in quanto membro di un gruppo di chiamata o di una coda.
Il KalliopePBX mette a disposizione due modalità di prelievo:

- diretto: l'utente che effettua il prelievo non ha alcuna informazione sul chiamante originale
- con invito: l'utente che effettua il prelievo verifica il chiamante originale prima di decidere se completare o meno il trasferimento

Operativamente il prelievo di gruppo viene effettuato digitando il codice di prelievo di chiamata diretto (default *9).
L'utente che ha effettuato il prelievo viene messo direttamente in comunicazione con il chiamante originale.
Nel caso di prelievo con invito invece il prelievo avviene digitando il codice di prelievo di chiamata diretto (default #9).
L'utente che sta effettuando il prelievo riceve prima un segnale di riaggancio e successivamente una chiamata in ingresso che mostra come chiamante il chiamante della chiamata che si intende prelevare.
A questo punto l'utente che sta effettuando il prelievo può decidere se completare il trasferimento (rispondendo alla chiamata) o meno (rifiutando la chiamata).
Solo nel momento in cui il trasferimento viene completato il destinatario originale smette di squillare.

Configurazione del servizio
++++
Il servizio può essere abilitato / disabilitato nel pannello PBX -> Piano di numerazione
Il codice del servizio può essere modificato nel pannello PBX -> Piano di numerazione
I gruppi di appartenenza e quelli di autorizzazione al prelievo sono definibili nel pannello dell'interno e configurabili anche mediante i template degli interni.

Interoperabilità con dispositivi di terze parti
++++
Nel caso in cui si voglia utilizzare questo servizio può essere molto utile avere a disposizione un tasto che consenta di effettuare la chiamata rapida al codice di servizio.

Esempi di configurazione
++++
**Su SNOM** -> Operando tramite la web gui di configurazione configurare Function keys con:

.. code-block:: console

   Account: selezionare dalla tendina l’account che stiamo utilizzando (se c’è un solo account configurato sul telefono è il primo della lista)
   Type: Speed Dial
   Value: *9
   
In alternativa modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">speed *9</fkey>

dove %%id%% è l’identificativo del tasto da configurare e %%line_id%% è l’identificativo dell’account associato (il valore è 1 se sul telefono è presente un solo account).

Esempio:

.. code-block:: console
   <fkey idx="0" context="1" label="PRELIEVO GRUPPO" perm="">speed *9</fkey>

**Su YEALINK** -> Operando tramite la web gui di configurazione configurare DSS Key con:

.. code-block:: console
   Type: Speed Dial
   Value: *9
   Line: La linea associata all’account che stiamo utilizzando (Line 1 se sul telefono è presente un solo account)
   Extension:

Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   memorykey.%%id%%.line=%%line_id%%
   memorykey.%%id%%.value=*9
   memorykey.%%id%%.type=13

Dove %%id%% è l’identificativo del tasto da configurare e %%line_id%% è l’identificativo dell’account associato il valore è 1 se sul telefono è presente un solo account).

Esempio:

.. code-block:: console
   memorykey.1.line = 1
   memorykey.1.value = *9
   memorykey.1.type = 13
   
 
Nel caso si intenda configurare il prelievo con invito è necessario sostituire il codice di prelievo di gruppo diretto (*9) con quello di prelievo con invito (#9).

Code di attesa (ACD)
----


Descrizione del servizio
++++
Il servizio ACD (Automatic Code Distribution), noto anche come servizio “code d’attesa”, consente di offrire un’accoglienza telefonica professionale impegnando l’attesa di chi chiama fintantoché non si libera un operatore. La chiamata in ingresso viene presa in carico dalla centrale che presenta al chiamante una serie di informazioni tramite file audio, musica d’attesa e mette in fila i chiamanti per distribuirli sui vari operatori della coda (o membri) sulla base di alcune politiche d’impegno che si possono configurare all’interno di ogni singola coda. Le “Code” sono un meccanismo analogo ai Gruppi di Chiamata, dai quali si differenziano per la possibilità di definire in maniera molto più raffinata la strategia di squillo e soprattutto per la modalità di smistamento delle chiamate in ingresso, che vengono accodate e servite con una politica FIFO (First In First Out) verso i membri della coda. Ad ogni coda può essere associato un numero arbitrario di membri (account), che serviranno le chiamate ad essa indirizzate. È importante ricordare che un operatore può essere impegnato su più code contemporaneamente e in caso di concomitanza di chiamate in attesa su più code, il servizio presenterà all’operatore la chiamata proveniente dalla coda a priorità più elevata.

Configurazione del servizio
+++++
*jpg*
Per accedere al servizio basta cliccare su “PBX” > “Code e gruppi di chiamata”. Ci troveremo così nella pagina dedicata alla lista delle code configurate con i parametri principali. Premendo su “Aggiungi una nuova coda”, possiamo passare alla configurazione della nuova coda.

*jpg*

Sono presenti i seguenti campi:

- Abilitato: pulsante che permette di selezionare la coda come attiva/non attiva
- Nome: campo che permette di inserire il nome che intendiamo dare alla coda (es. “Assistenza”)
- Priorità: valore numerico che permette di definire quale coda deve avere la priorità sulle altre, maggiore sarà il valore, più alta sarà la priorità
- Prefisso aggiunto al CLID: il prefisso viene aggiunto all’identificativo del chiamante (CLID) e consente di indicare sul display del terminale telefonico la coda di provenienza della chiamata (es. “ASS” per “Assistenza”)
- Controllo orario: è possibile scegliere i controlli orari già precedentemente configurati

Membri
+++++
Si definisce la lista degli operatori assegnati a questa coda. Per aggiungerli basta cliccare sul pulsante “Aggiungi membro”, è possibile scegliere tra i vari interni e di ciascuno selezionarne l’account. Se l’interno ha più account assegnati si può scegliere su quale account (terminale) andare a impegnare l’interno. La penalità è un valore che può essere assegnato a ogni operatore: più basso è il valore, maggiore sarà la possibilità di essere ingaggiato dal motore di accodamento. Più bassa è la penalità, più l’operatore è un “titolare” del servizio di quella coda.

*jpg*

Perché funzioni la distinzione basata sulle penalità è necessario che la strategia di squillo (campo presente nei “Parametri della coda”) sia di tipo ringall, cioè devono squillare tutti gli operatori (non c’è una distribuzione mirata sul singolo operatore). Quindi soltanto gli operatori disponibili con la più bassa penalità andranno ad essere impegnati. Si prenda ad esempio la seguente lista di membri di una coda:

*jpg*

Qualora la politica di impegno degli operatori sia impostata su “RingAll” solo gli operatori disponibili con la più bassa penalità squilleranno. Nel caso specifico di questo esempio, se l’interno 100 non dovesse essere già occupato, non registrato o in pausa, squillerà solo lui. Altrimenti squillerebbero contemporaneamente gli interni 102 e 101. Solo se anche questi ultimi fossero occupati, non registrati o in pausa squillerebbe l’interno 103. NOTA IMPORTANTE: qualora un operatore con la penalità minore non dovesse rispondere, sebbene disponibile, il motore di accodamento non passerà la chiamata agli operatori con penalità immediatamente superiore ma continuerà a far squillare l’operatore con penalità minore. Nell’esempio specifico se l’interno 100 risultasse disponibile la coda farebbe squillare sempre lui fintantoché non dovesse rispondere, senza scalare sugli interni 102 e 101 a penalità superiore.


Parametri della coda
+++++
*jpg*

- **Abilita pausa automatica**: funzionalità che mette automaticamente in pausa un operatore che non risponde a una chiamata a coda. Il funzionamento di questa opzione varia a seconda della strategia di squillo che si va a scegliere. Nel caso di ringall non è influente: la pausa automatica non viene attivata. Il concetto di pausa automatica viene introdotto per le funzionalità callcenter che permettono alla centrale di definire i ruoli di supervisore e operatore di coda. Qualora un utente fosse un operatore di coda ha, tra le possibilità, quella di mettersi “in pausa”. “In pausa” si intende cioè un utente registrato, disponibile e libero a livello telefonico, ma che comunque non può essere ingaggiato dalla coda. Lo stato di pausa/non pausa è tracciato all’interno dei registri della centrale, in modo da controllare il tempo di pausa dell’operatore. La messa in pausa è gestita tramite dei codici che abbiamo visto nella sezione del “Piano di enumerazione” e digitando i codici – personalizzabili – è possibile mettersi in pausa o togliersi dalla pausa.
- **Strategia di squillo**: menu a tendina che consente di definire le politiche di impegno degli operatori sulla coda, quindi il modo in cui il sistema distribuisce le chiamate entranti nella coda ai vari operatori. Scelte del menù a tendina:
   - **Tutti gli operatori (ringall)**: la chiamata arriva contemporaneamente a tutti gli operatori liberi della coda, tenendo in considerazione i valori delle penalità
   - **Lineare (linear)**: la chiamata viene inoltrata al primo operatore libero secondo la sequenza con la quale sono stati definiti i membri della coda (dall’alto verso il basso) ignorando il concetto di penalità che vale solo per ringall
   - **Meno recente (leastrecent)**: assegna la chiamata agli interni che da più tempo non rispondono alla chiamata. Il motore di accodamento della centrale tiene conto dell’ultima volta che l’operatore ha servito una chiamata della coda e, di conseguenza, lo assegna esclusivamente a quello che da più tempo non ha risposto
   - **Fewestcalls**: assegna la chiamata all’operatore che ha risposto a un numero inferiore di chiamate che viene calcolato sul giorno corrente, salvo riavvii della centrale
   - **Ciclica con memoria (RRMemory)**: distribuisce le chiamate con modalità round robin tra gli operatori disponibili e ricorda l’ultimo che ha cercato di chiamare
   - **Ciclica con ordinamento (RROrdered)**: come RRMemory, ma viene rispettato l’ordine degli operatori indicato nel file di configurazione
   - **Casuale (random)**: assegna la chiamata in modo aleatorio tra gli operatori disponibili

- **Durata dello squillo per operatore (sec.)**: indica per quanti secondi dovrà squillare il terminale dell’operatore ingaggiato (es. 15 sec). Durante questi secondi, se cambiano le condizioni (un altro operatore si libera e ci troviamo in una politica di ringall) la coda non presenta la chiamata all’operatore che si è appena liberato nel frattempo, ma andrà a includerlo nel pull degli operatori chiamabili solo alla scadenza del timeout di squillo successivo
- **Alla scadenza del timeout di squillo di tutti gli operatori, riprova dopo**: l’operatore ingaggiato squilla per un certo numero di secondi, ci sarà un’attesa di es. 5 secondi e poi andrà a scegliere il prossimo operatore secondo la strategia di squillo selezionata; squillerà nuovamente per 15 sec. Durante i 5 secondi il chiamante è in coda e non squilla nessun operatore.
- **Intervallo di riposo**: indica il tempo (sec.) per il quale l’operatore che ha appena concluso il servizio di telefonata (relativa alla coda), non verrà impegnato dalla coda
- **Alla risposta, riproduci questo messaggio all’operatore**: opzione che permette di selezionare un file audio precedentemente caricato. Nel momento in cui l’operatore risponde alla chiamata, prima di essere messo in comunicazione col chiamante, ascolterà un file audio che gli ricorderà da quale coda è proveniente quella chiamata. Questo tipo di opzione è utile per i callcenter multiservizio che rispondono per conto di terzi, per l’operatore – a volte – è funzionale presentarsi al chiamante
- **Notifica all’operatore il tempo di attesa del chiamante**: scelta che permette di comunicare all’operatore da quanto tempo il chiamante è in attesa
- **Avvio di chiamata agli operatori già impegnati in conversazione**: consente di attivare un’opzione qualora una coda fosse particolarmente importante, come per esempio relativa a un servizio ad alta priorità. Nell’ingaggio degli operatori si ignora il fatto che l’operatore ha il suo account già in conversazione, quindi la chiamata viene presentata comunque
- **Massimo tempo di attesa (sec.)**: parametro che monitora il tempo massimo di attesa oltre il quale scatenare un’azione di trabocco (vedi sotto)
- **Massimo numero di utenti permessi nella coda**: parametro che monitora il numero massimo di utenti permessi nella coda oltre il quale scatenare un’azione di trabocco (vedi sotto). (es. inserendo 0 non ci sono limitazioni)
- **Trabocco**: posso eseguire un file audio e poi un’azione di trabocco che è possibile scegliere nel menù a tendina

Trabocco immediato per le nuove chiamate
++++
Qualora un chiamante entrasse in una delle possibilità elencate nell’immagine sottostante, è possibile innescare immediatamente un trabocco, anche se non è stato raggiunto il tempo massimo di attesa e il numero massimo di utenti nella coda.

*jpg*
Trabocco immediato per le chiamate in coda
++++++
Trabocco immediato per le chiamate già in coda da tot tempo e nel caso si verificassero le possibilità elencate nell’immagine sottostante


Utenti della coda
++++
- **Messaggi di benvenuto**: è possibile selezionare un file audio precedentemente caricato
- **Classe di musica d’attesa**: il chiamante, dopo il messaggio di benvenuto, può ascoltare una musica di attesa (caricata precedentemente) o il normale tono di squillo
- **Annuncia la posizione in coda**: opzione che permette la comunicazione al chiamante della propria posizione in coda
- **Frequenza annuncio di posizione in coda (sec.)**: inserimento di una cifra che indica ogni quanti secondi aggiornare il chiamante del suo posizionamento in coda
- **Annuncia il tempo di attesa stimato**: calcolato sulla base delle statistiche del motore di accodamento, è possibile scegliere se annunciarlo ogni tot di secondi come la frequenza di annuncio della posizione in coda, solo una volta, o non annunciarlo.

Questo messaggio si innesca soltanto qualora il tempo di attesa medio sia superiore ai due minuti

Annuncio periodico personalizzato
++++
Strumento adottato, ad esempio, per comunicare al chiamante determinate procedure. È utilizzato per offrire informazioni più frequenti in richiesta a una determinata coda

- **Abilita l’annuncio periodico**: è possibile selezionare l’abilitazione dell’annuncio
- **File audio per l’annuncio periodico**: è possibile selezionare un file audio precedentemente caricato
- **Intervallo di riproduzione dell’annuncio periodico (sec.)**: inserimento del tempo (in sec.) dopo cui partirà ciclicamente il messaggio periodico

Messaggio su richiesta
++++++

- **Abilita la riproduzione su richiesta dell’operatore**: è possibile selezionare l’abilitazione del messaggio su richiesta
- **File audio per la riproduzione su richiesta**: è possibile selezionare un file audio precedentemente caricato
- **Sequenza da digitare per l’avvio dell’annuncio su richiesta**: sequenza che dovrà digitare l’operatore in conversazione su questa coda per scatenare il file audio caricato. (Es. l’operatore fa ascoltare determinate condizioni al cliente tramite la digitazione di un codice personalizzabile)


Richiamata su occupato
++++++
Servizio abilitato nel caso in cui sulla centrale viene assegnata la licenza callcenter. Consente al chiamante in attesa di non restare fisicamente al telefono per tutto il tempo prima di essere preso in carico da un operatore, ma si dà la possibilità – premendo il tasto 5 – di restare virtualmente in coda. Viene eseguito un IVR di sistema che chiede al chiamante se desidera essere ricontattato sull’attuale numero o se vuole essere richiamato su un altro numero (da specificare). L’utente rimane virtualmente in coda e la sua posizione non cambia, al suo turno la centrale chiama l’operatore disponibile che comunicherà alla centrale di innescare la richiamata verso l’utente che si era prenotato.

- **Abilitato**: è possibile può selezionare la richiamata su occupato
- **Classe di instradamento in uscita**: es. Italia no cellulari, se si inserisce un numero di cellulare il numero non verrà richiamato
- **Identità in uscita**: è una chiamata dalla centrale verso fuori, è possibile trattare il numero in uscita come se il chiamante fosse un interno già configurato

Integrazione con CTI
++++++
E’ possibile fruire di specifiche funzionalità messe a disposizione da ACD direttamente dai software Kalliope CTI e Kalliope Attendant Console quali ad esempio aggiunta dinamica degli operatori, metter in pausa gli operatori, accedere al supervisor pannel.
Si consideri il seguente esempio:

- attivare la licenza del modulo call center da Impostazioni di Sistema -> Licenze
- nel caso di versione multitenant, assegnare la licenza al tenant desiderato
- assegnare il ruolo di Supervisore all’utente preposto

All’apertura del software Kalliope CTI si avrà a disposizione:

- Un nuovo tab che consente di visualizzare le code a cui appartiene ed eventualmente mettersi in pausa.
- Nel caso di ruolo di supervisore è possibile accedere al Super visor panel


Piano di numerazione
-----

Descrizione del servizio
++++++++
Il piano di numerazione interno regola l’instradamento di una chiamata internamente al KalliopePBX. Il piano di numerazione viene impegnato dalle chiamate generate da un interno, e anche da quelle provenienti dall’esterno.
Per discriminare i diversi permessi associati a queste due tipologie di chiamata, il Piano di numerazione prevede due colonne, una con le selezioni abilitate per le chiamate originate da interni (locali e remoti) ed una per quelle provenienti da una linea esterna.
La selezione viene riscontrata sul piano di numerazione secondo l’ordinamento visualizzato, instradando la chiamata secondo la seguente priorità di matching:

1. Servizi
2. Selezioni personalizzate
3. Lista degli interni
4. Interni remoti
5. Altre selezioni


Servizi
+++++
Cliccando sulla matita, si apre il pannello di modifica delle selezioni e di abilitazione/disabilitazione dei vari servizi. I servizi abilitati ma a cui non è assegnata una selezione risultano inattivi.
*jpg*
Di seguito si riporta una descrizione dei singoli servizi attivabili:

- Prelievo di chiamata (di gruppo)
- Prelievo di chiamata diretto
- Prenotazione di chiamata
- Servizio eco
- Casella Vocale
- Audioconferenza
- Inoltro incondizionato
- Fork to Mobile
- Interruttori
- Ascolto passivo (servizio SPY)
- Codice commessa
- Pausa sulle code
- Parcheggio di chiamata

Riportiamo di seguito i valori di default dei servizi attivabili a livello di piano di numerazione.

.. list-table::  
   :widths: 25 25
   :header-rows: 1

   * - Descrizione
     - Selezione (di default)
   * - Prelievo di chiamata
     - *9
   * - Prelievo diretto
     - **<num.interno>
   * - Prelievo di chiamata di gruppo con invito
     - #9
   * - Prelievo di chiamata diretto con invito
     - #*<num.interno>
   * - CLIR (Imposta)
     - *671
   * - CLIR (Rimuovi)
     - *670
   * - Prenotazione di chiamata - CCBS/CCNR (Imposta)
     - 841
   * - Prenotazione di chiamata - CCBS/CCNR (Rimuovi)
     - 840
   * - Servizio Eco
     - 800
   * - Casella vocale
     - 801
   * - Audioconferenza
     - 802
   * - Lucchetto elettronico (Blocco)
     - 850
   * - Lucchetto elettronico (Sblocco)
     - 851
   * - Inoltro incondizionato (Blocco)
     - 811
   * - Inoltro incondizionato (Sblocco)
     - 810
   * - Fork to mobile (Commuta)
     - *50*
   * - Fork to mobile (Abilita)
     - *501
   * - Fork to mobile (Disabilita)
     - *500
   * - Fork to mobile (Controlla stato)
     - *509
   * - Interruttori (Commuta)
     - *51*<id>
   * - Interruttori (Abilita)
     - *511<id>
   * - Interruttori (Disabilita)
     - *510<id>
   * - Direttore-Segretaria (Commuta)
     - *52*<int.dir>[*<int.segr>]
   * - Direttore-Segretaria (Imposta)
     - *521<int.dir>[*<int.segr>]
   * - Direttore-Segretaria (Rimuovi)
     - *520<int.dir>[*<int.segr>]
   * - Gruppi di paging (Login)
     - *53<id>
   * - Hot Desking
     - *401
   * - Parcheggio di chiamata (Interno)
     - 888
   * - Parcheggio di chiamata (Primo slot)
     - 890
   * - Parcheggio di chiamata (Primo slot)
     - 899
   * - Speed Dial personali
     - #0<speed dial>
   * - Speed Dial di sistema
     - #<speed dial>
   * - Pausa sulle code (Imposta)
     - *81
   * - Pausa sulle code (Rimuovi)
     - *80
   * - Codice commessa
     - <cod.commessa>*<dest>
   * - Ascolto passivo (servizio SPY)
     - <codice><Interno da ascoltare> Accessibile solo da un interno assegnato ad un ruolo supervisore e utilizzabile solo su interni "operatore". Quando poi si è in chiamata, digitando i codici DTMF 4, 5 o 6 si può modificare la modalità di interazione (4=spy, 5=whisper, 6=barge)- Non esiste un codice di default. Va impostato.

Selezioni personalizzate
+++++
La seconda parte del Piano di numerazione permette di personalizzare l’instradamento associati a selezioni specifiche o archi di numerazione.
*jpg*
E' possibile manipolare il numero di selezione (togliere un certo numero di cifre in testa ed aggiunge un determinato prefisso) prima di inoltrarlo ad una delle destinazioni messe a disposizione dai menu a tendina contestuali.
Come destinazione di inoltro della chiamata è possibile scegliere tra:

- numero esterno
- un interno
- un gruppo di chiamata (tenendo conto o meno dell'eventuale controllo orario associato)
- una coda (tenendo conto o meno dell'eventuale controllo orario associato)
- un controllo orario
- un menu IVR
- una casella vocale
- una particolare stanza di audioconferenza MeetMe
- un'API esterna

La modifica di queste impostazioni viene effettuata cliccando sull’icona della matita sulla destra; il pannello di modifica elenca le regole di inoltro personalizzate che sono definite, ne permette la modifica, cancellazione e creazione. Si noti che le regole vengono automaticamente ordinate in fase di salvataggio (numericamente), ponendo come prime quelle esatte e successivamente quelle a range e a prefisso.

Controlli orari e interruttori
--------

Descrizione del servizio
+++++
I controlli orari sono un meccanismo per gestire l’instradamento delle chiamate su base temporale e manuale.

- **Su base temporale** perché si basano sulla definizione di fasce orarie riscontrate in sequenza, una dopo l’altra, per ciascuna delle quali è possibile definire la riproduzione di un particolare messaggio audio e il successivo inoltro della chiamata verso una specifica destinazione.
- **Su base manuale** perché i controlli orari possono utilizzare gli interruttori che sono un elemento particolare della centrale, un flag a due stati (acceso/spento), comandabile tramite un codice digitabile da telefono.
Normalmente, nelle soluzioni dei centralini telefonici tradizionali spesso si parlava di servizio giorno/notte, ovvero quel servizio che offriva un messaggio di cortesia negli orari di chiusura dell’ufficio, in questo caso il servizio del controllo orario permette di fare molte più scelte. È una entità di transito che può essere collegata in diversi punti del flusso di chiamata, dal momento che i controlli orari possono comparire nel menù a tendina di selezione di inoltro della chiamata al verificarsi di determinati eventi.

Configurazione degli interruttori
+++++++
Iniziamo configurando per prima cosa gli interruttori tramite **PBX > Interruttori**

*jpg*
L’interruttore può avere due stati, **acceso/spento**, è un servizio comandabile tramite la digitazione di un codice inserito da telefono o programmato su un tasto funzione di un terminale – dal momento che la centrale espone un servizio Busy Lamp Field con la visualizzazione dello stato – per commutare un interruttore e monitorare tramite il campo “lampade” se l’interruttore è acceso/spento.
Ci troviamo sulla pagina della Lista interruttori, cliccando su “Aggiungi interruttore” possiamo configurarlo.

- **Abilitato**: Abilitare o disabilitare un interruttore senza perderne la configurazione
- **Nome**: Identificativo dell'interruttore
- **Numero**: ID numerico dell'interruttore da utilizzare con il codice di abilitazione / disabilitazione / commutazione

Controllo di accesso dell’interruttore
+++++++
Ciascun interruttore prevede una ACL su base interni per il pilotaggio e quindi un’eventuale autenticazione

- **Interno**: Selezionare l'interno abilitato alla modifica dello stato dell'interruttore
- **Tipo di PIN**: Selezionare la modalità di autenticazione dell'interno, che può essere “Nessuno / Personalizzato / PIN dei servizi dell'interno”
- **Valore del PIN**: Inserire PIN personalizzato, solo se il valore precedente è impostato su Personalizzato

In PBX > Piano di Numerazione troviamo la pagina per attivare/disattivare/commutare gli interruttori.
Es. Per commutare basta digitare sul terminale telefonico:

- *51*1 per andare a cambiare lo stato dell’interruttore 1, dove 1 è l’id dell’interruttore
- *5111, per forzarne l’apertura, dove 1 è l’id dell’interruttore
- *5101 per forzarne la chiusura, dove 1 è l’id dell’interruttore

Mel caso in cui l’interruttore fosse spento e si provasse a digitare il codice di disabilitazione, resterebbe comunque spento. Qualora fosse stato impostato un PIN per la gestione degli interruttori, a seguito della digitazione di questo codice, verrà richiesto l’inserimento del PIN o della password affinché l’azione sull’interruttore venga completata correttamente.

Configurazione dei controlli orari
+++++
*jpg*

Procediamo andando su PBX > Controlli orari e cliccando su “Aggiungi controllo orario”

- **Abilitato**: Consente di disabilitare un controllo orario senza perderne la configurazione
- **Nome**: Identificativo del controllo orario
- **Abilita backdoor**: codice che consente di aggirare il controllo orario, inserendolo verrà applicata alla chiamata in ingresso l’instradamento previsto dallo scenario fuori dalle fasce orarie, ovvero “Trabocco fuori dalle fasce orarie”
- **Codice backdoor**: Consente di definire il codice di backdoor da utilizzare

Qualora venisse digitato il codice backdoor verrà forzato l’inoltro del trabocco fuori dalle fasce orarie. Questo servizio serve per impostare un controllo orario per apertura/chiusura di alcuni uffici ed è utile in caso si voglia lasciare ai dipendenti o ai soggetti con privilegi particolari, la possibilità di aggirare le limitazioni del controllo orario, digitando il codice. Ad esempio per entrare in comunicazione con un ufficio della propria azienda, indipendentemente dal fatto che verso il pubblico quell’ufficio risulta chiuso.

Fasce orarie
+++++++
Si possono indicare le fasce orarie di apertura o quelle di chiusura dell’azienda. Definiamo delle fasce orarie standard, durante le fasce orarie si possono prendere tutte le chiamate e girarle al trabocco durante le fasce orarie che presenta nel menu a tendina le varie scelte. Il menu a tendina presenta anche la voce “Ritorna al livello superiore” che permette di tornare indietro rispetto all’entità che ci ha portati su questo controllo orario. Vedi gruppi/code: i gruppi di chiamata fornivano la possibilità di definire un controllo orario, cioè una politica di accesso a servizio. Qualora inserissimo questo particolare controllo orario all’interno della configurazione di un gruppo o di una coda, per consentirgli di continuare l’accesso alla coda a cui è associato, dovremmo selezionare questa voce. Questo permette di usare lo stesso controllo orario in più gruppi e code.

**Situazioni particolari: festività**
Si può stabilire durante un determinato giorno, di procedere con azioni diverse. Per esempio, possiamo sovrascrivere il trabocco che abbiamo configurato come standard e configurarne uno differente. La disposizione grafica delle informazioni ha un senso importante: le scelte vengono fatte dall’alto verso il basso, quindi in alto vanno inserite le regole più particolari e poi in basso le più generali.

**Trabocco fuori dalle fasce orarie**: Azione di trabocco fuori dalle fasce orarie

Interruttori
+++++++++

Permettono di aggiungere il servizio giorno/notte manuale. Selezionando un interruttore precedentemente creato, come nell’esempio “Forza chiusura ufficio”, se dovesse risultare acceso e quindi volessi forzare la chiusura dell’ufficio dovrei mandare il file audio di chiusura e un’azione, es. “Riaggancia”. Se fosse chiuso e non volessimo forzare la chiusura, potremmo selezionare “Continua”, cioè si procede con l’interruttore successivo. Selezionando “Forza apertura ufficio”, verrà forzata l’apertura dell’ufficio indipendentemente dall’orario con cui abbiamo configurato il controllo orario. Se l’interruttore risulterà acceso, verrà eseguita la stessa azione configurata nel trabocco durante le fasce orarie. Qualora nessuno dei due interruttori sia acceso e comporti una forzatura, il controllo orario si comporterà sulla base della configurazione delle fasce orarie che abbiamo definito. Il codice backdoor interviene solo sul comportamento delle fasce orarie, se c’è una forzatura manuale di apertura/chiusura, il codice di backdoor non funziona.



Gruppi di chiamata
----

Descrizione del servizio
+++++++
Il servizio dei Gruppi di chiamata è un servizio di accoglienza della telefonata che serve a offrire al chiamante una sequenza ordinata di priorità di interni, a seconda della quale la chiamata andrà distribuita a uno o più interni in parallelo. Il gruppo di chiamata è un accorpamento di interni, distribuiti su diverse priorità a squillo contemporaneo, che individua dei reparti di un ufficio.

Configurazione del servizio
++++++
*jpg*
Procediamo cliccando su "PBX > Code e gruppi di chiamata" dal menu operativo.
Premendo su “Lista gruppi di chiamata” troviamo la lista dei gruppi già configurati.
Per passare alla configurazione, clicchiamo su “Aggiungi nuovo gruppo di chiamata”.

La configurazione prevede i seguenti campi:

- **Abilitato**: checkbox per abilitare o meno il gruppo
- **Nome**: inserire il nome che si preferisce
- **Prefisso aggiunto al CLID**: prefisso che viene aggiunto all’identificativo del chiamante (CLID) e consente di indicare sul display del terminale telefonico il codice personalizzabile di provenienza di quel determinato gruppo di chiamata (es. “ASS” per “Assistenza”)
- **Controllo orario**: è possibile definire per ciascun gruppo di chiamata un proprio controllo orario per differenziare i comportamenti a seconda dei giorni, mesi ecc.
- **Classe di musica d’attesa**: si può scegliere se presentare al chiamante il tono di squillo o una delle classi di musica d’attesa configurate sulla centrale
- **Trabocco**: al termine della consultazione di tutti i gruppi di priorità è possibile definire un’azione di trabocco, quindi in caso di assenza di risposta di qualsiasi interno appartenente a questo gruppo, è possibile eseguire uno dei file audio che avremo impostato e successivamente effettuare una delle azioni riportate nel menù a tendina

Priorità
+++++
Clicchiamo su “Aggiungi priorità” per procedere alla configurazione.

- **Durata dello squillo per operatore (sec.)**: valore che definisce la durata dello squillo di questo sottogruppo di priorità 1
- **Aggiungi interno**: definiamo gli interni appartenenti al gruppo di priorità 1

Aggiungendo un altro gruppo di priorità 2 (tramite “Aggiungi priorità”), sequenzialmente al gruppo 1, nel momento in cui passano i secondi di squillo del primo gruppo, si procede con il secondo.

I gruppi vengono eseguiti in sequenza, qualora nessun sottogruppo rispondesse alla chiamata, essa verrebbe deviata nel trabocco configurato.

Azioni di trabocco relative ai singoli interni coinvolti nei gruppi
+++++

Le azioni di trabocco del singolo interno – qualora la chiamata fosse diretta al gruppo e non al singolo interno – non vengono eseguite. Se l’interno 210 avesse un trabocco configurato sul proprio interno per mancata risposta verso numero esterno, nel momento in cui questo interno squillasse non perché chiamato direttamente, ma perché appartenente al gruppo di chiamata, il suo trabocco non verrebbe preso in considerazione. Allo stesso modo, le impostazioni lato centrale di inoltro incondizionato relative ai singoli interni appartenenti al gruppo non vengono prese in considerazione. Se si configura una deviazione sul terminale impostato con un account di un determinato interno, essa sarà correttamente eseguita perché non gestita dalla centrale, ma dal terminale. Qualora sull’interno fosse configurato il servizio Fork2Mobile – per far squillare il cellulare mobile associato al determinato interno – la chiamata viene fatta in parallelo anche sul mobile associato a quell’interno.


In sintesi:

- Le singole azioni di trabocco degli interni NON vengono eseguite
- L’attivazione del servizio di PBX «inoltro incondizionato» sugli interni NON causa la deviazione della chiamata
- L’attivazione della deviazione su uno dei terminali di un interno causa la deviazione della chiamata
- Il servizio Fork2Mobile dei singoli interni afferenti al gruppo viene invece innescata anche quando la chiamata è diretta al gruppo

Per inoltrare una chiamata in ingresso al gruppo di chiamata possono essere utilizzate due modalità:

- definire nel piano di numerazione una selezione personalizzata associata al gruppo di chiamata
- definire in un gateway o dominio VoIP una numerazione che abbia come destinazione il gruppo di chiamata


Inoltro di chiamata incondizionato
-------

Descrizione del servizio
+++++

Il servizio Inoltro Incondizionato consente di deviare la chiamata diretta ad un interno verso una differente destinazione (interna od esterna). Questa funzione può essere utilizzata per deviare le chiamate ricevute verso il numero di un collega o di un'altra qualsiasi selezione del piano di numerazione (e quindi anche verso gruppi o code, oppure sul proprio cellulare quando si è lontani dalla propria postazione di lavoro).

**NOTA**: il servizio opera solo sulle chiamate dirette all'interno e non per le chiamate destinate a gruppi di chiamata a cui l'interno appartiene, o a code di cui uno o più account dell'interno sono membri.

Ogni volta che viene attivato il servizio è necessario indicare verso quale numero deve essere programmato l’inoltro. Il KalliopePBX inoltrerà la chiamata in ingresso esclusivamente a questa numerazione. In caso di fallimento della chiamata non viene eseguita l’azione di trabocco dell’interno originale ma quella del destinatario dell’inoltro.

La chiamata inoltrata verso un numero interno presenterà sempre il chiamante originale mentre la chiamata inoltrata verso un numero esterno segue le regole di instradamento in uscita associate all’interno originale ed il numero presentato coinciderà sempre con quello che utilizza l’interno quando comunica verso la rete telefonica pubblica.

Operativamente l’attivazione/disattivazione del servizio Inoltro Incondizionato può essere effettuata in 3 modalità:

- **Da telefono**: il servizio viene attivato digitando il codice di attivazione (default 811) seguito dal numero verso il quale si vuole programmare l’inoltro. Il KalliopePBX conferma l’attivazione del servizio riproducendo il file audio “Salvato”. Nel caso in cui si voglia trasferire la chiamata verso un numero esterno deve essere anteposto il prefisso per le chiamate in uscita. Analogamente la disattivazione avviene digitando il codice relativo (default 810). In questo caso il KalliopePBX conferma la disattivazione con il messaggio “Grazie”. Questi codici possono essere utilizzati esclusivamente da un dispositivo associato all’interno su cui deve essere effettuata l’attivazione / disattivazione.
- **Da KalliopeCTI Desktop (in tutte le modalità)**: sotto la casella di composizione del numero appare l’icona Inoltro disattivato.png che identifica il Servizio Inoltro Incondizionato. Cliccando sull’icona il servizio viene attivato e l’icona diventa Inoltro attivo.png . La disattivazione viene effettuata cliccando nuovamente sull’icona. Posizionando il puntatore del mouse sull’icona è anche possibile visualizzare il numero verso il quale è configurato l’inoltro.
- **Da KalliopeCTI Mobile**: l’attivazione viene effettuata cliccando sul simbolo della ruota dentata Mobile tools.png nell’angolo in basso a destra e quindi cliccando sull’icona Mobile ufrwd off.png che identifica il Servizio Inoltro Incondizionato. Quando il servizio è attivo l’icona si modifica e accanto all’icona compare il numero verso il quale è stato programmato l’inoltro. Mobile ufrwd on.png Per disattivare il servizio è sufficiente cliccare nuovamente sull’icona.
Quando è attivo il servizio l’interno sui è abilitato l’inoltro non riceve la chiamata ma squilla unicamente il destinatario della deviazione. Tutti gli inoltri associati all’interno non sono pertanto applicati.

Configurazione del servizio
++++

Il servizio Inoltro Incondizionato è sempre attivo a livello globale.

L’abilitazione dei codici di attivazione / disattivazione da telefono e l’eventuale modifica sono gestiti nel Piano di Numerazione.

Interoperabilità con dispositivi di terze parti
+++++++++
Quando l’attivazione / disattivazione del servizio viene effettuata da telefono può essere molto utile avere a disposizione un tasto (con campo lampade) che consenta di verificare lo stato del servizio.

Per quanto riguarda il monitoraggio, il KalliopePBX invia dei messaggi SIP NOTIFY per comunicare i cambi di stato del servizio. Il telefono dovrà inviare una SIP SUBSCRIBE per richiedere l’invio delle informazioni di stato.

Questa operazione è normalmente effettuata configurando un tasto funzione di tipo BLF. L’oggetto da monitorare è ufwd<interno>.

Esempi di configurazione
+++++

**Su SNOM**

- Operando tramite la web gui di configurazione configurare Function keys con:

.. code-block:: console

   Account: selezionare dalla tendina l’account che stiamo utilizzando (se c’è un solo account configurato sul telefono è il primo della lista)
   Type: BLF
   value: ufwd<interno>

- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console
   
   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">blf sip:ufwd<interno>@%%KPBX_IP_ADDRESS%%;user=phone</fkey>

Dove %%id%% è l’identificativo del tasto da configurare E %%line_id%% è l’identificativo dell’account associato (il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console
   
   <fkey idx="0" context="1" label="Stato Inoltro 105" perm="">blf sip:ufwd105@192.168.23.112</fkey>

**Su YEALINK**

- Operando tramite la web gui di configurazione configurare DSS Key con

.. code-block:: console

   Type BLF
   Value: ufwd<interno>
   Line: La linea associata all’account che stiamo utilizzando (Line 1 se sul telefono è presente un solo account)

- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   memorykey.%%id%%.line=%%line_id%%>
   memorykey.%%id%%.value=ufwd<interno>
   memorykey.%%id%%.type=16
   
Dove %%id%% è l’identificativo del tasto da configurare

e %%line_id%% è l’identificativo dell’account associato il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console
   memorykey.1.line = 1
   memorykey.1.value = ufwd105
   memorykey.1.type = 16
   memorykey.1.pickup_value = %NULL%
   memorykey.1.xml_phonebook = %NULL%

Parcheggio della chiamata
-------

Descrizione del servizio
+++++++++
Questo servizio consente una volta che la comunicazione è stata instaurata di spostare la chiamata in uno slot di parcheggio.
Quando la chiamata è nello slot di parcheggio l'altro interlocutore viene messo in attesa mentre chi ha parcheggiato la chiamata può recuperarla da un qualsiasi telefono (non necessariamente quello che ha parcheggiato la chiamata). Nella configurazione di default sono disponbili 10 slot di parcheggio (890-899).
Se la chiamata non viene recuperata entro 90 secondi, viene automaticamente ripresentata al dispositivo (non all'interno) che l'ha parcheggiata.

Operativamente il trasferimento diretto viene effettuato digitando il relativo codice di servizio in chiamata (default #8).
Il KalliopePBX risponderà con il numero da chiamare per riprendere la comunicazione da un qualsiasi dispositivo.
A questo punto l'utente che ha parcheggiato la chiamata può riagganciare e riprenderla successivamente digitando il codice comunicato dal KalliopePBX.
Questa modalità di parcheggio richiede che non sia attivo il Direct Media per la chiamata in corso .
E' possibile utilizzare il servizio di Call Parking anche con Direct Media attivo semplicemente effettuando un trasferimento ad un interno a cui corrisponde il servizio di Call Parking (default 888).
In questo caso una volta effettuato il trasferimento con offerta, il KalliopePBX risponde con il numero da chiamare per riprendere la comunicazione.
A questo l'utente può riagganciare e riprenderla digitando il codice comunicato dal KalliopePBX.


Configurazione del servizio
+++++++

Il servizio può essere abilitato / disabilitato nel pannello PBX -> Servizi in chiamata
Il codice del servizio può essere modificato nel pannello PBX -> Servizi in chiamata
Il numero di slot di parcheggio utilizzabili e i corrispondenti interni sono configurabili nel pannello PBX -> Piano di numerazione


Interoperabilità
+++++++
Quando si utilizza il servizio di Call Parking può essere utile avere a disposizione un tasto (con campo lampade) che consenta di visualizzare lo stato di occupazione di ciascuno slot di parcheggio ed eventualmente riprendere la chiamata parcheggiata.

Per quanto riguarda il monitoraggio, il KalliopePBX invia dei messaggi SIP NOTIFY per comunicare i cambi di stato del servizio.
Il telefono dovrà inviare una SIP SUBSCRIBE per richiedere l’invio delle informazioni di stato.

Questa operazione è normalmente effettuata configurando un tasto funzione di tipo BLF.

L’oggetto da monitorare è l'interno corrispondente allo slot di parcheggio.
Oltre a monitorare lo stato di occupazione dello slot è possibile recuperare la chiamata parcheggiata cliccando sul tasto funzione corrispondente.


**Su SNOM**

- Operando tramite la web gui di configurazione configurare Function keys con:

.. code-block:: console

   Account: selezionare dalla tendina l’account che stiamo utilizzando (se c’è un solo account configurato sul telefono è il primo della lista)
   Type: BLF
   value: ufwd<interno>

- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console
   
   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">blf sip:<interno>@%%KPBX_IP_ADDRESS%%;user=phone</fkey>
   
Dove %%id%% è l’identificativo del tasto da configurare E %%line_id%% è l’identificativo dell’account associato (il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console
   
   <fkey idx="0" context="1" label="Slot parcheggio 890" perm="">blf sip:890@192.168.23.190</fkey>

**Su YEALINK**

- Operando tramite la web gui di configurazione configurare DSS Key con

.. code-block:: console

   Type BLF
   Value: <interno>
   Line: La linea associata all’account che stiamo utilizzando (Line 1 se sul telefono è presente un solo account)

- Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   memorykey.%%id%%.line=%%line_id%%
   memorykey.%%id%%.value=<interno>
   memorykey.%%id%%.type=16
   
Dove %%id%% è l’identificativo del tasto da configurare

e %%line_id%% è l’identificativo dell’account associato il valore è 1 se sul telefono è presente un solo account)

Esempio:

.. code-block:: console
   memorykey.1.line = 1
   memorykey.1.value = 890
   memorykey.1.type = 16
   memorykey.1.pickup_value = %NULL%
   memorykey.1.xml_phonebook = %NULL%





Servizio Echo
--------








Speed Dial
----------







Trasferimento di chiamata con offerta - conferenza a 3
-----









Trasferimento di chiamata senza offerta
-----




Voicemail
