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
   
   * - Template dell’interno
     - Indica il template contenente i parametri di default da utilizzare per la tipologia di interno prescelta. Tutti gli attributi successivamente presenti nel pannello importano i valori di default ma è possibile sovrascriverli se necessario
     - Template Interni


**Rubrica telefonica**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1
   
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
   
   * - Modalità di sblocco
     - Consente di scegliere la modalità di sblocco per l’interno.
       Aperto – Il lucchetto elettronico è sempre sbloccato
       Codice – Il lucchetto elettronico può essere sbloccato con il codice di sblocco definito nel piano di numerazione
       Password - Il lucchetto elettronico può essere sbloccato utilizzando il codice di sblocco e digitando successivamente il PIN dei servizi per l’interno
       - Aperto / Codice / Password
    * - Politica di sblocco
      - Consente di scegliere la politica di sblocco per l’interno.
Per chiamata – Il lucchetto deve essere sbloccato prima di effettuare ogni chiamata

Blocca automaticamente dopo il numero di minuti sottoindicato – Il lucchetto viene bloccato automaticamente allo scadere dell’intervallo indicato

Sbloccato finché l’utente lo blocca nuovamente – Il lucchetto una volta sbloccato deve essere bloccato esplicitamente dall'utente
      - Per chiamata / Blocca automaticamente dopo il numero di minuti sottoindicato /
Sbloccato finché l’utente lo blocca nuovamente
    * - Durata dello sblocco (sec.)
      - Tempo dopo il quale l’interno viene bloccato. Applicabile solo se la politica di sblocco è Blocca automaticamente dopo il numero di minuti sottoindicato
      - Numerico

**Prelievo di chiamata di gruppo**





Descrizione interfaccia
------------




Configurazione servizi
------------


