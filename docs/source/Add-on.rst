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
   * - Utenti abilitati (lista)
     -  
     -  
   * - Utente
     - Utente a cui assegnare un permesso
     - Dropdown 
   * - Permesso
     - Permesso da assegnare all’utente
     - Solo ricezione / Solo invio / Invio e ricezione
   * - Template
     -  
     -  
   * - Template istanza FAX
     - Template da utilizzare per la configurazione dell’istanza
     - Dropdown

