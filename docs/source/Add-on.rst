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
   Successivamente è necessario configurare la specifica istanza FAX nel pannello FAX → Istanze FAX. Nel pannello Istanza FAX sono definiti gli attributi associati ad    un’entità FAX. Un’istanza FAX deve corrispondere ad una selezione del piano di numerazione (come un interno), deve avere un nome e impegnare un canale di una          licenza Kalliope FAX Module.
   *jpg*
---------------------------+----------------------------------------------------------------------------------------+-------------------------------------------+


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
