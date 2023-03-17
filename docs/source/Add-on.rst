Add-on
=====

.. _installation:

Kalliope FAX
------------

    
.. raw:: html

  <div style="padding:30% 0 0 0;position:relative;">
    <iframe src="https://player.vimeo.com/video/526217255?h=7ac2c2814a&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;max-width:50%;" title="Tutorial Kalliope: demo Modulo Hotel">
    </iframe>
  </div>

Descrizione del servizio
+++++++++++
Il servizio FAX consente agli utenti Kalliope di inviare / ricevere fax dal proprio portale utente sulla WEB GUI o via e-mail.

Il servizio richiede l’acquisto di una licenza KPBX-V4-FAX. Ogni canale di licenza consente la configurazione di una istanza fax. L’istanza FAX corrisponde concettualmente ad un fax fisico al quale possono accedere uno o più utenti.

Configurazione del servizio
+++++++++++
Per la configurazione del servizio è necessario definire le impostazioni generali in termini di contemporaneità di utilizzo e archiviazione dei file ricevuti / inviati (inclusi report). Questa configurazione viene effettuata nel pannello FAX → Impostazioni FAX.

Impostazioni FAX
   Nel pannello di modifica impostazioni FAX è possibile impostare le configurazioni comuni a tutte le istanze FAX presenti nel sistema.
   
   *jpg*
   
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Parametro                   | Descrizione                                                                              | Tipo valore             |
   +=============================+==========================================================================================+=========================+
   | Impostazioni account                                                                                                                             |
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Contemporaneità in ingresso | Numero massimo consentito di FAX in ingresso nel PBX                                     | Numerico (0 = infinito) |
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Contemporaneità in uscita   | Numero massimo consentito di FAX in uscita nel PBX                                       | Numerico (0 = infinito) |
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Contemporaneità totali      | Numero massimo consentito di FAX in entrambe le direzioni nel PBX                        | Numerico (0 = infinito) |
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Percorsi di archiviazione (lista ordinata)                                                                                                       |
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Abilitato                   |                                                                                          | Checkbox                |   
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Tipo                        | Tipologia di storage: locale o remota                                                    | Locale / Remoto         |   
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Storage remoto              | Nome dello storage                                                                       | Dropdown                |   
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+
   | Cifratura                   | Algoritmo di cifratura da utilizzare per gli asset salvati su percorso di archiviazione  | Nessuna / Builtin       |   
   +-----------------------------+------------------------------------------------------------------------------------------+-------------------------+

Istanze FAX
   Successivamente è necessario configurare la specifica istanza FAX nel pannello FAX → Istanze FAX. Nel pannello Istanza FAX sono definiti gli attributi associati ad
   un’entità FAX. Un’istanza FAX deve corrispondere ad una selezione del piano di numerazione (come un interno), deve avere un nome e impegnare un canale di una
   licenza Kalliope FAX Module.
   
   *jpg*

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Tipo valore
   * - Abilitato
     -
     - Checkbox
   * - Selezione
     - Selezione del piano di numerazione corrispondente all’istanza FAX
     - Numerico
   * - Nome
     - Nome dell’istanza
     - Alfanumerico
   * - **Utenti abilitati (lista)**
     -  
     -  
   * - Utente
     - Utente a cui assegnare un permesso
     - Dropdown 
   * - Permesso
     - Permesso da assegnare all’utente
     - Solo ricezione / Solo invio / Invio e ricezione
   * - **Template**
     -  
     -  
   * - Template istanza FAX
     - Template da utilizzare per la configurazione dell’istanza
     - Dropdown
   * - **Impostazioni generali**
     -  
     -  
   * - Local station ID
     - Identificatore del FAX da inviare al dispositivo remoto
     - Alfanumerico
   * - Header info
     - Stringa di testo da includere nel margine superiore di ogni pagina inviata
     - Alfanumerico
   * - Contemporaneità totali
     - Numero massimo consentito di FAX in entrambe le direzioni
     - Numerico 
   * - ECM abilitata
     - Abilitazione Error Correction Mode
     - Checkbox      
   * - Rate minimo
     - Velocità minima di trasmissione
     - Numerico     
   * - Rate massimo
     - Velocità massima di trasmissione
     - Numerico     
   * - Modem
     - Standard modem supportati
     - Alfanumerico     
   * - **Impostazioni di ricezione**
     - 
     -
   * - Abilita ricezione
     - Abilitazione fax in ingresso
     - Checkbox      
   * - Contemporaneità in ingresso
     - Numero massimo consentito di FAX in ingresso
     - Numerico     
   * - **Impostazioni di trasmissione**
     - 
     -    
   * - Abilita invio
     - Abilitazione fax in uscita
     - Checkbox     
   * - Contemporaneità in uscita
     - Numero massimo consentito di FAX in uscita
     - Numerico     
   * - Classe di instradamento in uscita
     - Classe di instradamento da utilizzare per i FAX in uscita
     - Dropdown      
   * - Numero massimo di tentativi di trasmissione
     - Numero massimo di tentativi di trasmissione al termine dei quali il FAX viene dichiarato fallito
     - Numerico     
   * - Intervallo di ritrasmissione (minuti)
     - Intervallo di tempo tra un tentativo di ritrasmissione e il successivo
     - Numerico     
   * - **Impostazioni MAIL2FAX**
     - 
     -      
   * - Casella Mail2Fax
     - Nome della casella mail2fax
     - Alfanumerico     
   * - Metodo di autenticazione
     - Metodo di autenticazione con cui il Fax viene salvato e ricevuto
     - Dropdown      
   * - Pin di autenticazione
     - Pin con cui il Fax è autenticato da inserire anche nel testo della mail
     - Numerico     
   * - **Impostazioni di archiviazione**
     - 
     -     
   * - Prefisso del percorso
     - Prefisso da anteporre al percorso personalizzato del file archiviare
     - Dropdown     
   * - Percorso personalizzato
     - Percorso personalizzato in cui salvare il file da archiviare
     - Alfanumerico     
   * - Suffisso del percorso
     - Suffisso da posporre al percorso personalizzato del file archiviare
     - Dropdown     
   * - Archiviazione separata ingresso/uscita
     - Se e come archiviare separatamente i documenti in ingresso e in uscita
     - Prima del prefisso / Dopo il suffisso                         

**Nota**: Ricordarsi sempre di selezionare la Classe di instradamento in uscita.


Mail2Fax
   Se si vuole configurare anche il servizio MAIL2FAX è necessario selezionare dal pannello FAX → Istanze FAX, lista delle caselle Mail2Fax e aggiungere una nuova
   casella Mail2Fax.
   
   *jpg*
   
   
.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Tipo valore
   * - Abilitato
     - Abilitazione della casella Mail2FAX
     - Checkbox
   * - Nome
     - Nome della casella Mail2FAX
     - Alfanumerico  
   * - Indirizzo email
     - Indirizzo email associato alla casella
     - Alfanumerico  
   * - **Importazioni casella**
     - 
     - 
   * - Protocollo
     - Protocollo della casella di posta
     - Dropdown
   * - Abilita SSL
     - Abilitazione SSL	
     - Checkbox  
   * - Indirizzo del Server
     - Indirizzo del server di posta della casella mail
     - Alfanumerico  
   * - Porta del Server
     - Numero della porta del server di posta
     - Numerico
   * - Timeout
     - 	
     - Numerico  
   * - Nome Utente
     - Indirizzo mail dell'utente
     - Alfanumerico  
   * - Password
     - 	Password associata all'indirizzo mail dell'utente
     - Alfanumerico   
   * - **Chiave PGP Privata**
     -
     -
   * Da inserire solo nel caso di invio FAX con crittografia
     -
     -
     
Salvare le impostazioni e Applicare le modifiche.

Registro FAX
   Ogni utente a cui è stato assegnato il permesso di invio / ricezione su una istanza FAX visualizza il pannello FAX -> Registro FAX

   In questo registro è possibile:

   - visualizzare lo stato di avanzamento di tutti i fax ricevuti e scaricare il documento ricevuto.
   - visualizzare lo stato di avanzamento di tutti i fax inviati e scaricare il documento inviato e il report di invio
   
   *jpg*

Invio FAX
   *jpg*
   
   Ogni utente a cui è stato assegnato il permesso di invio su una o più istanze FAX visualizza sul proprio portale utente il pannello FAX -> Invia FAX

   Accedendo a questo pannello è possibile impostare le opzioni di invio del FAX:

   - la linea di origine (corrispondente all’istanza creata)
   - l’orario di invio qualora volessimo programmarlo, altrimenti l’invio sarà istantaneo
   - il destinatario
   - file da inviare (supportati i formati **pdf, doc, docx, odt**)

   Selezionando Invia il fax viene inviato.

   Per ogni fax inviato riceverà l’email di notifica dell’esito dell’invio del fax con il report di invio allegato.


Invio MAIL2FAX
   E’ necessario associare ad una istanza FAX la casella Mail2Fax. Nel pannello di modifica dell’istanza Fax, quindi selezionare in Impostazioni Mail2Fax:  
      - **Casella Mail2FAX**: nome della casella creata in precedenza
      - **Metodo di autenticazione**:
         - Nessuno: il fax viene inviato e ricevuto solo controllando l'indirizzo mail del mittente
         - PIN: la richiesta di invio FAX è autenticata anche mediante un pin che deve essere inserito nel testo della mail.
         - Firma PGP: l'identità del mittente della mail è autenticata tramite chiave PGP
      - **Richiedi cifratura messaggi**: è richiesto che l'allegato alla mail sia cifrato mediante la chiave PGP del mittente; è necessario in questo caso caricare le        chiavi pubbliche PGP nelle impostazioni di ciascun utente autorizzato all'uso del servizio.
  
   L'invio FAX tramite il servizio mail2fax richiede che, affinché il mittente venga riconosciuto ed il fax non scartato dal sistema, la mail mittente sia quella di      uno degli utenti abilitati all'uso del servizio (NOTA: il controllo della e-mail del mittente è case-sensitive, come quello della casella mail utilizzata per          raccogliere le mai lcon la richiesta di invio FAX) Quindi dal pannello Utenti e Ruoli, inserire per l’utente che gestisce l’istanza fax, l’indirizzo mail da cui        vengono inviate la mailFax. Selezionare modifica utente e inserire la mail nel campo apposito. E’ importante che che lo stesso indirizzo mail non sia presente per      più utenti (anche appartenenti a tenant diversi) per evitare che la mail non venga correttamente inviata e/o ricevuta.

   E’ ora possibile inviare da una casella di posta, la mail con il fax allegato. La mail deve avere:
      - nel campo OGGETTO il numero di telefono a cui inviare il fax. E’ possibile anche inserire l’istanza a cui inviare il Fax compilando l’oggetto con                       NumeroTelefono@istanza
      - nel campo DESTINATARIO l'indirizzo della casella mail2fax; la linea fax utilizzata per l'invio è (salvo che sia specificata esplicitamente nel campo OGGETTO)           la prima a cui la casella mail2FAX è associata
      - nel corpo della mail eventuale PIN associato all'istanza FAX, se si è scelta questa modalità di autenticazione
            - Il corpo della mail (in formato solo testo) deve contenere la sola stringa "FAXPIN:12345" (dove 12345 è il PIN assegnato in questo esempio)
      - come ALLEGATO il file del fax (supportati i formati pdf, doc, docx, odt)
   
   Se l’invio va a buon fine, nel pannello Registro Fax sarà visibile l’esito della transizione ed una mail di ricevuta verrà inviata al mittente.

Ricezione FAX
   Ogni utente a cui è stato assegnato il permesso di ricezione su una istanza FAX riceverà la notifica di ricezione del fax con il documento in allegato.
   La ricezione avviene con una email che ha come allegato il file pdf del fax ricevuto e come oggetto una stringa formattata nel seguente formato:
   **Oggetto: [SERIAL NUMBER] FAX ricevuto correttamente da 0XXXXXXXX**
   dove **0XXXXXXX** è il numero chiamante preceduto dallo 0 dell'impegno linea.

   Vediamo di seguito un esempio in caso di ricezione della notifica email di un FAX inviato dal numero 0501234567.

.. code-block:: console

   Oggetto: [KPBX40299999] FAX ricevuto correttamente da 050123456

dove 0501234567 è il numero da cui proviene il FAX.

Inoltre riportiamo un esempio del corpo dell'email (contenente altre informazioni):

.. code-block:: console

   Ricevuto FAX da 0501234567
   Data ed ora di ricezione: 12/03/2020 11:51:38
   Durata trasmissione: 34 secondi
   Num. pagine: 1 


Inoltre il file pdf allegato all'email ha il seguente pattern di naming:
F<0numero_chiamante>_T<numero_chiamato>_YYYY-MM-DD_HH_MM_SS_FAXID.pdf

A titolo esemplificativo riportiamo il nome che assumerebbe il file pdf allegato all'email di ricezione del FAX nel caso dell'esempio sopra citato.

.. code-block:: console

   F00501234567_T0509655637_2020-03-12_11_51_38_211.pdf

Inoltre è possibile visualizzare lo stato di avanzamento di tutti i fax ricevuti e scaricare il documento ricevuto nel registro FAX.





Kalliope Hotel
--------------

Descrizione del servizio
++++++++++++++

Il modulo Kalliope Hotel è un add-on di KalliopePBX, attivabile tramite apposita licenza, che offre un set di funzioni specifiche per l’hospitality. Le funzioni incluse sono:


- **Pannello receptionist**: questo pannello è utilizzato dai receptionist dell’hotel per la gestione ordinaria delle camere e dei servizi relativi, inclusi lo stato di occupazione, il nome dell’ospite, eventuali annotazioni e la prossima tra le sveglie impostate. Per ciascuna stanza è possibile accedere ad un pannello di stato di dettaglio, in cui visualizzare in modo più esteso i dati della stanza ed effettuare le operazioni relative (attivazione di una sveglia, check-in/check-out, impostazione del nominativo dell’ospite principale, ecc.)
- **Servizio check-in/check-out**: questo servizio modifica lo stato di occupazione di una determinata camera da “libera” a “occupata” e viceversa. Gli eventi di cambio stato sono marcati temporalmente e vengono utilizzati per generare il rapporto di documentazione addebiti per le chiamate effettuate dal telefono della camera, in accordo alle tariffe configurate (disponibile a partire dal firmware 4.9.6). È possibile inoltre differenziare l’accesso ai servizi telefonici in ciascuno degli stati “libera” e “occupata” della camera, utilizzando il meccanismo delle Classi di abilitazione.
- **Servizio sveglia**: questo servizio permette di generare una chiamata ad un orario predeterminato verso l’interno associato ad una camera; il riscontro da parte dell’ospite può avvenire semplicemente rispondendo alla chiamata, oppure mediante conferma esplicita prima o dopo l’ascolto del messaggio di sveglia; in caso di mancata conferma, il sistema può ripetere la chiamata più volte, secondo la configurazione effettuata per il servizio. La programmazione della sveglia può essere effettuata via web tramite il pannello receptionist; Per ciascuna camera possono essere attive più sveglie, anche ad orari diversi per ciascun giorno.
- **Servizio “pulizia camera”**: questo servizio permette di marcare la stanza come pulita/sporca e di commutarne lo stato sia dal pannello Receptionist della GUI, che telefonicamente tramite un codice di servizio dalla persona che effettua la pulizia della camera. Lo stato di pulizia di tutte le camere occupate viene automaticamente impostato al valore “sporca” durante la notte, per poi poter essere riportato a “pulita” in modo manuale.


Configurazione del servizio
+++++++++++++
 
Il Modulo Hotel viene configurato nel pannello “Modulo Hotel” “Configurazione”. La visibilità del pannello e dei relativi tab è condizionata all’attivazione della Licenza. Il pannello di configurazione prevede quattro tab:

- Lista Camere
- Lista Template delle Camere
- Valori predefiniti dei template delle camere
- Impostazioni globali

Impostazioni globali
 In questo pannello è possibile impostare il prefisso della selezione numerica da eseguire per impostare telefonicamente una stanza a pulita/sporca. Dall’interno di    ciascuna camera è possibile quindi effettuare una chiamata a tale prefisso seguito dal numero 0 per marcare la stanza come pulita o dal numero 1 per marcare la        stanza come sporca. Ad esempio nel caso di configurare come prefisso il codice *33, per marcare la stanza pulita è sufficiente chiamare la selezione *330 dal          telefono della camera. All’abilitazione del servizio, nel piano di numerazione verrà esposta in modalità sola lettura la relativa selezione. L’altra opzione            presente permette di abilitare o disabilitare il blocco delle chiamate dirette tra camere. Con il blocco attivo, non sarà possibile effettuare chiamate da una          camera all’altra in modo diretto; le camere potranno comunque chiamare gli altri interni della centrale (o essere chiamate da questi) o altre selezioni del            piano di numerazione.
 
 *jpg*
 
Configurazione delle camere
 La configurazione delle camere è effettuata in modo analogo a quanto viene fatto per la configurazione degli interni standard. Anche in questo caso è previsto un      meccanismo di configurazione basato su template (o modelli) per gestire le impostazioni comuni a più camere, ed un pannello in cui specificare i valori predefiniti    che saranno utilizzati ogni volta che viene creato un nuovo template di camera. Il flusso di lavoro quindi prevede prima di configurare i valori predefiniti dei        template, quindi creare uno o più template di camere, ed infine creare le vere e proprie camere, con i relativi numeri di interno. Come per gli interni standard,      anche a quelli delle camere è possibile assegnare uno o più account SIP, da utilizzare su uno o più terminali di camera; a differenza degli interni, non esiste una    distinzione particolare per gli account SIP utilizzati negli interni delle camere, per cui prima di procedere alla creazione delle camere è possibile creare gli        account necessari tramite il consueto pannello di gestione degli account SIP, nel menù “PBX” > “Interni ed account”. Come per gli interni, al fine di agevolare la      creazione di un numero elevato di camere è possibile ricorrere alla procedura di importazione massiva mediante file XLS/CSV, utilizzando come modello il file          disponibile cliccando sul link “Importazione massiva delle camere”.

*jpg*

Selezionando “Aggiungi nuova camera” è possibile aggiungere una camera alla lista e configurarla. Come indicato in precedenza, la configurazione delle camere ricalca la configurazione degli interni replicando il principio di configurazione mediante modelli (o template); i parametri disponibili per la configurazione delle camere sono un sottoinsieme di quelli degli interni standard. I parametri di configurazione di una camera sono:

- **Interno**: numero telefonico associato alla camera;
- **Nome**: Il nome della camera. Non necessariamente coincidente con il numero della camera, viene riportato insieme all’interno nella dashboard del receptionist;
- **Aggiungi account esistente/Crea account**: Consente di associare all’interno uno o più account SIP precedentemente creati, o di crearne uno in linea alla configurazione della camera;
- **Template dell’interno**: Indica il modello contenente i parametri di default da utilizzare per la tipologia di interno prescelta. Tutti gli attributi successivamente presenti nel pannello importano i valori di default ma è possibile sovrascriverli se necessario.

 
Le impostazioni successive sono ereditate dal template assegnato (modificabile dal pannello “Lista dei Template delle camere”, omologo a quello usato per i template degli interni standard) con possibilità di effettuare override per singola impostazione. In fase di creazione di un nuovo template di camera i valori di default sono inizializzati a quelli specificati nel pannello “Valori predefiniti dei template delle camere”. I parametri di configurazione della camera ereditabili da template sono:

- **Mostra nella rubrica locale**: Abilita o disabilita la visualizzazione dell’interno nella rubrica degli interni;
- **Modalità di pubblicazione LDAP**: Indica la modalità di pubblicazione dell’interno in LDAP tra le varie opzioni disponibili, in modo analogo a quanto previsto per gli interni;
- **Ente/Reparto**: questi due attributi di configurazione sono utilizzati come parametri di filtraggio all’interno della dashboard Receptionist, nel quale vengono interpretati con l’etichetta “Edificio” e “Piano”;
- **Classe di instradamento in uscita standard e ristretta**: come per gli interni, queste due classi determinano la tipologia (e l’instradamento) delle chiamate esterne permesse. Quando una camera si trova nello stato “libera” (quindi non occupata) viene assegnata al suo interno la classe ristretta mentre quando si trova nello stato “occupata” (e quindi è associata ad un ospite, a seguito di check-in) è possibile selezionare dal widget di gestione della camera quale delle 2 classi utilizza. In questo modo è possibile impedire le chiamate uscenti ai telefoni delle camere, anche se occupate, ed eventualmente sbloccarle su richiesta dell’ospite;
- **Limite chiamate contemporanee e livello di occupato**: identici alle omonime impostazioni dell’interno, permettono di definire rispettivamente il numero massimo di chiamate contemporanee possibili per l’interno e il numero di chiamate in corso su un interno al raggiungimento del quale questo deve essere considerato occupato (e quindi un eventuale ulteriore tentativo di chiamata a tale interno terminerà con tale esito);
- **Trabocchi**: come nel caso degli interni standard, indicano come deve essere gestita una chiamata destinata all’interno che termina per uno dei tre possibili esisti (non risposta, occupato, non disponibile) per ciascuna delle tre possibili origini (interna, esterna o trasferimento all’interno).


*jpg*

Servizio sveglia
 La licenza del modulo Hotel include l’abilitazione del servizio sveglia. Prima di poter utilizzare il servizio sveglia all’interno del modulo Hotel è necessario        effettuarne una preventiva configurazione, dal pannello “Applicazioni PBX” > “Servizio sveglia”. Il servizio sveglia permette di impostare una o più sveglie per        ciascuna camera, sotto forma di data e ora. AL momento previsto KalliopePBX si occuperà di effettuare una o più chiamate verso l’interno della camera ed                opzionalmente raccogliere la conferma di ricezione da parte dell’ospite.

La configurazione generale del servizio viene effettuata nel Tab “Impostazioni servizio sveglia”; queste includono:

- L’abilitazione esplicita del servizio;
- L’assegnazione di un Nome (che sarà utilizzato come Display Name per le chiamate effettuate dal servizio;
- Il file audio da riprodurre all’ospite nel momento in cui risponde alla chiamata del servizio sveglia;
   
Oltre a queste impostazioni necessarie sono presenti altri parametri con cui personalizzare le modalità di fruizione del servizio. Queste sono:

- Numero di tentativi di chiamata: è il numero massimo di chiamate che il PBX effettuerà verso l’interno per ciascuna sveglia impostata, nel caso in cui l’ospite      non dia conferma di aver risposto. Come impostazione predefinita la semplice risposta alla chiamata costituisce conferma di risposta, ma è possibile richiedere la      conferma mediante digitazione di un tasto prima o dopo la riproduzione del messaggio audio di sveglia;
- Timeout: è il tempo per il quale viene fatto squillare l’interno di destinazione prima di considerare il tentativo di sveglia fallito. Il sistema ripeterà la           chiamata un numero massimo di volte pari al valore impostato al punto precedente;
- Richiedi conferma di risposta: prima di riprodurre il messaggio audio viene chiesto di premere il tasto 1. La mancata digitazione del tasto impedisce il              proseguire della chiamata; in caso di riaggancio la sveglia viene considerata come “non confermata” ed un ulteriore tentativo di chiamata (se ve ne sono di residui)    viene eseguito dalla centrale;
- Richiedi conferma di ascolto: analogo al precedente, ma al termine della riproduzione del messaggio di sveglia (in questo caso viene chiesto di premere il tasto      9)
   
Al termine del numero di tentativi di chiamata senza che sia data conferma (secondo le modalità configurate esposte sopra) la sveglia risulterà “non risposta” e comparirà un avviso nella dashboard del receptionist a fini informativi. Tali avvisi potranno essere riscontrati (e quindi cancellati) dal receptionist dopo che questi abbia effettuato le necessarie azioni (chiamata manuale alla stanza, ecc.). I due tab presenti nel pannello “Lista di istanze di sveglie” e “Lista di istanze svegli terminate” contengono l’elenco delle sveglie attive e di quelle terminate. Il primo pannello contiene quelle programmate nel futuro, correntemente attive oppure terminate senza conferma di ricezione; il secondo pannello contiene invece l’elenco delle sveglie completate con risposta oppure quelle non risposte ma prese in carico manualmente dal receptionist (a seguito dell’annullamento dell’avviso sul pannello receptionist). In entrambi i casi per ciascuna sveglia è possibile visualizzare l’elenco completo degli eventi relativi a ciascun tentativo di chiamata con i relativi timestamp.

Pannello Receptionist
   Questo pannello raccoglie tutte le camere e viene utilizzato dai receptionist dell’hotel per la gestione ordinaria delle camere e dei servizi relativi. E’diviso in due parti, la colonna di destra che contiene le notifiche per le sveglie non risposte dagli ospiti, l’area principale a sinistra in cui sono visualizzate in forma di matrice tutte le camere raggruppate in base agli attributi “edificio” e “piano” di collocazione. Gli avvisi di “sveglia non risposta” compaiono automaticamente nel momento in cui terminano senza successo tutti i tentativi di chiamata associati alla sveglia di una camera; l’avviso riporta il nome e numero della camera, e l’orario a cui la sveglia era programmata. Cliccando sulla X all’interno dell’avviso questo viene cancellato; parallelamente la sveglia corrispondente viene spostata dal pannello di quelle attive a quello delle sveglie terminate (vedi sezione precedente relativa al servizio sveglia). Ciascuna camera configurata nella centrale compare all’interno della sezione di sinistra della dashboard sotto forma di widget (o riquadro); il colore del widget indica lo stato di occupazione della camera: una camera “verde” è libera mentre una camera “rossa” è occupata da un ospite. In quest’ultimo caso i 4 campi testuali presenti all’interno del riquadro della camera indicano nell’ordine:

- Il nominativo dell’ospite (o degli ospiti);
- Eventuali note associate alla camera;
- La prima sveglia programmata per quella camera;
- Il costo complessivo delle chiamate effettuate dalla camera a partire dall’istante di check-in al momento attuale (disponibile a partire dal firmware 4.9.6).

La barra superiore permette di applicare in tempo reale un filtraggio nella visualizzazione delle camere in base a:

- Edificio e/o piano;
- Stato di pulizia;
- Corrispondenza di un testo libero sui campi “nominativi ospiti” e “note” della camera;
- All’interno del widget è infine presente un pulsante con l’icona di un’aspirapolvere; questo pulsante ha la duplice funzione di indicare e poter commutare lo stato di pulizia della camera.

In caso di camera sporca il pulsante è acceso (in colore giallo); cliccando sul bottone il receptionist ha inoltre la possibilità di commutare lo stato da “sporca” a “pulita” e viceversa. Lo stato di pulizia delle camere è aggiornato ogni 10 secondi; una eventuale modifica dello stato mediante codice telefonico dalla stanza si riflette in tempo praticamente reale sullo stato visualizzato sul pannello.

*jpg*

Cliccando all’interno del widget di una camera si accede al pannello di stato di dettaglio, in cui è possibile eseguire le operazioni di check-in e check-out e visualizzare in modo più esteso i dati della stanza. 

*jpg*

Selezionando una stanza libera è possibile effettuare il check-in cliccando sul pulsante omonimo; in fase di check-in è necessario indicare il nominativo di almeno un ospite della camera, ma è possibile aggiungere anche i nominativi degli ospiti addizionali, così come eventuali note testuali. Contestualmente al check-in si può scegliere quale delle due classi di abilitazione (alle chiamate esterne) attribuire alla camera; tale impostazione è poi modificabile in seguito tornando nel pannello di dettaglio della camera.

In maggior dettaglio, durante l’operazione di check-in è possibile inserire i seguenti dati associati alla camera:

- **Intestatario (obbligatorio)**: nome della persona a cui è intestata la camera. È possibile aggiungere ospiti addizionali selezionando “Aggiungi addizionale”. In fase di filtraggio delle camere dalla dashboard, la ricerca a testo libero opera su tutti i nominativi inseriti.
- **Sveglie**: Data e ora a cui impostare la sveglia per la stanza se richiesta dall’intestatario. È possibile aggiungere una o più sveglie selezionando aggiungi. Questo servizio può essere impostato soltanto dall’operatore.
- **Chiamate esterne**: abilitare le chiamate esterne dalle camere con classe standard o ristretta. Questo servizio prevede la generazione di un reporter dettagliato delle chiamate effettuate dal telefono di una camera a partire dal momento del check-in comprensivo del costo calcolato a partire dalla durata in base ad una specifica tariffa, configurabile.
- **Note**: testo libero, permette di inserire dei promemoria. In fase di filtraggio delle camere dalla dashboard, la ricerca a testo libero opera anche sul contenuto di questo campo.

Completata la configurazione, cliccando su “Salva” viene effettuato il check-in (il widget passa da verde a rosso), ed il relativo timestamp viene associato alla camera per il calcolo della competenza delle chiamate. Oltre a queste impostazioni, nel pannello di dettaglio della camera è possibile visualizzare lo stato di pulizia della camera e (dal firmware 4.9.6) il conteggio cumulativo del costo delle chiamate effettuate dall’interno della camera a partire dall’istante di check-in fino all’istante corrente. Selezionando invece una stanza occupata, è possibile cliccare sul pulsante “Check out” per eseguire l’azione corrispondente (previa conferma), a seguito della quale lo stato della camera torna a disponibile (“libera”).

Lista Storico Prenotazioni
   In questo pannello è possibile visualizzare lo storico delle prenotazioni per ogni singola camera, visualizzando data ed ora del check-in e check-out, nome degli ospiti ed eventuali note. Per ogni camera è inoltre possibile scaricare il report XLSX con l’elenco delle chiamate effettuate dagli ospiti di quella camera all’interno del periodo di occupazione. Il pannello contiene sia le occupazioni correnti (per le quali quindi il timestamp di check-out è vuoto che quelle passate. Le informazioni relativi agli ospiti e le note presenti al momento del check-out vengono salvate nello storico prenotazioni.

*jpg*

Documentazione addebiti (Servizio Billing)
   Il servizio di Documentazione Addebiti presente su KalliopePBX (attualmente disponibile come componente inclusa nella licenza del Modulo Hotel), permette il calcolo dei costi delle chiamate effettuate da ogni interno associato ad una camera, tramite la definizione di un profilo di costo differenziabile in base alla destinazione (con un certo prefisso, numeri esatti, tutti gli altri numeri) ed alla linea di uscita utilizzata. Per maggiori informazioni clicca qui

Kalliope LAM
-------------

Descrizione del servizio
+++++++++++
Il modulo Kalliope LAM (Look At Me) è un add-on di KalliopePBX, attivabile tramite apposita licenza, che offre un set di funzioni specifiche per favorire la continuità operativa di un’azienda, indipendentemente dalla posizione in cui si trovino i propri dipendenti e clienti. KalliopeLAM permette infatti di organizzare delle riunioni virtuali proprio come avverrebbe in sale riunioni fisiche. Basata su motore open-source e completamente in cloud, è una piattaforma web based (click and go); i partecipanti alle riunioni accedono al meeting tramite il proprio browser web, semplicemente cliccando sul link contenuto nell’email di invito. Disponibile anche la versione app mobile per i sistemi operativi Android e iOS scaricabile gratuitamente da Google Play e App Store. Per maggiori informazioni sull'app mobile KLAM (clicca qui).

Configurazione del Servizio
++++++++++++
La gestione della piattaforma KalliopeLAM da parte degli utenti, ad esempio per la creazione eventi o l’assegnazione dei permessi, è completamente integrata nell’interfaccia web del PBX.La soluzione KalliopeLAM non è licenziata per utenti ma per stanze, ciascuna licenza abilita una stanza di videoconference, una vera e propria sala riunioni virtuale per la quale sarà possibile:

- Assegnare un nome alla stanza
- Definire le ownership della stanza: ovvero assegnarne l’uso ad uno o più utenti. Non ci sono limiti al numero di amministratori per stanza, basta che siano interni del PBX. L’utente che ha i permessi di gestione dell’intero servizio KalliopeLAM, ha la panoramica completa delle sale riunioni virtuali; può scegliere una stanza.

*jpg*

L’utente può:

- Accedere al calendario di "pianificazioni riunioni" di una determinata stanza e scegliere tra organizzare una riunione.
*jpg*

- Creare una nuova riunione inserendo i seguenti campi: nome della riunione, orario, password di accesso (opzionale), elenco dei partecipanti.
*jpg*

- Spedire gli inviti e i calendar a tutti i partecipanti dei una riunione cliccando sul pulsante “Salva e invia”.

Principali funzionalità
   - Videoconference web.
   - Protezione della riunione con password.
   - Waiting-room.
   - Desktop sharing
   - Chat
   - Alzata di mano
   - Statistiche interlocutore
   - Condivisione video YouTube
   
Protezione della privacy delle tue riunioni
   Sono stati implementati diversi meccanismi per garantire la privacy e la protezione tue riunioni sulla piattaforma KalliopeLAM.

- Nuove istanze di videoconference per ciascuna nuova riunione: Le diverse istanze saranno valide solo nel periodo indicato per la prenotazione, inizio e fine della riunione. Tali istanze (rappresentate nell’URL di condivisione della riunione) sono composte da 42 caratteri alfanumerici e nel caso di un invito come moderatore, sarà presente in coda all’URL un ulteriore token di 493 caratteri.
- Waiting room abilitata di default: Il moderatore viene avvisato del fatto che ci sia un guest che ha fatto richiesta di entrare e può decidere di accettarlo o meno. La waiting room è disabilitabile dal moderatore riunione per riunione.
- Definizione di una password di protezione per l’accesso alla riunione : La password può essere definita in due diversi momenti: o in fase di programmazione della riunione e durante lo svolgimento della riunione stessa.
- Se il moderatore esce dalla riunione i guest vengono disconnessi
- Il moderatore può eleggere a “moderatore” altri utenti
