API Rest
=====

Descrizione generale
--------

KalliopePBX offre un set di API REST che possono essere invocate da sistemi esterni per compiere azioni di tipo dispositivo (es. creazione di un interno, generazione di un backup e download, ecc.) o di consultazione (download del registro chiamate, ecc.).

L'accesso alle API può avvenire tramite HTTP o HTTPS, previa autenticazione, secondo il meccanismo descritto di seguito.

Meccanismo di autenticazione
---------

Il meccanismo di autenticazione delle API REST utilizza le stesse credenziali utente valide per l'accesso web. In particolare, ogni richiesta deve contenere un HTTP header custom, monouso, il cui nome è X-authenticate. La procedura di autenticazione è one-way, ossia non richiede l'invio di un challenge da parte del server, ma tutte le informazioni necessarie all'autenticazione sono generate esclusivamente lato client.

La proprietà di uso singolo dell'header di autenticazione previene gli attacchi per duplicazione, garantendo che la conoscenza dell'header X-authenticate di una certa richiesta non permetta di effettuarne un'altra illecita.


Costruzione dell'X-authenticate header
+++++

L'header è composto da una serie di dati in chiaro ed un digest costruito utilizzando tali dati, unitamente alla password dell'utente che effettua la richiesta. Di seguito un esempio di un X-authenticate header completo:

.. code-block:: console

    X-authenticate: RestApiUsernameToken Username="admin", Domain="default", Digest="+PJg7Tb3v98XnL6iJVv+v5hwhYjdzQ2tIWxvJB2cE40=", Nonce="bfb79078ff44c35714af28b7412a702b", Created="2016-04-29T15:48:26Z"
    
I dati che sono utilizzati (e trasmessi nella richiesta) nella costruzione dell'header sono:

- **Username**: lo username dell'utente (es. admin)
- **Domain**: il dominio del tenant di appartenza dell'utente. Nel caso di sistemi mono-tenant, il dominio predefinito è "default"
- **Nonce**: una stringa casuale esadecimale generata dal client , di lunghezza almeno pari a 8 caratteri. Ad ogni richiesta è necessario rigenerare un nuovo nonce, in quanto il sistema tiene traccia di tutti quelli utilizzati in precedenza, per un periodo pari al tempo di validità del nonce, che è pari a 5 minuti. Dopo 5 minuti è possibile riutilizzare un nonce utilizzato in precedenza; la protezione da attacchi basati su replica è in questo caso garantita dal timestamp di creazione del nonce
- **Created**: indica il timestamp di creazione del nonce; se l'ora di ricezione della richiesta differisce dall'ora impostata sul KalliopePBX per più di 5 minuti, la richiesta viene considerata invalida e rifiutata. Questo garantisce che il riuso di un X-authenticate header con lo stesso nonce non sia possibile né entro i 5 minuti del tempo di vita di un nonce (per la protezione da replica implementata) né oltre tale tempo di vita. Il formato della stringa del timestamp (riportato al timezone UTC) è "YYYY-MM-DDThh:mm:ssZ".

Il campo Digest è un hash dei dati sopra descritti e della password dell'utente, e si calcola applicando la funzione di hash sha256 alla concatenazione delle stringhe Nonce, digestPassword, Username, Domain e Created (concatenazione delle stringhe senza delimitatori):

.. code-block:: console

   Digest = sha256(Nonce + digestPassword + Username + Domain + Created)

Dato che sul KalliopePBX le password utente non sono salvate in chidigestPassword = sha256(password{<salt>})
aro ma sotto forma di hash non reversibile, per la generazione del Digest è necessario utilizzare l'hash della password con la stessa procedura utilizzata nel PBX (indicata come digestPassword) e non la password in chiaro.

La procedura di calcolo della digestPassword richiede, oltre alla password dell'utente, una ulteriore stringa denominata salt, univoca per tenant. Il salt può essere ottenuto dal KalliopePBX mediante una API REST apposita, invocabile in modo anonimo (senza autenticazione):

.. code-block:: console

   rest/salt/<dominio_tenant>
   
dove la stringa <dominio_tenant> ,nel caso di macchina single tenant, vale "default". Nel caso di sistema multi-tenant, per poter utilizzare le API a disposizione di pbxadmin, è possibile ottenere il salt relativo mediante l'API

.. code-block:: console

   rest/salt/pbxAdmin

La formula di calcolo della digestPassword è (i caratteri { e } fanno parte della stringa di cui si esegue lo sha256 e devono essere inseriti):

.. code-block:: console

   digestPassword = sha256(password{<salt>})

Ad esempio, supponendo che la password dell'utente sia "admin" e il salt sia uguale a "b5a8fdcf2f8d5acdad33c4a072a97d7a", la digestPassword risultante è:

.. code-block:: console

   digestPassword = sha256(admin{b5a8fdcf2f8d5acdad33c4a072a97d7a}) = dd7b0be7fa37d6cbaf0b842bf7532f229cb79ab8d54d509c2aa7eea27a53cd5e
   
Come esempio, con i dati seguenti:

.. code-block:: console

   Nonce: bfb79078ff44c35714af28b7412a702b
   digestPassword: dd7b0be7fa37d6cbaf0b842bf7532f229cb79ab8d54d509c2aa7eea27a53cd5e
   Username: admin
   Domain: default
   Created: 2016-04-29T15:48:26Z   
   
si ottiene:

.. code-block:: console

   Digest = base64(sha256binary(bfb79078ff44c35714af28b7412a702bdd7b0be7fa37d6cbaf0b842bf7532f229cb79ab8d54d509c2aa7eea27a53cd5eadmindefault2016-04-29T15:48:26Z))
   
   
che vale +PJg7Tb3v98XnL6iJVv+v5hwhYjdzQ2tIWxvJB2cE40=.

NOTA: la funzione sha256binary(..) indica la funzione sha256(..) che restituisce l'output in formato binario e non in formato esadecimale.

La stringa completa risultante da inserire all'interno dell'header X-authenticate è quindi quella indicata all'inizio del paragrafo e riportata di seguito:

.. code-block:: console

   X-authenticate: RestApiUsernameToken Username="admin", Domain="default", Digest="+PJg7Tb3v98XnL6iJVv+v5hwhYjdzQ2tIWxvJB2cE40=", Nonce="bfb79078ff44c35714af28b7412a702b", Created="2016-04-29T15:48:26Z"   
  
Elenco API
----
La lista dettagliata e aggiornata delle API è consultabile direttamente tramite l'interfaccia web di KalliopePBX all'indirizzo

.. code-block:: console

   http[s]://KALLIOPE_IP_ADDRESS/api/doc 

A partire dalla versione firmware 4.9.4 è disponibile inoltre una **collection Postman** (che sostituisce la sandbox integrata all'interno della pagina di documentazione); tale collection integra anche il codice per aggiungere automaticamente l'header di autenticazione richiesto (è necessario solo impostare l'indirizzo IP del PBX e le credenziali username/password dell'utente con cui invocare l'API).

Accedendo alla KalliopeTribe è disponibile un video che mostra l'utilizzo di tale collection per invocare in modo rapido le API di Kalliope.

E' possibile scaricare il file di collection per le varie versioni firmware dai seguenti link:

- `Collection Postman per firmware 4.9.4 - 4.9.8 <https://www.kalliopepbx.com/wiki/KalliopePBX%20API%204.9.4.postman_collection.json.zip/>`_
- `Collection Postman per firmware 4.9.9 o superiori <https://www.kalliopepbx.com/wiki/KalliopePBX%20API%204.9.9.postman_collection.json.zip/>`_
- `Collection Postman per Modulo Hotel, firmware 4.9.9 o superiori <https://www.kalliopepbx.com/wiki/Hotel%20API%204.9.9.postman_collection.zip/>`_
- `Collection Postman per KalliopeLAM, firmware 4.11.3 o superiori <http://www.kalliopepbx.com/wiki/KalliopeLAM.postman_collection_4_11_3.zip/>`_



E' inoltre disponibile il file con la specifica swagger delle API, sempre scaricabile dal KalliopePBX, all'indirizzo:

.. code-block:: console

   http[s]://KALLIOPE_IP_ADDRESS/api/doc.json

Manuale per le API relative al CDR
---------
Dal momento che le API relative al CDR sono le più comunemente utilizzate abbiamo realizzato un semplice documento di approfondimento su questa famiglia di API.
E' possibile scaricare il documento da questo link.

Classi per la generazione degli header di autenticazione
---------
Di seguito un elenco di progetti in vari linguaggi di programmazione per la generazione e validazione degli header di autenticazione.

- `phpRestApiUtils <https://github.com/NetResultsIT/phpRestApiUtils/>`_: implementazione in PHP
- `RegEx <https://regex101.com/r/IEgL5V/1/>`_: espressione regolare utile per validare gli header generati


   
   
   
   
