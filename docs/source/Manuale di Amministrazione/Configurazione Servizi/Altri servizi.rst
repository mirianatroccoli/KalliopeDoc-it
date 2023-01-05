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









