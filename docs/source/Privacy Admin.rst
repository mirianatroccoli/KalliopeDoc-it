Privacy Admin
======

L’utente speciale privacyadmin
-----

L’utente privacyadmin ha un accesso completamente indipendente dall’utente amministratore di sistema (admin) in modo da preservare integralmente le informazioni soggette alla privacy contenute all’interno della centrale KalliopePBX.
In particolare, quando si accede all’interfaccia web di KalliopePBX con le credenziali di "amministratore di privacy" (utente speciale privacyadmin) il menu operativo mostra solo le seguenti voci:

- Rubrica telefonica
- Registro delle chiamate
- Impostazioni di sistema
- Registrazione delle chiamate

Il registro delle chiamate permette di visionare tutte le chiamate effettuate e ricevute dalla centrale KalliopePBX complete di tutti i dettagli e con i numeri in chiaro. Ricordiamo invece che l’amministratore tecnico (admin) non può in alcun modo visionare i numeri in chiaro sul registro delle chiamate in quanto risultano tutti anonimizzati nelle ultime 3 cifre, a tutela della privacy del cliente finale.

Alla voce Impostazioni di sistema il privacyadmin può decidere di delegare i suoi “poteri” (ovvero i diritti di accesso alle informazioni soggette a privacy) anche ad altri utenti standard del centralino. Solo il privacy admin può delegare altri utenti e modificarne i diritti di accesso alle informazioni di privacy.
Il servizio di registrazione delle chiamate è disponibile solo all’utente speciale privacyadmin e agli utenti eventualmente da lui (e lui solo) delegati. Tale servizio si compone di due schermate:

- Visualizza registro (delle chiamate registrate)
- Modifica Impostazioni (del servizio di registrazione)

1. Visualizzazione registro delle chiamate
+++++

Nel registro delle chiamate registrate il privacyadmin (così come gli utenti eventualmente da lui delegati) può accedere alla lista delle registrazioni delle chiamate, effettuare ricerche avanzate, ascoltare le registrazioni direttamente dal browser web (cliccando sul simbolo Play.png ) oppure scaricarle sul proprio PC (cliccando sul simbolo Download.png).

*jpg*

Ogni mese viene creato automaticamente un nuovo tab per rendere la consultazione più agevole. Le chiamate vengono elencate di default dalla più recente alla più vecchia, e riportano:

- UniqueID, identificativo univoco della chiamata
- Data e ora di inizio e fine della registrazione
- Direzione, ovvero quale flusso è stato registrato (in / out / both / mix)
- Tipo di registrazione effettuata (incondizionata / su richiesta)
- Volume di archiviazione (storage locale / remoto)
- Percorso di archiviazione
- Richiedente
- Tipo di destinazione
- Nome destinazione

2. Impostazioni servizio di registrazione delle chiamate
+++++

In questa pagina è possibile impostare le entità che regolano il comportamento del servizio di registrazione delle chiamate. Per prima cosa è possibile impostare uno o più percorsi di archiviazione su cui andare a salvare le registrazioni. Oltre allo storage locale è infatti possibile selezionare percorsi di registrazione remoti (se opportunamente configurati). Nel riquadro "Entità abilitate alla registrazione delle chiamate" è possibile invece impostare le varie regole di registrazione desiderate.

*jpg*

Nella tabella seguente sono illustrati i parametri che è possibile definire per ogni entità di registrazione (da sinistra verso destra).

.. list-table::  
   :widths: 25 25 50
   :header-rows: 1

   * - Parametro
     - Descrizione
     - Valore
   * - Abilitato
     - Abilitare o disabilitare una entità di registrazione	
     - On/Off
   * - Tipo entità
     - Tipo di chiamata per la quale attivare la registrazione
     - Chiamata a gruppo/Chiamata a coda/Chiamata a interno/Chiamata da interno
   * - Entità
     - Dipende dal campo precedente. Indica l’identità coinvolta nella regola di registrazione	
     - Nome gruppo/Nome coda/Interno
   * - Tipo di registrazione
     - Indica se la registrazione della chiamata debba avvenire automaticamente per tutte le chiamate coinvolte oppure su richiesta, con possibilità di avviare la registrazione anche sulla chiamata in corso. In quest’ultimo caso la registrazione riguarderà la porzione di chiamata contenuta tra i comandi di inizio e fine registrazione su richiesta (codice definito e modificabile nel menu PBX > Servizi in chiamata)
     - Incondizionata/su richiesta
   * - Abilita/disabilita servizio per chiamate interne
     - Abilitare o disabilitare questa entità di registrazione qualora la chiamata avvenga tra due interni del KalliopePBX
     - On/Off
   * - Su avvio registrazione
     - Definisce il file da eseguire in chiamata per segnalare l’inizio della registrazione della chiamata (tra quelli resi disponibili sul KalliopePBX tramite le impostazioni File Audio)
     - Percorso del file audio tra quelli disponibili
   * - Su fine registrazione
     - Definisce il file da eseguire in chiamata per segnalare la fine della registrazione della chiamata (tra quelli resi disponibili sul KalliopePBX tramite le impostazioni File Audio)
     - Percorso del file audio tra quelli disponibili
   * - Prefisso del percorso
     - Permette di definire il prefisso del percorso di salvataggio del file della registrazione tra quelli disponibili (vedi immagine di esempio). Può anche rimanere vuoto
     - Nessun prefisso / Uno dei valori del menu a tendina 
   * - Percorso personalizzato
     - Permette di definire un percorso personalizzato di salvataggio del file della registrazione da appendere al prefisso eventualmente impostato nel campo precedente in modo da facilitarne la catalogazione sullo storage di destinazione. Questo campo può restare vuoto
     - Testo del percorso personalizzato
   * - Suffisso del percorso
     - Permette di definire il suffisso del percorso di salvataggio del file della registrazione tra quelli disponibili (vedi immagine di esempio). Può anche rimanere vuoto. Il suffisso del percorso di salvataggio verrà concatenato agli eventuali campi prefisso e percorso personalizzato. Alla file il percorso sarà quindi dato da prefisso + percorso personalizzato + suffisso
     - Nessun prefisso / Uno dei valori del menu a tendina
     
È possibile definire un numero arbitrario di entità di registrazione potendo quindi usufruire della massima flessibilità nella definizione dei criteri di accesso a questo servizio.

Abilitare l’accesso privacy agli utenti Kalliope
+++++
Come già detto, l’utente privacyadmin ha la possibilità di delegare agli altri utenti Kalliope l‘accesso alle informazioni di privacy e alla configurazione/consultazione delle registrazioni.
Il privacyadmin può abilitare l’accesso agli utenti Kalliope dal tab Gestione utenti selezionando la checkbox in corrispondenza dell’utente desiderato e cliccando sul tasto Abilita accesso privacy, come si può vedere nell’immagine. Allo stesso modo è possibile disabilitare l’accesso privacy per un utente precedentemente abilitato.

*jpg*

Una volta abilitato l’accesso privacy è sufficiente che l’utente acceda a Kalliope con le proprie credenziali e vedrà le nuove voci relative alla privacy direttamente nel menù operativo.
     
     
