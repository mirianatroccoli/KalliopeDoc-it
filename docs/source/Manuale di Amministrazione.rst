Manuale di Amministrazione
=====

Concetti base
====

Caratteristiche di base
-----
SIPv2 (UDP, TCP, TLS and WebSocket; RTP e SRTP)
Codec audio supportati (con transcoding) : G.711 (A.law, u.law), G.726, GSM, G.722 (wideband), G.729, Opus
Codec video supportati (passthrough, no transcoding): VP8 H.264, H.263+, H.263, H.261
Supporto Fax (audio o T.38 passthrough)
Busy Lamp Field
Supporto ENUM
Controllo accessi sugli IP per gli interni (ACL)
Supporto SNMP (v1/v2c) in lettura (demone Net-SNMP)
Supporto LDAP (sia client che server)

Interni e account SIP
---------

Gli interni sono le principali entità telefoniche. Un interno è un'entità logica associata ad un numero che viene usato come identificativo per tutte le chiamate effettuate dall'interno ed è il numero digitato da chi vuole contattare l'interno. Ogni interno ha alcuni attributi che ne definiscono i permessi (per le chiamate uscenti dall'interno) e il comportamento (per chiamante entranti all'interno), insieme a certe informazioni identificative (nome e cognome, ente, ecc.).

Gli account SIP sono entità di "servizio" e consistono delle credenziali (username e secret) che devono essere configurate su un terminale SIP (hardphone o softphone) per l'autenticazione sul PBX. L'autenticazione è effettuata dai dispositivo con due procedure: "registrazione SIP" e l'esecuzione di una nuova chiamata.

Il rapporto fra gli interni e gli account SIP è uno a molti: ogni interno può essere associato a più di un account SIP, che si comorteranno tutto come un'unica entità telefonica per quanto riguarda identità, presentazione, permessi, ecc.

È anche possibile creare un utente unico per ciascun interno; a questi utenti si possono assegnare permessi e ruoli diversi per permettergli di accedere alla propria pagina web personale, eseguire certe mansioni di amministrazione o di configurazione, utilizzare le applicazione KalliopeCTI (Desktop o Mobile) e invocare le API REST disponibili. Per ulteriori dettagli, vedere la pagina su utenti e ruoli.

Registrazione SIP e più dispositivi per interno
++++++

La registrazione SIP fornisce al PBX le informazioni sull'attuale posizione dell'account SIP, cioè l'indirizzo IP e la porta (insieme al protocollo, per esempio UDP, TCP, TLS o WebSocket) dove si può trovare l'account SIP quando il PBX deve mandargli un messaggio (per esempio un INVITE relativo ad una chiamata entrante). La registrazione è eseguita dal dispositivo durante l'attivazione (se l'account è configurato correttamente) e viene aggiornata periodicamente prima che ne scada la validità; ogni registrazione periodica richiede la ripetizione della procedura di autenticazione. Il tempo di validità della registrazione viene stabilito durante la procedura. Il dispositivo inserisce un valore di "Proposed Expiry" (in secondi, solitamente 3600 di default) nella richiesta REGISTER; se l'autenticazione ha successo, il PBX risponde con un messaggio "200 OK" che notifica l'effettivo tempo di registrazione al dispositivo, che quindi deve mandare una nuova registrazione prima della scadenza (solitamente questa registrazione viene effettuata quando è passato circa metà del tempo, per avere tempo di rimandarla in caso di fallimenti). Se il timeout di registrazione scade senza che la registrazione sia aggiornata, la posizione dell'account viene scartata dal PBX e le chiamate destinate a quell'account falliranno perché il dispositivo risulterà "non disponibile".

KalliopePBX salva un'unica posizione per ogni account SIP configurato; se lo stesso account SIP è configurato su più dispositivi attivi contemporaneamente, i messaggi periodici di registrazione mandati di ciascun dispositivo cambieranno ripetutamente la posizione salvata sul KalliopePBX. Una chiamata destinata all'account SIP verrà quindi presentata solo al dispositivo che ha eseguito la registrazione per ultimo. È però possibile avere più dispositivi che si comportano come un unico interno definendo un account SIP per ogni dispositivo desiderato e associando ciascuno di essi allo stesso interno.

Attributi e template degli interni
+++++
Ogni interno ha il proprio insieme di attributi che ne descrivono l'identità e il comportamento telefonico. Alcuni attributi sono specifici per ciascun dispositivo e devono essere configurati individualmente, mentre altri possono essere in comune ad un sottoinsieme di interni. I primi includono il numero di interno stesso (che deve essere unico nel PBX, o in ciascun tenant in sistemi multi-tenant) e dettagli personali come nome e cognome, indirizzo e-mail, e il codice PIN personale usato per l'autenticazione per accedere certi servizi del PBX. I secondi includono limiti e permessi di chiamata e le azioni di trabocco da eseguire quando una chiamata all'interno fallisce, che dipendono dall'origine della chiamata e dalla causa del fallimento.

Per facilitare la gestione di questi attributi comuni, KalliopePBX introduce il concetto di template di interno: un insieme di attributi e impostazioni che possono essere assegnati a più interni. Definendo più di un template (con diverse impostazioni per ogni tipo di interno), si può ridurre il numero di impostazioni da specificare per ciascun interno e permette di modificare facilmente la stessa impostazione per ogni interno che condivide lo stesso template semplicemente modificando il valore dell'impostazione ne relativo template.

Nel pannello di configurazione per ogni interno si può sovrascrivere qualunque impostazione ereditata dal template se è necessaria un'eccezione. Le impostazioni sovrascritte non cambiano quando viene modificato il template.

Attributi degli account SIP
++++++
Come gli interni, gli account SIP hanno attributi specifici (principalmente lo username, che deve essere unico nel PBX, e il SIP secret) e attributi che possono essere comuni ad una "classe" di account. Questi includono i protocolli di trasporto, emdia e codec supportati, l'ACL autorizzato, e altri; some per gli interni, si possono usare template di account SIP con impostazioni comuni.

Configurazione Interni
+++++

*jpg*

Nel pannello interni sono definiti gli attributi associati ad un utente che utilizza i servizi messi a disposizione dal KalliopePBX. L’attributo principale che identifica l’utente è l’interno telefonico (Telephone Extension). Nel caso in cui più apparati (Account) siano associati allo stesso utente questi condivideranno l’identità telefonica definita in questo pannello. Questo significa ad esempio che le chiamate verso l’interno telefonico saranno presentate a tutti gli apparati associati all’utente e che le chiamate effettuate da qualsiasi apparato dell’utente presenteranno la stessa identità telefonica.

Per configurare gli interni basta aprire il menu operativo e cliccare su PBX > Interni e Account.
Per creare un nuovo interno procedere cliccando su "Aggiungi interno".

- **Abilitato**: Consente di disabilitare un interno senza perderne la configurazione
- **Interno**: Indica il numero telefonico interno al PBX al quale è possibile contattare l’utente
- **Nome**: Utilizzato per costruire il Display Name visualizzato dai telefoni e per la pubblicazione dell’utente in rubrica
- **Cognome**: Utilizzato per costruire il Display Name visualizzato dai telefoni e per la pubblicazione dell’utente in rubrica.
- **Indirizzo e-mail**: Indirizzo e-mail utilizzato per la pubblicazione dell’utente in rubrica
- **Numero mobile**: Numero telefonico utilizzato per la pubblicazione nella rubrica interni e per i servizi Fork2Mobile e FastTransfer
- **PIN dei serivizi**: Codice da utilizzare per l’accesso ai servizi telefonici che possono richiedere autenticazione (casella vocale, interruttori, paging, lucchetto elettronico)

**Account**


.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Aggiungi account esistente
     - Consente di associare all'interno uno o più account SIP precedentemente creati
     - Account
   * - Crea account
     - Consente di creare un nuovo account SIP da associare all'interno
     - Account
 
 **Casella vocale**
 
.. list-table::  
   :widths: 25 25 50
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore   
   * - Crea casella vocale
     - Consente di creare la casella vocale dell’interno
     - Si / No
   * - Indirizzo e-mail
     - Indica l’indirizzo e-mail da utilizzare per ricevere le e-mail di notifica ricezione messaggi in casella vocale con opzionalmente allegati i file audio contenenti i messaggi registrati.
     - xxxxx@dominio.yy
   * - Notifica nuovi messaggi in casella vocale tramite email
     - Se questa opzione è abilitata viene inviata via e-mail la notifica di ricezione di un messaggio in casella vocale
     - Si / No
   * - Inoltra i messaggi vocali come allegati
     - Se questa opzione è abilitata viene allegato all'e-mail il file audio contenente il messaggio registrato
     - Si / No
   * - Cancella da Kalliope i messaggi vocali inoltrati
     - Se questa opzione è abilitata una volta effettuato l’invio via e-mail le registrazioni vengono cancellate dal KalliopePBX e non saranno quindi più accessibili da telefono o dall'app KalliopeCTI Mobile
     - Si / No
   * - Abilitato
     - Consente di abilitare o disabilitare la casella vocale senza perderne la configurazione ed i messaggi ricevuti
     - Si / No

**Impostazioni utente locale**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Crea utente locale
     - Consente di creare un utente locale sul KalliopePBX nel caso in cui sia necessario abilitare l’accesso GUI o CTI
     - Si / No
   * - Abilita accesso GUI
     - Abilita l'accesso utente alla WEB GUI con ruolo standard Utente di Tenant. Il ruolo associato all'utente può essere modificato nel pannello Gestione utenti
     - Si / No
   * - Abilita accesso CTI
     - Abilita l’utente ad utilizzare i client KalliopeCTI. Nel caso in cui sia richiesta la modalità di utilizzo KalliopeCTI PRO o KalliopeCTI PHONE è necessario assegnare la licenza all'utente nel pannello Gestione utenti
     - Si / No
   * - Nome utente
     - Nome utente da utilizzare per il login della GUI o dei client CTI
     - Alfa-numerico
   * - Password
     - Password da utilizzare per il login della GUI o dei client CTI
     - Alfa-numerico

**Template**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Template dell’interno
     - Indica il template contenente i parametri di default da utilizzare per la tipologia di interno prescelta. Tutti gli attributi successivamente presenti nel pannello importano i valori di default ma è possibile sovrascriverli se necessario
     - Template Interni


**Rubrica telefonica**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Mostra nella rubrica locale
     - Abilita o disabilita la visualizzazione dell’interno nella rubrica degli interni
     - Si / No
   * - Modalità di pubblicazione LDAP
     - Indica la modalità di pubblicazione dell’interno in LDAP tra le varie opzioni disponibili. La regola di pubblicazione LDAP generale è definita nel pannello Impostazioni LDAP
     - Disabilitato / Regola pubblicazione LDAP / Presentando il numero sottoindicato / Regola di pubblicazione LDAP applicata all'interno sottoindicato
   * - Interno LDAP personalizzato
     - Interno su cui viene applicata la regola di pubblicazione LDAP. Questo campo viene visualizzato solo se l’opzione Regola di pubblicazione LDAP applicata all’interno sottoindicato è selezionata
     - Numerico
   * - Numero LDAP personalizzato
     - Numero telefonico associato all’utente nella rubrica LDAP. Questo campo viene visualizzato solo se l’opzione Presentando il numero sottoindicato è selezionata
     - Numerico
   * - Ente
     - Utilizzato nella pubblicazione in rubrica (corrisponde all’attributo organization nella pubblicazione sulla rubrica LDAP)
     - Alfa-numerico
   * - Reparto
     - Utilizzato nella pubblicazione in rubrica (corrisponde all'attributo organizationUnit nella pubblicazione sulla rubrica LDAP). E' il reparto di riferimento dell’interno
     - Alfa-numerico

**Classi di servizio**


.. list-table::  
   :widths: 25 25 50
   :header-rows: 1
   
   * - Parametro
     - Descrizione
     - Valore   
   * - Classe di instradamento in uscita standard
     - Indica la classe di instradamento associata all'utente quando il lucchetto elettronico è sbloccato. Nel caso in cui la modalità di sblocco del lucchetto elettronico sia impostata ad Aperto questa è la classe applicata a tutte le chiamate.
     - Classi di instradamento in uscita
   * - Classe di instradamento in uscita ristretta
     - Indica la classe di instradamento associata all’utente quando il lucchetto elettronico è bloccato. Nel caso in cui la modalità di sblocco del lucchetto elettronico sia impostata ad Aperto questa classe non viene mai utilizzata.
     - Classi di instradamento in uscita

**Limiti**


.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Limite chiamate contemporanee
     - Numero massimo di chiamate contemporanee (in ingresso e in uscita) su tutti gli account associati all'interno ammesse per l’interno. Impostare questo limite ad 1 impedisce all'interno di utilizzare servizi quali il trasferimento con offerta poiché la chiamata in attesa di essere trasferita risulta comunque come chiamata attiva.
     - Numerico (0 = nessun limite)
   * - Livello di occupato
     - Numero di chiamate su tutti gli account associati all'interno a partire dal quale l’utente viene considerato occupato (il PBX quindi non presenta la chiamata ai dispositivi ma risponde con il SIP Message 486 Busy Here). Impostare questo limite ad 1 nel caso di singolo account blocca le notifiche di chiamate in ingresso sul telefono anche se il Call Waiting è abilitato sull'apparato
     - Numerico (0 = nessun limite)
 
**Lucchetto elettronico**


.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Modalità di sblocco
     - Consente di scegliere la modalità di sblocco per l’interno. **Aperto** –> Il lucchetto elettronico è sempre sbloccato **Codice** –> Il lucchetto elettronico può essere sbloccato con il codice di sblocco definito nel piano di numerazione **Password** -> Il lucchetto elettronico può essere sbloccato utilizzando il codice di sblocco e digitando successivamente il PIN dei servizi per l’interno
     - Aperto / Codice / Password
   * - Politica di sblocco
     - Consente di scegliere la politica di sblocco per l’interno. **Per chiamata** –> Il lucchetto deve essere sbloccato prima di effettuare ogni chiamata **Blocca automaticamente dopo il numero di minuti sottoindicato** –> Il lucchetto viene bloccato automaticamente allo scadere dell’intervallo indicato **Sbloccato finché l’utente lo blocca nuovamente** –> Il lucchetto una volta sbloccato deve essere bloccato esplicitamente dall'utente
     - Per chiamata / Blocca automaticamente dopo il numero di minuti sottoindicato / Sbloccato finché l’utente lo blocca nuovamente
   * - Durata dello sblocco (sec.)
     - Tempo dopo il quale l’interno viene bloccato. Applicabile solo se la politica di sblocco è Blocca automaticamente dopo il numero di minuti sottoindicato      -
     - Numerico

**Prelievo di chiamata di gruppo**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Gruppi di appartenenza
     - Elenco dei gruppi autorizzati a prelevare le chiamate dirette all’interno (le chiamate dirette a questo interno possono essere prelevate da tutti gli interni con autorizzazione al prelievo su uno di questi gruppi).
     - Gruppo di prelievo
   * - Autorizzazione al prelievo
     - Elenco dei gruppi su cui l’interno è autorizzato a prelevare chiamate (l’interno può prelevare le chiamate dirette ad interni che hanno tra i gruppi di appartenenza un gruppo su cui l’interno è autorizzato al prelievo)
     - Gruppo di prelievo


**Trabocchi**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Interno
     - Azione di trabocco su chiamate provenienti da un interno (anche remoto)
     - 
   * - Esterno
     - Azione di trabocco sulle chiamate provenienti dall’esterno
     - 
   * - Trasferimento
     - Azione di trabocco sui trasferimenti di chiamata
     - 
   * - Timeout (sec.)
     - Tempo alla scadenza del quale viene eseguita l’azione di trabocco configurata in caso di nessuna risposta
     - Numerico
   * - Nessuna risposta
     - La chiamata è considerata senza risposta alla scadenza del timeout
     - Riaggancia / Selezione personalizzata / Chiedi selezione / Numero esterno / Interno / Gruppo / Coda / Controllo orario / IVR / Casella vocale / Stanza MeetMe
   * - Occupato
     - L’interno è considerato occupato se è stato raggiunto il Busy Level impostato per l’interno oppure se il terminale invia il SIP Response 486 Busy Here
     - Riaggancia / Selezione personalizzata / Chiedi selezione / Numero esterno / Interno / Gruppo / Coda / Controllo orario / IVR / Casella vocale / Stanza MeetMe
   * - Non disponibile
     - L’interno è considerato non disponibile se il terminale non è registrato o non è raggiungibile a livello IP oppure se il terminale invia il SIP Response 480 Temporarily Unavailable
     - Riaggancia / Selezione personalizzata / Chiedi selezione / Numero esterno / Interno / Gruppo / Coda / Controllo orario / IVR / Casella vocale / Stanza MeetMe
     
Configurazione Account
+++++
Nel pannello Account sono definite le credenziali SIP utilizzabili da un dispositivo per registrarsi ed effettuare / ricevere chiamate tramite il KalliopePBX. A queste credenziali sono associati attributi per incrementare la sicurezza e modifiche del comportamento del KalliopePBX in termini di segnalazione e flussi audio da associare ad uno specifico dispositivo. Questi attributi sono definiti a livello di account e non di interno perché due account associati allo stesso interno ma a dispositivi differenti possono avere requisiti differenti.

**Esempio**: ad un interno posso associare un account utilizzato su un telefono fisico ed uno utilizzato su un softphone. Mentre per il telefono fisico posso utilizzare codec con maggior consumo di banda ad es. G711a per il softphone che viene utilizzato ad esempio in telelavoro posso scegliere di utilizzare codec quali il G729 che ottimizzano l’utilizzo della banda.

Per configurare gli account basta aprire il menu operativo e cliccare su PBX > Interni e Account. Per creare un nuovo account procedere cliccando su "Account" nella barra in alto e successivamente su "Aggiungi Account SIP"

- **Abilitato**: Consente di disabilitare un account senza perderne la configurazione
- **KCTI Mobile App**: Consente di utilizzare questo account con l'app mobile KalliopeCTI abilitando l'invio dei messaggi push per la segnalazione delle chiamate
- **Nome utente**: Username utilizzato per l’autenticazione SIP del dispositivo || Alfa-numerico
- **Password**: Password utilizzata per l’autenticazione SIP del dispositivo || Alfa-numerico
- **Template dell'account**: Indica il template account contenente i parametri di default da utilizzare per la tipologia di interno prescelta
- **Abilita verifica di registrazione**: Quando questa opzione è abilitata il KalliopePBX verifica che la richiesta di setup di chiamata (SIP INVITE) provenga dallo stesso IP: porta da cui ha ricevuto la richiesta di registrazione (SIP REGISTER)
- **Indirizzo abilitato**: Indica l’indirizzo ip o la subnet da cui il KalliopePBX accetta richieste di registrazione e setup di chiamata
- **Maschera di sottorete abilitata**: Completa l’informazione della ACL su base IP per le richieste di registrazione e setup di chiamata
- **Abilita NAT**: Quando questa opzione è abilitata il KalliopePBX ignora gli indirizzi IP presenti negli header SIP e SDP e risponde sempre all'indirizzo IP e porta da cui ha ricevuto la richiesta . Questa opzione deve essere abilitata solo per dispositivi si trovano dietro un NAT rispetto al KalliopePBX e che non risolvono il problema dell’attraversamento NAT (tramite STUN / ICE / ALG SIP).
- **Abilita direct media**: Questa opzione consente di instaurare dei flussi audio tra 2 PBX che si trovano in condizioni di visibilità diretta (no NAT). Se questa funzione è abilitata i servizi che richiedono il monitoraggio del flusso RTP (ad es. registrazione chiamate, trasferimento di chiamata e parcheggio con codici di servizio del KalliopePBX) sono disabilitati.
- **Abilita SRTP**: Questa opzione consente di abilitare il supporto alla cifratura dei flussi RTP. Poiché lo scambio delle chiavi avviene all’interno dei messaggi SIP / SDP in plaintext è opportuno utilizzare SRTP insieme alla cifratura della segnalazione mediante TLS. (vedi Configurazione TLS/SRTP)

**Impostazioni di outbound proxy**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Indirizzo dell'outbound proxy
     - Consente di impostare l'indirizzo IP/hostname dell'outbound proxy da utilizzare
     - Alfa-numerico
   * - Porta dell'outbound proxy
     - Consente di impostare la porta dell'outbound proxy da utilizzare
     - Numerico
   * - Protocollo dell'outbound proxy
     - Consente di impostare il protocollo da utilizzare per comunicare con l'outbound proxy. È possibile impostare solamente protocolli abilitati nelle Impostazioni SIP
     - UDP / TCP / TLS / WS / WSS

**Impostazioni di trasporto**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Abilita trasporto UDP
     - Consente di abilitare il protocollo di trasporto UDP per la segnalazione SIP. Questa opzione non è presente se il trasporto UDP non è abilitato nelle Impostazioni SIP
     - Si / No
   * - Abilita trasporto TCP
     - Consente di abilitare il protocollo di trasporto TCP per la segnalazione SIP. Questa opzione non è presente se il trasporto TCP non è abilitato nelle Impostazioni SIP
     - Si / No
   * - Abilita trasporto TLS
     - Consente di abilitare il protocollo di trasporto TLS per la segnalazione SIP. Questa opzione non è presente se il trasporto TLS non è abilitato nelle Impostazioni SIP
     - Si / No
   * - Abilita trasporto Web Socket
     - Consente di abilitare il protocollo di trasporto Web Socket (HTTP) per la segnalazione SIP. Questa opzione non è presente se il trasporto Web Socket (HTTP) non è abilitato nelle Impostazioni SIP
     - Si / No
   * - Abilita trasporto Web Socket sicuro
     - Consente di abilitare il protocollo di trasporto Web Socket sicuro (HTTPS) per la segnalazione SIP. Questa opzione non è presente se il trasporto Web Socket sicuro (HTTPS) non è abilitato nelle Impostazioni SIP
     - Si / No

**Codec audio**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
     - Aggiungi codec
     - In questa sezione è possibile selezionare e ordinare i codec audio utilizzabili dall'account (e che quindi verranno inseriti nella media description del protocollo SDP)
     - PCM a-law / G.722 / G.726 / G.729 / GSM / Opus / PCM u-law

**Codec video**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Aggiungi codec
     - In questa sezione è possibile selezionare e ordinare i codec video utilizzabili dall'account (e che quindi verranno inseriti nella media description del protocollo SDP)
     - H.261 / H.263 / H.263+ / H.264 /VP8

**Interno**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Interno
     - In questa sezione è possibile selezionare l'interno al quale associare l'account SIP
     - Interno

Licenze
-----

*jpg*

La pagina licenze si divide in tre sezioni: Lista delle licenze, Recupera le licenze dal server e Lista delle licenze G.729.

Lista delle licenze
+++++

In questa sezione è mostrata una lista delle licenze già attivate con le seguenti informazioni:

- ID
- Chiave di attivazione
- Prodotto
- Data di attivazione
- Data di scadenza
- Canali

Cliccando su **Attiva nuova licenza** si accede ad una schermata dove è possibile introdurre la chiave di attivazione valida per il prodotto acquistato.

In questa sezione è possibile caricare le licenze relative a: Kalliope Multi-Tenant, KalliopeCTI Pro, KalliopeCTI Phone, Kalliope Attendant Console CTI, Kalliope Attendant Console Phone, Kalliope Call Center, Upgrade Mini to Lite.

Recupera le licenze dal server
+++++
Qui è possibile visualizzare quali licenze sono state attivate in precedenza su un determinato seriale.
Questa sezione si divide in:

- Licenze prodotto aggiornate sul server
- Licenze prodotto importabili automaticamente
- Licenze prodotto importabili manualmente


Lista delle licenze G729
+++++

*jpg*

Analogamente, la sezione dedicata alle licenze G729 mostra una lista delle licenze già attivate con le seguenti informazioni:

- Chiave di licenza
- Canali
- Data di scadenza
- Scarica

Cliccando su **Attiva nuova licenza G729** si accede alla procedura di attivazione delle licenze G729 divisa in tre fasi:

1. Inserimento della chiave di licenza G729
2. Accettazione delle condizioni d'uso
3. Inserimento dei dati personali

Una volta inserite le informazioni richieste è possibile cliccare sul pulsante Attiva per completare la procedura.





Descrizione interfaccia
=====




Configurazione servizi
=====

