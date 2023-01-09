Altri servizi 
====

Alta affidabilità
-------------

Descrizione del Servizio
+++++++++
L’alta affidabilità ha l’obiettivo di incrementare la robustezza del sistema VoIP mettendo insieme due nodi fisici o due macchine virtuali che lavorano congiuntamente in modo attivo/passivo. Solo uno dei due PBX in un certo istante è operativo e serve le chiamate, mentre l’altro è in standby ed è pronto ad acquisire il servizio delle chiamate nel momento in cui il nodo passivo fallisce. Nell’operazione di trasferimento delle risorse da un nodo all’altro non c’è mantenimento delle chiamate in corso. Per design, il failure che un sistema ad alta affidabilità intende gestire, è un completo arresto delle funzionalità del nodo attivo in quel momento:

- nativamente non esiste il caso di monitoraggio di un servizio se esso non è operativo, come invece accade in altri meccanismi di ridondanza in cui si considera degradato il nodo, anche se uno dei servizi non è operativo
- possono accadere spiacevoli episodi se i 2 nodi che fanno parte del cluster perdono la loro vista reciproca, perché ognuno di loro è convinto di essere l’unico e quindi si attiva, causando una situazione di "split brain"
Il pannello dell’Alta affidabilità è disponibile solo all’admin o nel caso di macchina Multitenant, al PBX Admin.

Configurazione del servizio
+++++++++++
Si procede andando su Impostazioni > Stato alta affidabilità Ci troviamo così nella pagina della **Configurazione dell’alta affidabilità**.

È possibile cambiare lo stato del sistema come “Abilitato come coordinatore” o “Abilitato”. Per esempio, possiamo scegliere “Abilitato come coordinatore” per un nodo da tenere come coordinatore e selezionare (tramite un’altra scheda browser) un altro nodo semplicemente come “Abilitato”, che farà da secondario e riceverà la configurazione dall’altro nodo.

Impostazioni di rete
++++++++++

*jpg*
Per una configurazione completa, è necessario andare su impostazioni > impostazioni di rete e controllare che siano configurate due interfacce di rete per l’alta affidabilità con ognuna il proprio indirizzo IP. Le due interfacce sono connesse allo stesso virtual switch che non ha interfacciamento con il pubblico. Ha un unico DNS configurato e una rotta.

Configurazione dell’alta affidabilità
++++++++
Configurazione del servizio (Abilitato come coordinatore)

- **S/N nodo remoto**: è il serial number, serve perché la prima comunicazione tra le due centrali (nodo coordinatore e secondario) viene fatta con una sessione SSH interattiva, in cui viene chiesta l’autenticazione con user e password. La password è calcolata dal serial number della macchina. Quindi il nodo coordinatore ha bisogno di sapere il serial number dell’altro nodo per poter ottenere la password con cui connettersi e fornire i comandi necessari
- **Abilitato**: posso scegliere quale servizio configurare su una o entrambe
- **Interfaccia**: è possibile visualizzare tutte le interfacce di rete presenti sulla macchina
- **Indirizzo IP locale**: è possibile visualizzare qual è l’indirizzo IP locale
- **Indirizzo IP remoto**: è possibile visualizzare qual è l’indirizzo IP remoto
- **Indirizzo IP risorsa**: è l’indirizzo IP che verrà acquisito e condiviso su una determinata interfaccia
- **Gruppo di ping**: si possono inserire gli indirizzi IP separati da spazi e saranno quei nodi che ciascuno dei due pingerà periodicamente per verificare chi dei due ne vede di più
- **Interfaccia di sincronizzazione**: definisco una interfaccia scelta che sarà utilizzata per la sincronizzazione dei dati e nei registri tra i due nodi (es. eth1)
- **Nodo attivo predefinito**: si sceglie quale dei due nodi deve acquisire la risorsa di default in caso di indecisione.

Impostazioni avanzate
++++++

- **Timeout keepalive – soglia warning (sec.)**: è una soglia dopo la quale viene generato un warning (al momento solo nei log)
- **Timeout keepalive – fuori servizio (sec.)**: questo valore definisce dopo quanto tempo di mancata comunicazione con il nodo si deve assumere che sia inattivo e quindi se è possibile che l’altro nodo faccia l’acquisizione delle risorse
- **Timeout inizializzazione (sec.)**: valore che garantisce un tot di secondi prima di decidere di acquisire le risorse (nel caso ci sia un nodo già attivo). Più alto è il valore, più tempo impiegherà la macchina all’avvio per diventare operativa perché entrambi i nodi aspettano questo tempo

Premendo “Salva e avvia il servizio” viene scritto nel database il setting e viene avviata l’alta affidabilità.


Stato alta affidabilità
+++++++++

Dopo il salvataggio della configurazione, ci troviamo nella pagina dello Stato alta affidabilità in cui possiamo visionare:

- I nodi con i rispettivi serial number e IP di sincronizzazione
- Lo stato del cluster con l’abilitazione del servizio, lo stato del pairing, lo stato del servizio, l’heartbeat
- Lo stato delle risorse con il nodo attivo
- Lo Stato del cluster - opzione “pair”: si aggancia il nodo secondario e potremo vedere il pannello di stato in modalità passiva:


Stato alta affidabilità nodo passivo
++++++++++
- **Sgancia nodo**: si disabilita l’alta affidabilità, si lascia quindi il cluster degradato e la risorsa in esercizio sul nodo attivo
- **Commuta nodo attivo**: forzare l’acquisizione delle risorse
Stato alta affidabilità nodo attivo
- **Disabilita alta affidabilità**: la spegne su entrambi i nodi
- **Sgancia nodo passivo**
- **Commuta nodo attivo**: forzare la commutazione delle risorse sull’altro nodo


Attività pianificate
---------

Gestione attività pianificate
++++++++
Tramite questo servizio (disponibile a partire dal firmware 4.5.8) è possibile definire delle attività che verranno eseguite automaticamente da KalliopePBX secondo una politica di pianificazione definita dall’utente.
Le tipologie di attività definibili sono le seguenti:

- Invio CDR Call Center
- Invio CDR (disponibile a partire dal firmware 4.7.0)


Definizione di una nuova attività pianificata
+++++++++
Il pannello per la definizione delle attività pianificate è raggiungibile attraverso il seguente percorso: menù Operativo → monitoraggio → attività pianificate.
Per aggiungere una nuova attività pianificata fare click sulla voce “Pianifica nuova attività” Nuova attivita call center.png in alto a sinistra del pannello, dopo aver selezionato dal relativo menu a tendina la tipologia di attività che si vuole pianificare.

Come creare una nuova attività pianificata di invio CDR Call Center
+++++++++

.. note::

   La possibilità di poter definire attività pianificate di tipo “Invio CDR Call Center” è vincolata alla presenza della licenza Call Center sul PBX.

Dopo aver selezionato dal menu a tendina la voce “Invio CDR Call Center” e fatto click sulla voce “Pianifica nuova attività”, comparirà un form come quello rappresentato di seguito.

I parametri da configurare sono i seguenti:

**Impostazioni generali**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Nome
     - Il nome da assegnare all’attività pianificata. Il nome inserito comparirà nell’oggetto e corpo delle mail inviate al termine dell’esecuzione dell’attività
     - Alfa-numerico
  * - Abilitato
    - Abilitare o disabilitare l'esecuzione dell'attività pianificata. Le attività pianificate disabilitate possono essere eseguite solo manualmente
    - Si / No
  * - Tipo di pianificazione
    - Selezionare il periodo di esecuzione automatica dell'attività pianificata
    - Giornaliera / Settimanale / Mensile
  * -  Orario di pianificazione
    - Permette di indicare l'orario in cui ogni giorno l'attività pianificata sarà eseguita ed il risultato inviato via email ai destinatari impostati
    - Ora e minuti
  * - Giorno della settimana
    - Disponibile solo nel caso in cui il tipo di pianificazione sia "Settimanale". Permette di indicare il giorno della settimana nel quale l'attività pianificata sarà eseguita (all'ora impostata) ed il risultato inviato via email ai destinatari impostati
    - Giorno della settimana
  * - Giorno del mese
    - Disponibile solo nel caso in cui il tipo di pianificazione sia "Mensile". Permette di indicare il giorno del mese nel quale l'attività pianificata sarà eseguita (all'ora impostata) ed il risultato inviato via email ai destinatari impostati
    - Data

**Impostazioni dell'Invio CDR Call Center**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Intervallo
     - Selezionare l'intervallo di tempo sulla base del quale si desidera esportare il CDR Call Center
     - Giorno corrente / Giorno precedente / Settimana corrente / Settimana precedente / Mese corrente / Mese precedente
   * - Formato del file
     - Selezionare il formato del file nel quale il CDR Call Center deve essere esportato	
     - XLSX / XLSX (dettagliato) / CSV / CSV (dettagliato) / JSON / XML
   * - Esporta eventi operatore
     - Se selezionato aggiunge al CDR Call Center esportato tutti gli eventi degli operatori. Questa impostazione è selezionabile solamente se si è scelto un formato di file di tipo "dettagliato".
     - Si / No
   * - Comprimi se la dimensione supera questo valore in MB (0 = comprimi sempre)
     - Indicare una dimensione massima accettabile (in MB) del file generato dal processo di esportazione CDR Call Center, superata la quale il file verrà compresso in formato zip prima di allegarlo alla email. Se si indica il valore 0 il file viene compresso sempre, indipendentemente dalla sua dimensione.
     - Numerico
   * - Notifica a tutti i supervisori
     - Indicare se il CDR Call Center esportato debba essere inviato per email a tutti gli utenti che abbiano assegnato il ruolo di supervisore ed abbiano un indirizzo email configurato
     - Si / No
   * - Destinatari
     - In congiunzione o in alternativa alla notifica ai supervisori, è possibile specificare un numero arbitrario di destinatari ai quali inviare il CDR Call Center esportato
     - Alfanumerico

.. note::

   Deve essere sempre presente almeno un destinatario oppure deve essere selezionata la notifica ai supervisori, altrimenti il form mostra un opportuno messaggio di errore e la definizione dell'attività pianificata non potrà essere salvata.
   

Come creare una nuova attività pianificata di invio CDR
+++++++
Dopo aver selezionato dal menu a tendina la voce “Invio CDR” e fatto click sulla voce “Pianifica nuova attività”, comparirà un form come quello rappresentato di seguito.

I parametri da configurare sono i seguenti:

**Impostazioni generali**

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Nome
     - Il nome da assegnare all’attività pianificata. Il nome inserito comparirà nell’oggetto e corpo delle mail inviate al termine dell’esecuzione dell’attività
     - Alfa-numerico
   * - Abilitato
     - Abilitare o disabilitare l'esecuzione dell'attività pianificata. Le attività pianificate disabilitate possono essere eseguite solo manualmente
     - Si / No
   * - Tipo di pianificazione
     - Selezionare il periodo di esecuzione automatica dell'attività pianificata
     - Giornaliera / Settimanale / Mensile
   * - Orario di pianificazione
     - Permette di indicare l'orario in cui ogni giorno l'attività pianificata sarà eseguita ed il risultato inviato via email ai destinatari impostati
     - Ora e minuti
   * - Giorno della settimana
     - Disponibile solo nel caso in cui il tipo di pianificazione sia "Settimanale". Permette di indicare il giorno della settimana nel quale l'attività pianificata sarà eseguita (all'ora impostata) ed il risultato inviato via email ai destinatari impostati
     - Giorno della settimana
   * - Giorno del mese
     - Disponibile solo nel caso in cui il tipo di pianificazione sia "Mensile". Permette di indicare il giorno del mese nel quale l'attività pianificata sarà eseguita (all'ora impostata) ed il risultato inviato via email ai destinatari impostati
     - Data
     
 **Impostazioni dell'Invio CDR**
 
.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Intervallo
   - Selezionare l'intervallo di tempo sulla base del quale si desidera esportare il CDR
   - Giorno corrente / Giorno precedente / Settimana corrente / Settimana precedente / Mese corrente / Mese precedente
 * - Formato del file
   - Selezionare il formato del file nel quale il CDR deve essere esportato
   - XLSX / XLSX (dettagliato) / CSV / CSV (dettagliato) / JSON / XML
 * - Comprimi se la dimensione supera questo valore in MB (0 = comprimi sempre)
   - Indicare una dimensione massima accettabile (in MB) del file generato dal processo di esportazione CDR, superata la quale il file verrà compresso in formato zip prima di allegarlo alla email. Se si indica il valore 0 il file viene compresso sempre, indipendentemente dalla sua dimensione.
   - Numerico
 * - Destinatari
   - È possibile specificare un numero arbitrario di destinatari ai quali inviare il CDR esportato, deve però essere sempre presente almeno un destinatario
   - Alfanumerico
   
Esecuzione manuale delle attività pianificate
+++++++

Tra le azioni disponibili per le attività pianificate definiti c'è la possibilità di eseguirle su richiesta senza dover attendere la pianificazione impostata. Per avviare l'attività in background basta fare click sul pulsante con il simbolo Play.png.

Al termine della richiesta si viene avvisati con un messaggio che la generazione del report è stata avviata.


Audit Log
---------

Descrizione del servizio
+++++++++
L’Audit Log è un registro che contiene tutte le modifiche da configurazione eseguite, marcate con l’utente che ha effettuato la modifica.

Le modifiche non sono immediatamente irreversibili, ma è possibile visualizzare che cosa è stato modificato e, in caso, andare a ripristinarlo.

Conoscere l’utente che ha effettuato le modifiche è importante, l’utente “admin” non è l’unico in grado di eseguire modifiche alla configurazione, ma si possono creare ruoli personalizzabili e assegnare degli utenti a questi specifici ruoli. In questo modo si delega parte della configurazione della centrale a del personale del cliente. Quindi tutte le modifiche effettuate dal cliente saranno marcate con il nome utente a lui assegnato. Clicca sul link di seguito per un approfondimento sugli utenti e ruoli.

*jpg*

Per raggiungere il servizio basta seguire il percorso del menu "Registri > Audit Log".

L’Audit Log contiene i registri delle modifiche ordinati per mese ed è possibile esportare il registro in vari formati: XLSX, CSV, JSON, XML.
È presente il filtro “Seleziona colonne visualizzate” per mirare la ricerca a specifiche sezioni presenti.

Infatti, l’Audit Log permette di visualizzare:

- **Id di transazione**
- **Giorno del mese**: è possibile selezionare una data specifica
- **Timestamp**
- **Nome utente**: nome dell’utente che ha effettuato la modifica
- **Indirizzo IP**
- **Azione**
- **Tipo oggetto**
- **Descrizione**















