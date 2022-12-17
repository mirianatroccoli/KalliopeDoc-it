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
+------+---------------+---------------+
| Item | Character     | Prova         |
+======+===============+===============+
| 1    | Prova         | Prova         |
+------+---------------+---------------+
| 2    | Prova         | Prova         |
+------+---------------+---------------+


To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache

