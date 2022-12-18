Add-on
=====

.. _installation:

Kalliope FAX
------------

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

.. prompt:: bash $
   Oggetto: [KPBX40299999] FAX ricevuto correttamente da 050123456

dove 0501234567 è il numero da cui proviene il FAX.

Inoltre riportiamo un esempio del corpo dell'email (contenente altre informazioni):

.. prompt:: bash $
   Ricevuto FAX da 0501234567
   Data ed ora di ricezione: 12/03/2020 11:51:38
   Durata trasmissione: 34 secondi
   Num. pagine: 1 


Inoltre il file pdf allegato all'email ha il seguente pattern di naming:
F<0numero_chiamante>_T<numero_chiamato>_YYYY-MM-DD_HH_MM_SS_FAXID.pdf

A titolo esemplificativo riportiamo il nome che assumerebbe il file pdf allegato all'email di ricezione del FAX nel caso dell'esempio sopra citato.

.. prompt:: bash $
   F00501234567_T0509655637_2020-03-12_11_51_38_211.pdf

Inoltre è possibile visualizzare lo stato di avanzamento di tutti i fax ricevuti e scaricare il documento ricevuto nel registro FAX.





Kalliope Hotel
-----------------

Descrizione del servizio
++++++++++++++

Il modulo Kalliope Hotel è un add-on di KalliopePBX, attivabile tramite apposita licenza, che offre un set di funzioni specifiche per l’hospitality. Le funzioni incluse sono:


- **Pannello receptionist**: questo pannello è utilizzato dai receptionist dell’hotel per la gestione ordinaria delle camere e dei servizi relativi, inclusi lo stato di occupazione, il nome dell’ospite, eventuali annotazioni e la prossima tra le sveglie impostate. Per ciascuna stanza è possibile accedere ad un pannello di stato di dettaglio, in cui visualizzare in modo più esteso i dati della stanza ed effettuare le operazioni relative (attivazione di una sveglia, check-in/check-out, impostazione del nominativo dell’ospite principale, ecc.)
- **Servizio check-in/check-out**: questo servizio modifica lo stato di occupazione di una determinata camera da “libera” a “occupata” e viceversa. Gli eventi di cambio stato sono marcati temporalmente e vengono utilizzati per generare il rapporto di documentazione addebiti per le chiamate effettuate dal telefono della camera, in accordo alle tariffe configurate (disponibile a partire dal firmware 4.9.6). È possibile inoltre differenziare l’accesso ai servizi telefonici in ciascuno degli stati “libera” e “occupata” della camera, utilizzando il meccanismo delle Classi di abilitazione.
- **Servizio sveglia**: questo servizio permette di generare una chiamata ad un orario predeterminato verso l’interno associato ad una camera; il riscontro da parte dell’ospite può avvenire semplicemente rispondendo alla chiamata, oppure mediante conferma esplicita prima o dopo l’ascolto del messaggio di sveglia; in caso di mancata conferma, il sistema può ripetere la chiamata più volte, secondo la configurazione effettuata per il servizio. La programmazione della sveglia può essere effettuata via web tramite il pannello receptionist; Per ciascuna camera possono essere attive più sveglie, anche ad orari diversi per ciascun giorno.
- **Servizio “pulizia camera”**: questo servizio permette di marcare la stanza come pulita/sporca e di commutarne lo stato sia dal pannello Receptionist della GUI, che telefonicamente tramite un codice di servizio dalla persona che effettua la pulizia della camera. Lo stato di pulizia di tutte le camere occupate viene automaticamente impostato al valore “sporca” durante la notte, per poi poter essere riportato a “pulita” in modo manuale.


 Configurazione del servizio
 +++++++++++++++++
 
 
    
    
     
