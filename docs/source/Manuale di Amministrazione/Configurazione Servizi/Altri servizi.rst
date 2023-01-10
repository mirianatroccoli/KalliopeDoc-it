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


Auto-Provisioning
------------

Descrizione del servizio
+++++++
Il servizio Auto Provisioning consente di generare e trasferire sui telefoni il file di configurazione necessario al corretto funzionamento del dispositivo. Questo file contiene anche le informazioni relative allo specifico account / interno associato al telefono stesso.

Configurazione del servizio
+++++++
In questa sezione sono raccolte tutte le configurazioni necessarie ad effettuare l’auto-provisioning di un dispositivo telefonico.
È inoltre possibile consultare l'elenco dispositivi built-in per l'auto-provisioning

Lista dei dispositivi
+++++++++

Questo pannello contiene l’elenco di tutti i dispositivi per cui è stata configurata la generazione del file di provisioning associato.
Per ogni dispositivo è possibile configurare i parametri riportati nella seguente tabella.

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Abilitato
   - Consente di disabilitare la generazione del file di provisioning associato al dispositivo
   - Si / No

**Modello del dispositivo**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Marca
   - Elenco dei produttori per cui è stato definito almeno un modello di dispositivo
   - Marca
 * - Modello
   - Elenco dei dispositivi associati al produttore selezionato
   - Modello
 * - Template
   - Elenco dei template associati al modello selezionato
   - Template


**Redirection Server**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Redirection Server per il provisioning
   - Elenco dei redirection server definiti per il produttore selezionato
   - Redirection Server
 * - Provisionato sul redirection server
   - Campo in sola lettura indica se il provisiong sul redirection server è stato effettuato con successo
   - Si / No


**Configurazione del dispositivo**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Indirizzo MAC
   - Indirizzo MAC del dispositivo (sono accettati i formati AABBCCDDEEFF, AA:BB:CC:DD:EE:FF, AA-BB-CC-DD-EE-FF)
   - MAC Address
 * - Note
   - Campo libero contenente annotazioni sul dispositivo
   - Stringa
 * - Abilita DHCP
   - Imposta il valore del placeholder %%IPADDRMODE%% ad on / off per questo dispositivo. Il placeholder potrà essere utilizzato nel template per generare il file di configurazione con la con le impostazioni di rete richieste.
   - Si / No
 * - Indirizzo IP
   - Imposta il valore del placeholder %%IPADDR%% per questo dispositivo. Il placeholder potrà essere utilizzato nel template per generare il file di configurazione con le impostazioni di rete richieste.
   - IP Address
 * - Maschera di sottorete
   - Imposta il valore del placeholder %%IPNETMASK%% per questo dispositivo. Il placeholder potrà essere utilizzato nel template per generare il file di con le impostazioni di rete richieste.
   - Subnet Mask
 * - Gateway
   - Imposta il valore del placeholder %%IPGATEWAY%% per questo dispositivo. Il placeholder potrà essere utilizzato nel template per generare il file di configurazione con le impostazioni di rete richieste.
   - IP Address
 * - DNS1
   - Imposta il valore del placeholder %%IPDNS1%% per questo dispositivo. Il placeholder potrà essere utilizzato nel template per generare il file di configurazione con le impostazioni di rete richieste.
   - IP Address
 * - DNS2
   - Imposta il valore del placeholder %%IPDNS2%% per questo dispositivo. Il placeholder potrà essere utilizzato nel template per generare il file di configurazione con le impostazioni di rete richieste.
   - IP Address
 * - Nome utente
   - Imposta il valore del placeholder %%PHONEUSERNAME%% per questo dispositivo. Il placeholder potrà essere utilizzato nel template per impostare le credenziali di accesso al telefono. Questo stesso valore sarà utilizzato da KalliopePBX per il pilotaggio del telefono quando viene associato al dispositivo un applicativo KalliopeCTI PRO.
   - Stringa
 * - Password
   - Imposta il valore del placeholder %%PHONEPASSWORD%% per questo dispositivo. Il placeholder potrà essere utilizzato nel template per impostare le credenziali di accesso al telefono. Questo stesso valore sarà utilizzato da KalliopePBX per il pilotaggio del telefono quando viene associato al dispositivo un applicativo KalliopeCTI PRO.
   - Stringa

**Controllo remoto**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Indirizzo
   - Se definito, specifica l'indirizzo IP a cui è raggiungibile (da parte del PBX) l'interfaccia web del telefono (in HTTP) al fine di poterne effettuare il controllo remoto (tramite l'applicativo KalliopeCTI Pro). Se vuoto, il PBX utilizzerà l'indirizzo IP da cui l'account associato a questo device è registrato a livello SIP
   - Indirizzo IP
 * - Porta
   - Come il campo precedente, ma relativo alla porta su cui l'interfaccia web del telefono è visibile da parte del PBX.
   - Intero (range 1-65535)

**Utilizzatore del dispositivo**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Account
   - Account e corrispondente interno associati al dispositivo (i placeholder dinamici sono calcolati a partire da questa associazione). Se non viene associato l’account il file di configurazione non viene generato e il dispositivo è inserito come Disabilitato.
   - Account

**Lista dei template**

Questo pannello contiene l’elenco di tutti i template definiti sul KPBX.
E’ obbligatorio definire un template per ogni modello di telefono per cui si desidera generare un file di provisioning.

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Nome
   - Nome del template
   - Stringa
 * - Marca del dispositivo
   - Elenco dei produttori per cui è stato definito almeno un modello di dispositivo
   - Marca
 * - Modello del dispositivo
   - Elenco dei dispositivi associati al produttore selezionato
   - Modello
   
**Contenuto del template**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Template
   - Questo campo libero deve contenere il template da utilizzare per la generazione del file di provisioning
   - Testo

Lista dei modelli di dispositivo
+++++++++

Questo pannello contiene l’elenco di tutti i modelli di dispositivo definiti sul KPBX. Alcuni modelli di dispositivo sono distribuiti con il firmware del KPBX. Altri modelli possono essere aggiunti dall’utente per generare file di configurazione per modelli/produttori non esplicitamente supportati.

E’ inoltre possibile definire delle regole che consentono di creare dei file di provisioning con nomi arbitrari. Il nome del file può essere composto da un prefisso, indirizzo MAC (in diversi formati) e un suffisso.

Per ogni modello di dispositivo è possibile definire i parametri riportati nella seguente tabella.

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Nome
   - Nome del modello di dispositivo
   - Stringa
   
   
**Marca del dispositivo**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Scegli Marca
   - Consente di selezionare una marca esistente o crearne una nuova selezionando la voce Nuova Marca
   - Marca
 * - Nome Marca
   - Nel caso di Nuova Marca contiene il nome da associare
   - Stringa
 * - Nome
   - Nome del modello di dispositivo
   - Stringa
   
**Regola di generazione del nome del file di provisioning**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Scegli regola
   - Consente di selezionare una regola esistente o crearne una nuova selezionando la voce Nuova Regola
   - Marca
 * - Nome regola
   - Nel caso di Nuova Regola contiene il nome da associare
   - Stringa
 * - Prefisso
   - Prefisso da aggiungere al nome file
   - Stringa
 * - Formato indirizzo MAC
   - Consente di selezionare il formato del MAC address da inserire nel nome file da una lista
   - Formato MAC Address
 * - Suffisso
   - Suffisso da aggiungere al nome file
   - Stringa
   
   
Lista dei placeholder personalizzati
++++++++++++++

Questo pannello contiene l’elenco di tutti i placeholder definiti dall’utente sul KPBX in aggiunti a quelli presenti di default. I placeholder custom hanno un formato del tipo %%_PLACEHOLDER%% e possono essere utilizzati all’interno dei template.
E’ possibile definire due tipi di placeholder:

- Statico: viene utilizzato per non modificare tutti i template in cui viene utilizzato uno specifico valore.
- Dinamico: viene utilizzato per aggiornare dinamicamente alcuni valori associati al KPBX e non allo specifico utente. In questo momento gli unici placeholder dinamici disponibili sono quelli relativi agli IP address associati alle diverse interfacce di rete / VLAN.
  
.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Placeholder
   - Identificativo del placeholder. Il placeholder da utilizzare è %%_PLACEHOLDER%%
   - Stringa
 * - Tipo
   - Consente di definire il tipo di placeholder
   - Statico/dinamico
 * - Valore
   - Nel caso di placeholder statico viene inserito il valore da sostituire in generazione, nel caso di placeholder dinamico l’attributo del KPBX da utilizzare per la sostituzione.
   - Stringa / Attributo KPBX
   
Lista dei redirection server
++++++

Questo pannello contiene l’elenco di tutti i redirection server configurati dall’utente sul KPBX. Attualmente è supportata l’integrazione con i redirection server dei seguenti produttori:

- SNOM (https://sraps.snom.com/)
- Yealink (https://ymcs.yealink.com/)

.. note::

   In virtù di alcune limitazioni delle API messe a disposizione da Yealink / Escene la procedura di configurazione è differente nel caso di utilizzo del redirection server SNOM rispetto a quello degli altri due produttori. In particolare, nel caso di Yealink / Escene è necessario definire preventivamente un server accedendo alla WEB GUI di gestione del servizio RPS. Il nome di questo server verrà riferito in fase di configurazione del redirection server.

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Marca del dispositivo
   - Marca del dispositivo per cui si sta definendo il redirection server
   - Snom / Yealink / Escene
   
   
**Credenziali**

.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Username
   - Utente per l’autenticazione sul server RPS del produttore
   - Stringa
 * - Password
   - Password per l’autenticazione sul server RPS del produttore
   - Stringa

**Impostazioni**
  
.. list-table::  
 :widths: 25 25 50
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Abilitato
   - Consente di disabilitare il redirection server senza perderne la configurazione
   - Si / No
 * - Nome
   - Nome del redirection server da creare (se SNOM) o da utilizzare (nel caso Yealink / Escene)
   - Stringa
 * - Indirizzo di provisioning
   - Nel caso SNOM URL a cui viene effettuata la redirezione (ad es. https://192.168.0.100/provisioning/ )
   - Stringa
   
   
   
   
Template
+++++++
La generazione del file di configurazione per uno specifico dispositivo viene effettuata a partire da un template associato alla marca/modello di telefono che si intende utilizzare.
Il formato del template dipende dalla marca/modello del telefono utilizzato ma anche eventualmente dalla versione del firmware installata sul dispositivo.
Nella definizione del template è possibile utilizzare dei placeholder che il KalliopePBX sostituirà automaticamente in fase di generazione del file.
Questi placeholder includono:

- Attributi del KalliopePBX (ad es. porta SIP UDP/TCP del centralino)
- Attributi dell’account/interno associato al telefono (ad es. credenziali SIP, nome, cognome, etc.)
- Attributi del telefono (ad es. parametri di rete, credenziali di accesso, etc.)

Una volta definito il template è necessario specificare il MAC address del dispositivo per il quale si intende generare il file di configurazione e l’account/interno da associare al dispositivo.
I file generati devono quindi essere trasferiti ai telefoni. Il KalliopePBX mette a disposizione i seguenti protocolli per il trasferimento dei file:

- **TFTP**: i file sono disponibili direttamente nella root del TFTP server nel caso di KalliopePBX monotenant. Nel caso di KalliopePBX multitenant deve essere aggiunto al path il Tenant UUID (link) (ad es. un possibile comando potrebbe essere get <tenant_uuid>/snom370-0004167898B1.htm.)
- **HTTP / HTTPS**: i file sono pubblicati al seguente URL http(s)://<ip_address>/provisioning/ nel caso di KalliopePBX monotenant. Nel caso di KalliopePBX multitenant deve essere aggiunto al path il Tenant UUID (link) (http(s)://<ip_address>/provisioning/<tenant_uuid>/)

Tutti i file generati sono visualizzabili anche nel Gestore File.
Per indicare al telefono quale protocollo deve essere utilizzato per scaricare il file di configurazione oltre all’indirizzo IP (ed eventuale path) del server di provisioning esistono diverse modalità la cui configurazione e ordine di esecuzione dipende dal modello di telefono utilizzato. Le modalità comunemente disponibili sono le seguenti:

- **SIP PnP**: il telefono all’avvio invia un messaggio SIP SUBSCRIBE ad un indirizzo multicast. Se sul KalliopePBX il servizio SIP PnP è abilitato il PBX risponde con una SIP NOTIFY contenente l’IP address del TFTP server da utilizzare. Questa modalità non è utilizzabile nel caso di KalliopePBX multitenant.
- **Redirection Server**: il telefono all’avvio prova a contattare il Redirection Server del produttore. Se il MAC Address del telefono è stato inserito il telefono viene rediretto al server indicato per il download del file di configurazione. In questa modalità è possibile utilizzare uno qualsiasi dei protocolli disponibili (in base al parametro configurato sul redirection server).
- **DHCP OPTION 66**: nel caso in cui in fase di assegnazione dell’indirizzo IP il DHCP Server comunichi al telefono anche la DHCP Option 66 contenente l’URL da contattare (incluso il protocollo da utilizzare), il telefono utilizzerà questa informazione per effettuare il download del file di configurazione.
- **Manuale**: è possibile avviare la configurazione anche manualmente dal telefono o dalla WEB GUI inserendo il protocollo da utilizzare e l’IP address (oltre eventualmente al path).

   
Cattura
-------

Il tool di cattura permette di acquisire le tracce dei pacchetti in ingresso / uscita dalle interfacce di rete di KalliopePBX applicando, eventualmente, un filtro di selezione basato su:

- Tipo di protocollo (tutti o una combinazione di ICMP/UDP/TCP)
- Indirizzo IP (sorgente o destinatario)
- Porta sorgente o di destinazione

Una volta impostati i filtri desiderati, è sufficiente cliccare sul pulsante Inizia la cattura. Il pulsante Termina la cattura permette di interrompere la cattura che, in ogni caso, si arresta automaticamente al raggiungimento di un file di dimensione pari a 10 MB.

Al termine della cattura, è possibile scaricare il file pcap sul proprio PC cliccando sul pulsante Scarica oppure eliminarlo cliccando sul pulsante Elimina. Avviando una nuova cattura, questa va a sovrascrivere quella precedente. Anche il riavvio del PBX provoca la cancellazione del file pcap.


Chiamate attive
---------

Descrizione del servizio
+++++++
Il sottomenu “chiamate attive” del servizio di Monitoraggio è raggiungibile cliccando su "Monitoraggio > Chiamate attive", come mostrato nell'immagine a destra.

La pagina mostra il pannello dove è disponibile la lista delle chiamate attive, filtrata in base a:

.. list-table::  
 :widths: 25 25
 :header-rows: 1

 * - Sorgente
   - Destinazione
 * - Linked ID	
   - 
 * - Canale
   - Canale
 * - Stato
   - Stato
 * - ID chiamante
   - ID del chiamato
 * - Nome chiamante
   - Nome del chiamato
 * - Numero chiamato	
   - 
 * - Data di creazione
   - Data di creazione
 * - Tempo di attività
   - Tempo di attività
 * - Data di connessione
   - Data di connessione
 * - Tempo di attività dalla connessione
   - Tempo di attività dalla connessione
 
   
Eventi PBX
--------

Descrizione del servizio
++++++++++++

Nella pagina degli Eventi PBX sono visualizzate tutte le notifiche relative agli eventi che si verificano al momento dell’accesso alla centrale.

Per raggiungere il servizio basta seguire il percorso "Registri > Eventi PBX". È possibile visualizzare, per ogni evento:

- ID
- Tipo evento
- Giorno del mese
- Timestamp
- Severity
- Parametri

È inoltre possibile esportare i dati nei seguenti formati:

- XLSX
- CSV
- JSON
- XML

 
Gestione dei filesystem remoti
-------

Descrizione del servizio
+++++++++++
Per raggiungere il servizio basta seguire il percorso "Impostazioni di sistema > Gestione dei filesystem remoti".

Nella seguente pagina è contenuta la lista dei filesystem remoti, ovvero i file contenuti su un eventuale computer remoto.

Configurazione del servizio
+++++++++
Per aggiungere un filesystem, premere su “Aggiungi nuovo filesystem remoto” La configurazione del nuovo filesystem consente di inserire:

- Protocollo (CIFS/NFS)
- Nome
- Indirizzo del server
- Condivisione
- Nome utente
- Password

   
Gestione dei tenant
---------

Descrizione del servizio
+++++++++
Nella pagina di gestione dei tenant è possibile visualizzare la lista dei tenant e dei gruppi di tenant.

Configurazione del servizio
++++++++

Per raggiungere il servizio di “Gestione dei tenant” basta cliccare su “Impostazioni di sistema > Gestione dei tenant”.
Sbloccando il lucchetto in alto a destra per entrare in modalità di modifica, è possibile creare un nuovo tenant.


Lista dei tenant
+++++++++
Per creare un nuovo tenant è necessario cliccare su “Crea nuovo tenant”. Sono presenti i seguenti campi da compilare e/o selezionare:

- **Modalità operativa**: può essere completa (può fare e ricevere chiamate), limitata con blocco chiamate uscenti (impedisce di effettuare chiamate in uscita, ad eccezione delle chiamate ai numeri della whitelist) e disabilitata (viene inibito il funzionamento di quel determinato tenant).
- **Nome**
- **Dominio**: nome del dominio che funge da componente degli username dopo la “@” (es. admin@dominio)
- **Password**: dell’admin di tenant che si può inizializzare alla creazione del tenant
- **Url del logo personalizzato**: è possibile far in modo che quando un utente del tenant entra nell'interfaccia web della centrale, veda un logo personalizzato in alto a sinistra.
- **Email del referente**: email del referente per l’invio della notifica di creazione del tenant
- **Gruppo di tenant (default group / nuovo gruppo)**: è utile per raggruppare più tenant amministrativamente distinti (ciascuno con il proprio admin) in una confederazione.

La configurazione dei gruppi di tenant è spiegata al paragrafo successivo.

- **Prefisso degli account SIP**: assicurazione dell’univocità degli account SIP, ovvero tutti gli account SIP di un determinato tenant avranno lo stesso prefisso.

Infatti, per evitare che ci possa essere una collisione, cioè che due admin di tenant creino lo stesso account SIP, a ciascun tenant viene assegnato un prefisso (una stringa alfanumerica di 6 caratteri) in modo che tutti gli account SIP di un certo tenant condividano lo stesso prefix. I caratteri del prefisso vengono generati casualmente, ma è possibile personalizzarli.

**N.B.** Questa è la differenza principale che c’è tra tenant di default (quello che si trova preimpostato sulla centrale) e gli altri. Infatti il primo, che nasce da una macchina monotenant, possiede gli account che mancano di prefix.

Es. Se si possiede un account x, definito nel tenant di default, per continuare a utilizzarlo, si riconfigura il telefono per assegnare un prefisso al tenant default oppure si corre il rischio di tenere l'account senza prefix.

- **Numero massimo di account** (-1 è illimitato)
- **Numero massimo di interni** (-1 è illimitato)
- **Limite chiamate contemporanee** (-1 è illimitato): interessa il limite di chiamate esterne
- **Quota di archiviazione locale** (in MB): quota di storage interno alla macchina che può essere usata dal tenant per registrare file audio custom o messaggi della segreteria telefonica
- **Provisioning fallback abilitato**

Una volta configurato è possibile accedere al proprio tenant di cui si è amministratori.

Lista dei gruppi di tenant
++++++++
In questa sezione è possibile creare un nuovo gruppo di tenant o modificarlo. Il gruppo di tenant serve quindi per raggruppare più tenant di più virtual pbx – amministrativamente distinti – in un gruppo. Quindi è possibile, dopo averli messi nello stesso gruppo, fare una condivisione del piano di numerazione e fare in modo che i tenant comunichino direttamente tra interni.

- **Nome**: nome del gruppo di tenant
- **I tenant in questo gruppo condividono le sezioni**: opzione spuntabile o meno
- **Tenant appartenenti a questo gruppo**: elenco dei tenant che appartengono a quel determinato gruppo.

Interni remoti
+++++++++
Nel piano di numerazione le selezioni impostate che sono servite dal tenant selezionato vengono definite sotto alla sezione “interni remoti”.

- **Tipo di selezione** (selezione esatta, intervallo di selezione, selezione a prefisso)
- **Valore della selezione**
- **Tipo di destinazione**
- **Valore della destinazione**


Gestione delle sedi
------

Descrizione del servizio
+++++++++
Le sedi possono essere configurate a livello di PBX admin. Una sede si definisce in base agli indirizzi IP con i quali si presentano i telefoni che appartengono a quella determinata sede.

Configurazione del servizio
++++++++++
Per configurare il servizio di gestione delle sedi, è sufficiente seguire il percorso “Impostazioni di sistema > Gestione delle sedi”.
Per creare una nuova sede basta cliccare su “Crea nuova sede”.
La scheda deve essere riempita delle seguenti informazioni:

- **Nome**: nome della sede
- **Limite chiamate totali**: numero massimo di chiamate totali che si permettono su questa sede
- **Chiamate intra sede**: possono essere escluse dal conteggio/incluse nel conteggio
- **Subnet**: ip di registrazione del telefono che appartiene a una determinata sede


Nel conteggio delle chiamate totali ci sono le chiamate dei telefoni che vanno verso l’esterno oppure verso servizi della centrale, o verso un risponditore ecc. Bisogna quindi comunicare alla centrale se un’eventuale chiamata tra due interni di questa sede si deve imputare nel conto delle chiamate che occupano il flusso oppure no. Questo dipende dalla comunicazione tra i telefoni, ovvero se comunicano in direct media oppure no. Se una chiamata tra due telefoni della stessa sede non è in direct media, occupa due flussi all’interno della connettività.

Per quanto riguarda le chiamate intra sede, se non si è sicuri di avere un direct media applicato su tutte le chiamate interne, si dovranno includere nel conteggio. Se invece le chiamate interne alla sede lavorano in direct media, si possono escludere dal conteggio.

**N.B.** Le chiamate intra sede sono diverse da quelle tra interni.
Con “Escluse dal conteggio” quindi, le chiamate intra sede andranno in direct media.

Esempio di un caso specifico: Nel caso in cui più tenant insistono fisicamente dietro la stessa connettività di accesso, i telefoni dei vari tenant si presenteranno alla centrale con lo stesso IP. Si può quindi partizionare questa capacità per suddividerla tra i vari tenant che insistono su una determinata sede. Nel caso semplice ci sarà un unico tenant per cui si assegnano:

- **Tenant**
- **Limite chiamate uscenti**: numero che deve essere minore del limite chiamate totali e che rappresenta il numero massimo che sarà impegnato da chiamate esterne
- **Limite chiamate totali** (che insistono sulla sede)
- **Chiamate intra sede**


Gestione file audio
---------

Descrizione del Servizio
++++++

Il servizio di Gestione File Audio comprende il caricamento e la personalizzazione dei file audio da eseguire durante l’erogazione di determinati servizi.

Configurazione File Audio
+++++++++
Seguendo il percorso Suoni > File Audio, ci troveremo nella pagina in cui è presente la lista dei file audio che si trovano sulla centrale e per ciascuno è possibile personalizzare:

- La riproduzione:
   - Riproduzione nel browser: il file viene riprodotto direttamente nel browser
   - Download: il file viene scaricato localmente
   - Riproduzione su un dispositivo: si può scegliere su quale interno e quale account riprodurlo. Premendo “Riproduci” squillerà l’interno scelto e si potrà ascoltare tramite la cornetta il file audio
- La sostituzione:
   - Caricare un nuovo file audio: è possibile selezionarlo localmente
   - Registrare un nuovo file audio: è possibile registrare un nuovo file audio usando un terminale telefonico. Si sceglie quindi l’interno e l’account sul quale verremo richiamati dalla centrale, quest’ultima ci fornirà delle istruzioni per la corretta registrazione del file
- L’eliminazione dei file audio che non ci servono più


I primi 3 file che visualizziamo sono builtin, cioè file messi a disposizione della centrale:

1. builtin/rec-start: file di avviso dell’inizio della registrazione, nel caso di abilitazione di recording dell’audio delle telefonate
2. builtin/rec-stop: avvisa la fine della registrazione dell’audio della telefonata
3. builtin/spu-start: messaggio audio che notifica a un operatore di un callcenter (qualora fosse attiva la licenza) che un supervisor sta iniziando l’ascolto passivo di quella telefonata

Carica nuovo file audio
+++++++++++
È possibile caricare un nuovo file audio

- Percorso di destinazione esistente: il percorso è una cartella che consente di identificare in modo più semplice delle tipologie di file
- Nuovo percorso di destinazione: è possibile inserire il nuovo percorso
- File: è possibile scegliere un file audio (.wav e .mp3)

I file saranno disponibili nella “Lista dei file audio”.

Registra nuovo file audio
++++++++++

- Nome del file
- Percorso di destinazione esistente
- Nuovo percorso di destinazione
- Dispositivo di registrazione: interno e account da usare per la registrazione del file audio

C’è una limitazione per la dimensione del file che non può superare i 5MB di dimensione.

Configurazione Classi di musica di attesa
+++++++++++
Per configurare le classi di musica d'attesa procediamo andando su Suoni > Classi di musica di attesa.

La musica d’attesa è la riproduzione di file audio che viene utilizzata per molti servizi tra i quali le code di attesa o durante i trasferimenti di chiamata da un interno all’altro. La centrale ha a disposizione 5 classi di musica di attesa preconfigurate, ma è possibile creare un numero arbitrario di nuove classi di musica d’attesa.


Nuova classe di musica di attesa
........

- Nome
- Abilita riproduzione random: opzione che permette di eseguire in modo casuale i file audio inseriti nella playlist, che altrimenti verrebbero normalmente eseguiti dall’alto verso il basso


Modifica classe di musica di attesa
..........

- Carica nuovi file audio: è possibile caricare una serie di file audio


Configurazione Impostazioni Audio
++++++++++
Per configurare le impostazioni Audio procediamo andando su Suoni > Impostazioni audio.

- Lingua del file audio di sistema: è possibile cambiare la lingua
- Classe di musica di attesa predefinita: è possibile visualizzare la lista di playlist precaricate o che aggiungeremo in seguito
- Servizio di ascolto passivo: indica la scelta del file audio da usare di default per il servizio di ascolto passivo

Configurazione Lingue personalizzate
++++++++++
Per il Singletenant Admin e il Multitenant PBX Admin è disponibile la funzione “Lingue personalizzate”.

Per arrivare al servizio basta premere su “Suoni > Lingue personalizzate”.

In questo pannello è possibile definire delle varianti partendo da una base front audio in una determinata lingua.

Infatti nella scheda di personalizzazione si può inserire:

- Nome
- Language pack di base
- Variante

A livello di impostazioni audio è possibile scegliere quindi una lingua custom che eredita tutti i prompt audio della lingua base che si è scelta. Infatti, cliccando sull’elenco della lingua custom creata, sono mostrati tutti i file audio che costituiscono il language pack della lingua di base selezionata. È possibile modificare lo speaker o cambiare il contenuto dei file caricando un file audio che va a sostituire quello standard. Tutto ciò che non viene sostituito, viene ereditato dalla lingua primaria scelta.

Carica archivio con i file audio
++++++++
È possibile caricare uno zip contenente i file audio, questi vengono automaticamente riallocati su quelli precedenti.



Impostazioni SIP
---------

Descrizione del servizio
++++++++++
Il pannello delle impostazioni SIP contiene le specifiche dei setting del motore telefonico. Il protocollo SIP regola la comunicazione tra la centrale e i telefoni e tra la centrale e gli altri gateway.


Configurazione del servizio
+++++++++++
Il pannello è raggiungibile dal menu “PBX > Impostazioni SIP”. Nel caso di un sistema multitenant, il pannello è ad uso del pbx admin perché anche in un nodo multitenant lo stack SIP che gira sulla macchina è unico e condivide le impostazioni tra tutti i tenant. I tenant però possono eseguire in maniera autonoma la configurazione dei propri interni / gruppi / code / account.

- **Abilita controllo pedante dei messaggi SIP**: questa abilitazione fa sì che venga effettuato un controllo più rigoroso della correttezza formale dei messaggi SIP inviati alla centrale e, nel caso in cui questo controllo formale indichi delle malformazioni all’interno del pacchetto SIP, lo scarta.
È una misura di sicurezza che serve ad evitare che arrivino alla centrale dei pacchetti SIP malformati che creano malfunzionamenti o attacchi alla macchina stessa. Nel caso in cui ci si interfaccia con dei provider (gateway, telefoni) che creano dei messaggi SIP non formattati del tutto correttamente, può essere utile disabilitare il flag. In questo caso, viene rilassato il parsing dei messaggi e viene reso accettabile.

- **Modalità DTMF**: toni che possono essere spediti durante una telefonata per mandare comandi o informazioni all’altro interlocutore. Esistono tre modalità previste dallo standard SIP con cui poter inviare e riconoscere i DTMF spediti dall'interlocutore o da mandare all’interlocutore.
   - **RFC 2833**: si può considerare affiancata alla 4733 che richiama ed estende la 2833.
Questa modalità prevede che i toni DTMF sono inviati come pacchetti di tipo RTP event all’interno del flusso RTP di una chiamata. I toni DTMF fanno lo stesso percorso del flusso audio, ma non vengono inviati sotto forma di toni, ma di pacchetti RTP event. Questi messaggi RTP event sono inviati mandando un primo pacchetto (inizio del tono) e successivamente, con periodicità tipica del VoIP, ne viene mandato un altro che allunga la durata del tono. Il contenuto di questi messaggi RTP event è il numero dei tasti premuti e i simboli *#.

Esempio:

Si può visualizzare il tono DTMF inviato in modalità RFC 2833 da parte della centrale 10.0.20.100 verso il pbx:

*jpg*

Questo RTP che arriva viene poi ribaltato dalla centrale all’interlocutore.

Il pacchetto audio è spedito verso un flusso che ha una porta sorgente e destinazione che contiene il flusso RTP. Nel momento in cui la centrale manda un DTMF in modalità RTP event all’interno dello stesso flusso, non cambiano gli estremi delle porte (sono gli stessi del pacchetto audio), ma cambia il payload type.

*jpg*

Nel secondo caso il payload type è il 101 perché l’RTP event cambia il payload type. Kalliope usa di default, per l’invio dei DTMF, il 101.

Il payload diventa un’informazione esplicita del tasto che viene premuto, il volume e la durata in campioni.

L’UDP, in caso di centrale che abbia più di una interfaccia di rete, fa sì che il servizio VoIP venga attivato su tutte le interfacce della centrale. Si può aggiungere una seconda interfaccia di rete, o aggiungere dei Tag VLAN.

*jpg*

La durata è un dato utile perché nel caso in cui la centrale dovesse convertire questo DTMF, nel momento in cui lo spedisce all’interlocutore in un formato diverso dall’RFC 233, dovrebbe riprodurlo per una durata corrispondente. L’impostazione settata in questo pannello vale per tutti gli account SIP definiti nel pannello “Interni e account” ed è usata come impostazione di default per tutte le linee di ingresso e di uscita.

A differenza degli account, nel pannello non c’è la possibilità di andare a cambiare i DTMF: quando si manda un DTMF verso un account lo si manda con le impostazioni SIP e lo stesso si verifica quando un account SIP manda un DTMF. Invece, nel pannello delle linee di ingresso e di uscita si può cambiare la modalità DTMF o lasciarla come di default.

*jpg*

Questa modalità è spesso indicata come AVB (Attribute Value Pair) su altri apparati.

- SIP INFO: è una modalità che non manda messaggi RTP o RTP event, ma un messaggio SIP di tipo info. L’info è un tipo di messaggio SIP che contiene come payload contiene il tasto e la durata, viene trasmesso una sola volta e ha un percorso di rete che segue quello della segnalazione SIP che è diverso dal percorso che effettua il flusso RTP.
- In banda: i toni DTMF digitati sono mandati sotto forma di toni audio all’interno del flusso RTP.
Infatti, se si analizzano le tracce che contengono toni DTMF si trovano solo RTP e non si può distinguere se siano toni o meno. Il problema della trasmissione DTMF sotto toni audio è che se vengono utilizzati dei codec diversi dal G.711, questi introducono una compressione nell’audio e una deformazione dei toni. Mentre una conversazione risulta comprensibile, il riconoscimento di questi toni potrebbe fallire.

*jpg*

Quindi, l’utilizzo della modalità DTMF “in banda” è scoraggiato perché se il flusso RTP subisce un degrado per perdite o congestione, i toni, anche usando G.711 vengono deformati e possono non venire riconosciuti. Quindi l’utilizzo dei DTMF in audio è raccomandato solo in associazione ad un codec compresso PCM a-low o PCM u-low, ma può comunque essere soggetto a errori.

La modalità più utilizzata è la RFC 2833.

I successivi due campi sono due attributi che impattano sia gli account SIP che le linee di ingresso e uscita, come nel caso della modalità DTMF, anche i seguenti due sono modificabili rispetto al valore di default nelle linee di ingresso e di uscita.

- **Abilita accettazione RPID (Remote Party ID)**: abilita accettazione COLP (nominato così nelle linee di ingresso e uscita).
L’abilitazione fa in modo che si estragga l’identità del chiamante non solo dal FROM che manda, ma dagli header PAI, RPID ecc. Si tratta di un header SIP che trasporta un’informazione aggiuntiva che identifica il chiamante. Durante una chiamata, ci sono dei casi in cui l’identificativo della persona con cui si parla possa cambiare nel tempo. La funzionalità del COLP fa in modo che la centrale notifichi che l’interlocutore è cambiato, ci sono dei casi in cui è necessario fornire questa informazione all’interlocutore, e altri in cui non lo è. Questo flag fa sì che si accetti dai telefoni collegati alla centrale, l’identificativo chiamante presente nell’header RPID o PAI (P-Asserted-Identity).

N.B. A livello di uscita si raccomanda che la voce sia disabilitata poiché non si vuole che la centrale modifichi l’identificativo della linea connessa.

- **Send rpid mode**: Modalità invio COLP (nominato così nelle linee di ingresso e uscita).
Ha tre opzioni: disabilitato / remote party ID / P-Asserted-Identity. In questo caso, l’impostazione che viene utilizzata verso i telefoni e che si raccomanda è l’invio del PAI. Questo flag fa sì che la centrale avverta che l’interlocutore con cui si comunica è cambiato, manda un messaggio che aggiorna l’informazione tramite l’header PAI. L’informazione di cambio interlocutore è utile verso i telefoni, ma normalmente su una linea di uscita deve essere disabilitato.

.. note::
   Se si va a fare un trunk verso un’altra centrale in cui configuro interni remoti, in questo caso la linea non è un trunk di uscita verso un operatore, ma è l’interconnessione con un’altra centrale sulla quale è utile attivare la modalità di aggiornamento del COLP.

I tre campi successivi servono per impostare i parametri di qualità del servizio in uscita dalla centrale. Sono presenti i valori esadecimali del TOS e i codici di priorità che nella rete servono per decidere in caso di congestione, quali pacchetti far viaggiare con priorità rispetto agli altri. Quindi, garantisce che flussi audio e video abbiano trattamento privilegiato rispetto all’invio della mail.

- TOS SIP
- TOS Audio
- TOS Video

Questi valori possono essere cambiati se la rete in cui si trova a operare la centrale richiede che siano usati diversi valori di TOS per l’audio, la segnalazione e/o il video.

- **Abilita Video**: per abilitare a livello globale il supporto alle videochiamate
- **Bitrate massimo per le chiamate video**: attributo che vale solo per le chiamate video e determina il bitrate massimo che la centrale accetta e offre per le videochiamate, di default è 384 Kbps per non occupare troppa banda. Spesso i valori possono essere alzati per aumentare la qualità.
- **Abilita supporto alla cifratura RTP (SRTP)**: abilita a livello di centrale la possibilità di attivare l’encryption dei flussi RTP che normalmente viaggiano in chiaro (chiunque riesca a intercettare il flusso RTP della chiamata può ascoltarne il contenuto).

SRPT è un protocollo che si basa sul preventivo scambio di chiavi tra chiamante e chiamato, il flusso è cifrato con un cifratore a chiave simmetrica. La chiave viene scambiata in fase di setup della chiamata e, se non si usa un protocollo di trasporto della segnalazione sicuro come TLS e si usa invece TCP o UDP, si può leggere in chiaro sul messaggio SIP. L’attivazione dell’SRPT ha senso se è accoppiata a un protocollo di segnalazione di tipo sicuro come TLS.

.. warning::
   L’abilitazione dell’SRTP nelle impostazioni SIP non abilita automaticamente l’effettivo utilizzo dell’SRTP, ma abilita il modulo da supporto SRPT. È necessario abilitarlo nel pannello degli “Interni e account”. Qui, è presente la spunta “Abilita SRPT”: in questo modo può essere ereditato da tutti gli account che usano quel determinato template.

I due campi successivi non sono necessari da configurare, se non quando si vuole esporre il servizio tramite WebRtc (tramite Web Socket) ed è necessario specificare un server STUN per acquisire l’informazione necessari aa far chiudere correttamente segnalazione e media.

.. note::
   STUN è un protocollo che serve per distribuire l’informazione dell’IP pubblico utilizzato da un client che si trova dietro un NAT. Viene usato dai client web rtc (telefono web) per fare in modo che la centrale sappia qual è l’indirizzo IP a cui spedire i flussi media. Va di pari passo con l’abilitazione del trasporto (protocollo per le segnalazioni SIP) tramite Web Socket e, una volta attivato il Web Socket Sicuro, c’è necessità di specificare un server STUN, che la centrale usa pere imparare quali sono le porte che utilizzerà per la segnalazione e per il media.

- Indirizzo del server STUN
- Posta del server STUN

NAT Helper
+++++++
Questa sezione è particolarmente importante per rendere la centrale disponibile in accesso dal pubblico.

- Host esterno: indirizzo IP pubblico
- Periodo di aggiornamento dell’host esterno (sec.)
- Porta UDP esterna
- Porta TCP esterna
- Porta TLS esterna
- Reti locali

Per tutti i messaggi inviati alle reti marcate come locali usa il proprio indirizzo privato come da routing, mentre ciò che è fuori dalle reti locali usa l’indirizzo IP che specificate nell’host esterno.

Codec video predefiniti
..........
Per abilitare il supporto alle videochiamate si spunta la sopracitata casella “Abilita video” e selezionare quali codec video sono supportati dalla centrale.

Codec audio
.........
Anche per l’audio si può selezionare quali codec sono supportati dalle centrale.


Impostazioni SSL
-------

Descrizione del Servizio
++++++++++
La sezione impostazioni SSL (Secure Sockets Layer) contiene la gestione delle CA (Certification Authority) affidabili.

Configurazione del Servizio
++++++++++
Per raggiungere la sezione delle impostazioni SSL, è sufficiente seguire il percorso "Impostazioni di sistema > Impostazioni SSL" come mostrato nella figura a destra.

Gestione delle CA affidabili
.........
In questa sezione è presente la lista delle Certification Autority dei vendor dei telefoni che la centrale ritiene valide per autenticare un certificato client.

Difficilmente il certificato del server viene emesso direttamente da una delle CA presenti nel telefono, poiché sono CA di tipo no root. Spesso i certificati sono emessi da CA intermedie.

.. note::
   È importante ricordare la corretta sequenza della catena: CA root > CA intermedia > certificati server


La CA root emette un certificato per una CA intermedia e quest’ultima emette i certificati server. Bisogna quindi caricare il certificato server composto da certificato vero e proprio e chiave privata e le CA intermedie che servono per costruire la catena di trust fino alla CA root.

I certificati devono essere messi insieme dentro un unico file .pem. Il telefono quindi fornisce il certificato client, il certificato viene validato dal pbx usando le CA affidabili presenti nel pannello.

Se il certificato viene ritenuto valido e sia il CN (common name) che il MAC address coincidono col file che sta richiedendo, allora tutto corrisponde, la sessione si chiude e può partire il download del file di provisioning.

Mentre sui browser sono spesso precaricate CA intermedie, nei telefoni, per ragioni di occupazione di memoria ci sono solo le CA root. Se carichiamo sulla macchina solo il certificato server firmato da una intermedia (firmata da una CA root), ma il server passa al telefono solo il proprio certificato e non quello intermedio, questo non è ritenuto valido dal telefono.

È necessario quindi caricare sia la CA intermedia che il certificato server.


Gestione del certificato del server
..........
In questa sezione è possibile caricare il certificato del server in un singolo file .pem.

Di default, su tutti i Kalliope, è presente un certificato self assigned che è emesso da una CA autogenerata e interna alla centrale.

È possibile creare un nuovo certificato CSR (Certificate Signing Request), premendo su "Crea nuovo CSR" e inserendo:

i dettagli del nuovo certificato e le identità aggiuntive:

- Stato
- Provincia
- Località
- Ente
- Reparto
- Nome comune
- E-mail


Gestione dell'autorità di certificazione locale
.............
In questa sezione si possono osservare i dettagli del certificato di root e la lista dei certificati emessi.

È anche possibile:

- Emettere un nuovo certificato premendo su "Emetti nuovo certificato" e inserendo i dettagli del nuovo certificato e le identità aggiuntive:
   - Installa come un certificato del server
   - Stato
   - Provincia
   - Località
   - Ente
   - Reparto
   - Nome comune
   - E-mail
- Scaricare il certificato di root della CA locale (.pem)
- Scaricare il certificato di root della CA locale (.der)
- Eliminare l'autorità di certificazione locale

Inoltro su PBX isolato
----------

.. note::
   
   **Informazioni**
   
   - Firmware: 4.5.9 e superiori
   - Disponibile in sistema single-tenant e multi-tenant (livello admin di tenant)
   
Descrizione funzionale
++++++++
Questo servizio permette di specificare una destinazione di inoltro di tutte le chiamate in ingresso al PBX (o al tenant, in sistemi multi-tenant) nel caso in cui tutti gli account SIP associati agli interni siano irraggiungibili.

Questo servizio è particolarmente utile negli scenari in cui il PBX è installato in remoto rispetto ai terminali (ad esempio installazione in data center remoto, e telefoni presenti in sede cliente); nel caso in cui la sede del cliente diventi isolata rispetto alla centrale, tutte le chiamate in entrata potranno essere inoltrate ad una destinazione di backup (ad esempio un numero di cellulare, o un messaggio di cortesia).

In ambiente multitenant, l'attivazione del servizio e la configurazione della destinazione di inoltro sono configurabili in modo differenziato ed indipendente per ciascun tenant, direttamente dall'admin del tenant stesso.

Configurazione del servizio
+++++++++
La configurazione del servizio viene effettuata nel pannello PBX -> Impostazioni Generali, nella sezione "Comportamento in caso tutti gli account siano non registrati".

Oltre alla checkbox di abilitazione del servizio, è presente il tradizionale modulo di selezione dell'azione di inoltro, con il quale è possibile specificare un eventuale file audio da riprodurre al chiamante, e l'azione da compiere sulla chiamata in ingresso (selezionabile da menu a tendina). Nel caso di inoltro della chiamata ad un numero esterno (di raggiungibilità di emergenza) è necessario specificare (oltre al numero di destinazione, senza l'eventuale prefisso di selezione linea esterna) anche l'identità (che determinerà il numero chiamante presentato in uscita) e la classe di abilitazione che KalliopePBX utilizzerà per effettuare la chiamata.


Interfacciamento tramite AMI con software di terze parti
-----------

Descrizione del servizio
++++++++++
L'Asterisk Manager Interface presente su KalliopePBX consente l'interfacciamento con software di terze parti.
Il pannello mostrato a destra permette di definire le credenziali di autenticazione (username e password), insieme ad una ACL composta da uno o più indirizzi/subnet IP. L'utente configurato dispone dei diritti di lettura “call” e di scrittura “call,originate”.

Configurazione del servizio
+++++++++

Abilitando l'interfaccia AMI da GUI Kalliope è, quindi, possibile interfacciare sistemi esterni con il KalliopePBX per effettuare operazioni di click-to-call.

La sintassi standard per effettuare il c2c via AMI (dall'interno %interno% verso la destinazione %toNum%, comprensivo di prefisso di uscita se esterno) su KalliopePBXv4 è la seguente, in cui vengono impostate alcune variabili di canale:

.. code-block:: console

   Action: Originate
   Async: true
   Channel: Local/%interno%@c2c
   Context: from_c2c
   Exten: %toNum%
   CallerId: %callerId%
   Timeout: %timeout%
   Priority: 1
   Variable: C2C_SRC=%interno%
   Variable: C2C_DST=%toNum%
   Variable: __TENANT_UUID=%tenantUid%

Dove:

- **%callerId%** = in formato "%displayname%" <%numero%> ( noi impostiamo "c2c: %toNum%" <%toNum%>)
- **%timeout%** = numero di millisecondi di squillo per accettare la chiamata sul terminale del chiamante (noi impostiamo 10000)
- **%tenantUid%** = l'UUID del tenant utilizzato. In caso di PBX monotenant va indicato comunque, è riportato sul pannello dei settings AMI (nei firmware 4.2.x) o nel widget della dashboard (nei firmware 4.3.x)

Nel caso del TSP Xtelsio Tapi for asterisk (frequentemente utilizzato per l'integrazione dell'applicativo Estos ProCall con sistemi Asterisk) non è possibile (alla data odierna) impostare queste variabili nella chiamata AMI, per cui è stato sviluppato un meccanismo che si basa su dei contesti wrapper per impostare a dialplan le variabili necessarie.

Il messaggio AMI da far inviare diventa quindi (sono comunque supportate entrambe le modalità):

.. code-block:: console

   Action: Originate
   Async: true
   Channel: Local/%interno%@c2c_%tenantUid%
   Context: from_c2c_%tenantUid%
   Exten: %toNum%
   CallerId: "c2c: %toNum%" <%interno%>
   Timeout: %timeout%
   Priority: 1



Modalità operativa ridotta
---------

Descrizione del servizio
+++++++++++
Questo servizio consente all'amministratore del KPBX di definire delle modalità operative ristrette in cui è possibile limitare alcune tipologie di chiamate pur mantenendo inalterata la configurazione telefonica (interni/account, instradamento, linee di uscita).
Al momento sono previste tre diverse modalità operative:

- Completa: consente la piena operatività del PBX senza alcun blocco sulle chiamate. Questa è la modalità di default di KalliopePBX.
- Limitata: blocco chiamate uscenti: consente le chiamate tra interni e verso i numeri di servizio del KPBX e verso i numeri definiti nella whitelist. Tutte le altre chiamate uscenti sono bloccate.
- Disabilitata: tutte le funzionalità telefoniche sono disabilitate (registrazione account, chiamate tra interni, etc.).

In ambiente multitenant la modalità operativa è configurabile per tenant ma esclusivamente dal pbxadmin.

Configurazione del servizio
+++++++++++++
La modalità operativa può essere configurata nel pannello PBX --> Modalità operativa

Whitelist
.......
In caso di modalità limitata deve essere specificata la whitelist se si vogliono consentire chiamate in uscita verso specifiche numerazioni (ad es. chiamate di emergenza).
La configurazione della whitelist viene effettuata nel pannello PBX --> Whitelist



Monitoraggio servizi
--------

Descrizione del servizio+
++++++++++++
Per accedere al servizio di Monitoraggio Servizi basta seguire il percorso “Monitoraggio > Monitoraggio Servizi”.
Nella pagina è possibile visualizzare e filtrare i seguenti elementi per affinare la ricerca:

.. list-table::  
 :widths: 25 25
 :header-rows: 1

 * - Parametro
   - Valore
 * - Interno
   - Alfanumerico
 * - Nome
   - Alfanumerico
 * - Cognome
   - Alfanumerico
 * - CFIM
   - Qualsiasi valore/OFF/ON
 * - CFBS
   - Qualsiasi valore/OFF/ON
 * - CFNA
   - Qualsiasi valore/OFF/ON
 * - CFUN
   - Qualsiasi valore/OFF/ON
 * - DND
   - Qualsiasi valore/OFF/ON
 * - Fork2Mobile
   - Qualsiasi valore/OFF/ON
 * - Busylevel
   - Alfanumerico

Per quanto riguarda il busylevel, tramite l’icona di modifica Modifica.JPG è possibile "Abilitare il livello di occupato" per un determinato interno selezionato:

*jpg*


Notifica eventi
----------
Descrizione del servizio
++++++++++

Tramite questo servizio è possibile monitorare gli eventi selezionati ricevendo delle notifiche.

Per ogni evento selezionato dall’utente è possibile associare delle azioni di notifica, come l’invio di una mail o la chiamata ad un Web Service.

Configurazione del servizio
++++++++
Nella sessione Monitoraggio → Notifiche è possibile gestire la funzionalità di notifica.

Notification Action List
........
In Notification Action List è possibile aggiungere una nuova notification selezionando l’azione di Email o WebService.

Email
......
Selezionando Add New Email Notification Action è possibile definire il destinatario della mail di notifica dell’evento e le informazioni che vogliamo trasmettere. Nella tabella seguente sono illustrati i parametri che è possibile definire per l’Email Notification.

.. list-table::  
 :widths: 25 25 25
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Abilitato
   - Consente di disabilitare l’Email Notification
   - Si / No
 * - Nome
   - Identificativo della notifica
   - Alfanumerico

**Email Settings**

.. list-table::  
 :widths: 25 25 25
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Destinatari
   - Indirizzo email del destinatario della notifica
   - Alfanumerico
 * - Soggetto
   - Oggetti della mail di notifica
   - Alfanumerico
 * - Body
   - Testo dell’email contenente placeholder sia di default che specifici dell’ evento	  - Alfanumerico

I parametri generici sono elencati nella seguente tabella:

.. list-table::  
 :widths: 25 25
 :header-rows: 1

 * - Parametro
   - Descrizione
 * - %event_id%
   - sequenziale dell'evento
 * - %event_name%
   - identificativo dell'evento
 * - %event_description%
   - descrizione testuale dell'evento
 * - %event_severity%
   - criticità dell'evento (numerica, da 4 a 0 corrispondenti ai livelli DEBUG|INFO|WARNING|CRITICAL|FATAL
 * - %event_timestamp%
   - epoch di occorrenza dell'evento
   
I parametri specifici di evento sono invece elencati nella nel pannello Notification; questi paramentri possono essere riportati in tre formati diversi: JSON, XML e AVP.

Il set completo dei parametri relativi ad un evento è ottenibile con il placeholder: %call_params[<format>]%


Web Service

Selezionando Add New WebService Notification Action è necessario inserire il nome della notification che partirà al verificarsi dell’evento, tra le impostazioni generali.

Nella tabella seguente sono illustrati i parametri che è possibile definire per la WebService Notification.


.. list-table::  
 :widths: 25 25 25
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - Abilitato
   - Consente di disabilitare la WebService Notification
   - Si / No
 * - Nome
   - Identificativo della notifica
   - Alfanumerico

**WebService Settings**

.. list-table::  
 :widths: 25 25 25
 :header-rows: 1

 * - Parametro
   - Descrizione
   - Valore
 * - URL
   - URL di Notifica
   - Alfanumerico
 * - Tipo Auth
   - Tipo di Autenticazione
   - None/ Basic
 * - Auth username
   - Username per autenticazione (solo in caso Auth)
   - Alfanumerico
 * - Auth password
   - Password per autenticazione (solo in caso Auth)
   - Alfanumerico
 * - Tipo Request
   - Tipo della richiesta
   - Get/Post
 * - Request content
   - Contenuto della richiesta (solo Post)
   - Placeholder

Al verificarsi dell’evento arriverà una segnalazione al WebService esterno che gestirà le informazioni ricevute.

Notification List
............
Nella sezione Notification List, selezionando Add new notification è possibile selezionare l’evento per cui ottenere la notifica.

Nella tabella seguente sono elencati gli eventi che possono essere monitorati e a cui può essere associata una notifica.


.. list-table::  
 :widths: 25 25
 :header-rows: 1

 * - Evento
   - Descrizione
 * - ademco.*.* / alarmreceiver.*.*
   - Eventi specifici utilizzati dal modulo opzionale KalliopeLift per interfacciarsi con i combinatori telefonici degli ascensori
 * - cti.client.background
   - Un client CTI (sistema operativo mobile) è stato messo in backrground
 * - cti.client.login
   - Un client CTI ha effettuato il login
 * - cti.client.login-failed
   - Un client CTI ha fallito un login
 * - cti.client.logoff
   - Un client CTI ha effettuato il logout
 * - mobile-app.call.incoming
   - Chiamata in arrivo all'account dell'app mobile
 * - mobile-app.call.timeout
   - La chiamata all'account dell'app mobile è scaduta
 * - mobile-app.status.not-logged
   - L'applicazione mobile non è registrata
 * - mobile-app.wake-up.registered
   - L'app mobile si è attivata
 * - mobile-app.wake-up.sent
   - Notifica di sveglia inviata all'account dell'app mobile
 * - mobile-app.wake-up.timeout
   - L'applicazione mobile non si attiva entro 5 secondi dall'invio della notifica
 * - pbx.account.incomingcall
   - Una chiamata per un interno inoltrata all'account
 * - pbx.account.startcall
   - Tentativo di chiamata all'account avviato
 * - pbx.account.unavailable
   - Tentativo di chiamata all'account non iniziato perché l'account non è disponibile
 * - pbx.call.end
   - Una chiamata finisce
 * - pbx.call.start
   - Una chiamata inizia
 * - pbx.dynamic-routing.enter
   - Una chiamata è entrata nel servizio di Instradamento dinamico
 * - pbx.dynamic-routing.input
   - Un nuovo parametro è stato inserito dal chiamante nell'instradamento dinamico
 * - pbx.extension.answercall
   - Chiamata all'interno risposta da uno degli account associati
 * - pbx.extension.failedcall
   - Chiamata all'interno fallita
 * - pbx.extension.incomingcall
   - Chiamata all'interno in arrivo
 * - pbx.extension.missedcall
   - Un interno ha perso una chiamata; l'evento viene innescato solo se nelle azioni di trabocco di quell'interno è spuntata la voce "genera evento"
 * - pbx.queue.enqueue
   - Chiamata in attesa
 * - pbx.queue.enter
   - Una chiamata arriva al servizio di coda
 * - pbx.queue.ringmember
   - Una chiamata viene presentata ad un operatore di coda
 * - pbx.queue.ringnoanswer
   - Un operatore selezionato non ha gestito la chiamata; la chiamata è ancora in coda e andrà ad altri operatori, se ci sono e non è scaduto il tempo massimo di attesa
 * - pbx.queue.servedcall
   - Una chiamata nella coda è stata servita, ovvero risposta da un operatore
 * - pbx.queue.unservedcall
   - Una chiamata nella coda non è stata servita globalmente; rappresenta quindi l'esito finale della chiamata che non è stata servita da nessun operatore
 * - pbx.queuemember.added
   - Un operatore di coda aggiunto
 * - pbx.queue.enqueue
   - Una chiamata entra nel servizio di coda; la coda è aperta
 * - pbx.queuemember.pause
   - Un operatore di coda è entrato in pausa
 * - pbx.queuemember.unpause
   - Un operatore di coda è uscito dalla pausa
 * - pbx.spy.start
   - Avviata la spia di supervisore
 * - pbx.spy.stop
   - Interrotta la spia di supervisore
 * - pbx.queuemember.removed
   - Un operatore di coda è rimosso
 * - pbx.wake-up.unanswered
   - Il servizio sveglia non ha avuto risposta dalla camera
 * - pbx.user.create
   - È stato creato un nuovo utente di Kalliope
 * - pbx.user.password-change
   - È stata cambiata la password di un utente di Kalliope
 * - storage.quota.exceeded
   - È stata superata la quota di archiviazione riservata ad un determinato tenant
 * - storage.quota.restored
   - L'occupazione di archiviazione di un determinato tenant è tornata sotto la quota riservata











































Registro delle chiamate
------------





Richieste di Provisioning
-----------

Descrizione del servizio
++++++++
Per visualizzare le richieste di provisioning, è necessario seguire il percorso “Registri > Richieste di provisioning”.

All’interno di questa sezione sono registrate le richieste di provisioning che provengono dai telefoni.

È possibile visualizzare:

- Giorno del mese della richiesta
- Timestamp
- Indirizzo IP
- Protocollo
- Identità del certificato
- User Agent
- Percorso richiesto
- Indirizzo MAC richiedente
- Percorso locale
- Codice di stato HTTP

Rubrica telefonica
----------

Servizi in chiamata
------------

Questa sezione dell'interfaccia Kalliope permette di configurare i codici relativi ai servizi in chiamata.

L'unico servizio per il quale non è possibile personalizzare il codice è la cancellazione di un trasferimento con offerta, di default è *0.

I restanti codici sono liberamente configurabili e si riferiscono ai servizi riportati nella seguente tabella.

.. list-table::  
 :widths: 25 25
 :header-rows: 1

 * - Servizio
   - Default
 * - Trasferimento con offerta
   - *4 Trasferimento, *0 Annulla trasferimento, *9 Shuttle, *3 Converti in una conferenza a tre
 * - Trasferimento diretto
   - #4
 * - Parcheggio chiamata
   - #8
 * - Trasferimento rapido
   - **
 * - Registrazione chiamata su richiesta
   - *1
 * - Codice riaggancio chiamata
   - *0

Statistiche di utilizzo
------------

Descrizione del servizio
+++++++++

Il servizio è raggiungibile tramite “Registri > Statistiche di utilizzo”.

Le statistiche di utilizzo sono uno strumento utile per visualizzare l’andamento – annuale e/o mensile – dell’utilizzo della centrale PBX. La pagina fornisce una visione del modo in cui crescono le occupazioni a livello di PBX.

Sono visualizzati i Tenant definiti con il Nome, Dominio e UUID. Il primo numero rappresenta il numero di interni configurati sul Tenant, il secondo è il numero di istanze FAX e il terzo è il numero di camere hotel che sono state create.

La visualizzazione può essere ridimensionata anche al mese corrente e al mese precedente con la visualizzazione dei singoli giorni del mese.


È inoltre possibile esportare i dati nei seguenti formati:

- XLSX
- CSV
- JSON
- XML

Supporto SNMP
----------
Descrizione del servizio
+++++++++++
Funzionamento del protocollo
..........
SNMP è lo standard per la gestione ed il monitoraggio di rete. È quindi un protocollo che serve per il monitoraggio dello stato di una macchina, nello specifico, per acquisire da un server di monitoraggio esterno al Kalliope parametri di stato legati al carico della CPU, occupazione di memoria, spazio disco, chiamate contemporanee. È un protocollo standard disponibile su Kalliope, sulla centrale si rendono disponibili gli OID (oggetti sottoposti a monitoraggio). Si usano quelli definiti nel MIB 2 standard, dove ci sono gli identificativi degli oggetti resi disponibili tramite l’agent. Il server è il sistema di monitoraggio che interroga, mentre l’agent SNMP è il servizio che serve per esporre i dati a un client che ne faccia richiesta. L’SNMP prevede che il client faccia una richiesta all’agent per sapere il valore dell’OID e l’agent restituisce il valore.

I dati all’interno dell’agent sono organizzati sottoforma di albero. I dati indicano per esempio la versione del firmware primario, secondario, informazioni riguardo i servizi telefonici, la dimensione della memoria virtuale occupata dal processo, il numero totale di tentativi di autenticazione fallita da parte di client SIP.

Gli oggetti sono definiti come indice di una foglia sotto ad un padre: c’è una struttura ad albero che permette di accedere, specificando l’indirizzo del percorso tra i sottoalberi fino alla foglia, quale è l’oggetto che si vuole monitorare. L’SNMP prevede:

- Manager
- Agent
- Protocollo

La rappresentazione di un OIP avviene come sequenza di numeri, es: 1.3.6.1.2.1.4.6 è il percorso all’interno dell’albero e ciascun punto del percorso ha una sua corrispondenza testuale.

Configurazione del servizio
+++++++++
Per attivare il sopporto NSMP basta andare su “Impostazioni di sistema > Impostazioni SNMP” e premere sulla spunta “Abilitato”.

Impostazioni di sistema
.........
Le seguenti informazioni sono obbligatorie e se non vengono inserite, il servizio SNMP non può avviarsi.

- **sysName**: è un particolare OID sotto l’albero system (che è il primo figlio ed è indicato come 1.3.1.2.1.1), sysName è il nome della macchina ed è 1.3.6.1.2.1.1.5.0 (lo 0 in fondo poiché è di tipo scalare).
- **sysLocation**: è la location fisica, funge come una sorta di inventario
- **sysContac**t: indirizzo mail del referente da contattare se c’è un’anomalia in quel determinato nodo
Nelle impostazioni definite c’è l’albero delle MIB 2 e le host-resources (1.3.6.1.25) che sono i due che si espongono su Kalliope. Vengono anche esposte le MIB proprietarie e il software può leggere tutto l’albero poiché lo scansiona interamente ed è compito dell’agent restituire i valori. Il file delle MIB serve per permettere al software che fa monitoraggio di sapere la singola foglia che conosce solo per numero che cosa sia.
Per gli esempi di configurazione è stato utilizzato il client iReasoning MI Browser che può fare interrogazioni SNMP e mostra l’organizzazione dei sottoalberi.

Impostazioni di accesso SNMP
...........

- **Indirizzo IP di ascolto**: es. di default 0.0.0.0 significa che ascolta su tutte le interfacce della centrale. Ma, se abbiamo un pbx con più interfacce di rete, alcune pubbliche e alcune private, e si vuole che il servizio SNMP sia accessibile solo da una di queste interfacce, si può mettere l’indirizzo IP dell’interfaccia su cui si vuole che sia attivo il servizio. Si può quindi fare un bind del servizio sull’IP inserito, questo deve essere uno degli IP che la centrale ha (una delle sue interfacce o quello dell’Alta Affidabilità nel caso di un cluster). Nell’ultimo caso, nel caso di AA, è bene che venga fatto monitoraggio esplicito non puntano l’IP della risorsa ma i singoli IP dei due nodi.
- **Porta di ascolto**: 161 è la porta standard poiché SNMP utilizza il protocollo di traporto UDP.
- **Community v1/v2**: sono le versioni base di SNMP supportate dai sistemi di monitoraggio, non è ancora abilitato il supporto SNMP v3. Il valore predefinito che viene usato è “public”
- **ACL**: Access Control List, è una restrizione a quale indirizzo IP deve avere il client per l’interrogazione. Se arriva una richiesta SNMP fuori dall’ACL, questa viene rifiutata.

.. warning::
   
   Non è consigliato ACL 0.0.0.0/0, è sempre bene restringere l’accesso solo agli IP autorizzati
   
Impostazioni delle trap
...........
Le trap sono un meccanismo di tipo reattivo che gli agent SNMP hanno per notificare il verificarsi di eventi. Kalliope non ha aggiunto tra specifiche al sistema e sono presenti quelle base:

- 0: ColdStart
- 1: WarmStart
- 2: linkDOwn
- 3: linkUp
- 4: authenticationFailure
- 5: egpNeighbortLoss
- 6: enterpreseSpecific

Indicazioni sulla configurazione delle TRAP:

- Metodo di invio delle TRAP: specificare se si vuole mandare la trap in versione 1 o 2
- Indirizzo IP di destinazione delle TRAP: indicare indirizzo IP del server di monitoraggio a cui inviare le TRAP
- Porta di destinazione delle TRAP: es. 162 è la standard

Sulla dashboard viene indicata l’esecuzione del servizio SNMP tramite il pallino verde e lo stato “Attivo”.

È possibile fare un’interrogazione dell’agent su Kalliope tramite un qualunque client SNMP (in questo caso si utilizza il già sopracitato iReasoning MIB Browser). Bisogna indicare l’indirizzo IP a cui collegarsi e poi impostare

- Agent NSMP Version: i valori di default con cui fare la richiesta, ovvero si può scegliere se farla in versione 1 o 2
- Agent Read Community: qual è la community di lettura per poter avere accesso ai dati
- Agent Port: si può indicare la porta standard, 161
- Agent Write Community: non è abilitata la possibilità di fare scrittura tramite SNMP

Dopo aver effettuato l'interrogazione è possibile leggere il contenuto dell’albero che è presente su Kalliope. La lettura può essere fatta oggetto per oggetto: Il sottoalbero system presente le seguenti informazioni tra cui il sysContact, il sysName e il sysLocation.

Il pannello interfaces restituisce le varie interfacce presenti e per ciascuna indica lo stato operativa e i byte scambiati in ingresso e uscita, questo permette ai sistemi di monitoraggio di far vedere il grafico dell’occupazione:


Esempio del kpbxNode:

*jpg*

.. note::
   Il contatore delle autenticazioni fallite (evidenziato in blu) è un dato importante poiché nel momento in cui dovesse arrivare un burst di autenticazioni fallite, probabilmente si tratterebbe di un attacco proveniente dall’esterno.


KalliopePBX espone delle MIB che consentono il monitoraggio del funzionamento dell’apparato tramite il protocollo di comunicazione standard SNMP.
Le MIB SNMP consultabili su Kalliope sono:

MIB-II standard (RFC 1213) – Questa MIB definisce gli oggetti per la gestione e il monitoraggio di un apparato in una rete TCP/IP, in particolare su Kalliope sono implementati i seguenti sottoalberi: system, interfaces, at, ip, icmp, tcp, udp, transmission, snmp OID: 1.3.6.1.2.1.1/2/3/4/5/6/7/10/11
https://datatracker.ietf.org/doc/rfc1213/

Host Resource MIB (RFC 2790) - Questa MIB definisce un insieme di oggetti contenenti la configurazione di host (server/computer) collegati ad una rete TCP/IP indipendentemente dal sistema operativo, dai servizi di rete e dalle applicazioni software installate. OID: 1.3.6.1.2.1.25
https://datatracker.ietf.org/doc/rfc2790/

UCD-SNMP-MIB – Questa MIB definisce gli oggetti per il monitoraggio delle performance di un host (ad es. CPU /RAM / occupazione dischi). OID: 1.3.6.1.4.1.2021
http://www.net-snmp.org/mibs/UCD-SNMP-MIB.txt

Kalliope MIB: questa MIB proprietaria fornisce informazioni aggiuntive sulla configurazione e il funzionamento dei servizi implementati sul nodo Kalliope come ad es. numero di account configurati o registrati, chiamate contemporanee, numero totale di chiamate. OID:1.3.6.1.4.1.33732
Scarica i file di definizioni delle MIB:

Media:Definizioni MIB.zip







