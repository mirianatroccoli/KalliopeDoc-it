Servizi telefonici tradizionali
=====

Call Hold and Music on Hold
----------

Per mettere la chiamata corrente in attesa, si opera sul corrispondente tasto funzione presente sul terminale telefonico; in base al modello specifico il tasto può essere un tasto fisico dedicato (normalmente indicato con “Hold”) oppure essere uno dei tasti dinamici.


Call Pickup
-------

Descrizione del servizio
+++++
Questo servizio consente ad un utente del centralino di prelevare la chiamata diretta ad un altro interno.
Nel caso in cui stia squillando un determinato interno, ma l’utente chiamato non può o non vuole rispondere alla chiamata, un altro utente può, dal proprio telefono, rispondere alla chiamata piuttosto che recarsi fisicamente a rispondere presso il telefono che sta squillando.
Il prelievo di chiamata diretto si applica a tutte le chiamate destinate all'interno, anche quelle ricevute in quanto membro di un gruppo di chiamata o di una coda.

Il KalliopePBX mette a disposizione due modalità di prelievo:

- diretto: l'utente che effettua il prelievo non ha alcuna informazione sul chiamante originale
- con invito: l'utente che effettua il prelievo verifica il chiamante originale prima di decidere se completare o meno il trasferimento

Operativamente il prelievo diretto viene effettuato digitando il codice di prelievo di chiamata diretto (default **) seguito dal numero di interno del destinatario originale della chiamata.
L'utente che ha effettuato il prelievo viene messo direttamente in comunicazione con il chiamante originale.

Nel caso di prelievo con invito invece il prelievo avviene digitando il codice di prelievo di chiamata diretto (default #*) seguito dal numero di interno del destinatario originale della chiamata.
L'utente che sta effettuando il prelievo riceve prima un segnale di riaggancio e successivamente una chiamata in ingresso che mostra come chiamante il chiamante della chiamata che si intende prelevare.
A questo punto l'utente che sta effettuando il prelievo può decidere se completare il trasferimento (rispondendo alla chiamata) o meno (rifiutando la chiamata).
Solo nel momento in cui il trasferimento viene completato il destinatario originale smette di squillare.


Configurazione del servizio
+++++
Il servizio può essere abilitato / disabilitato nel pannello PBX -> Piano di numerazione
Il codice del servizio può essere modificato nel pannello PBX -> Piano di numerazione

Interoperabilità con dispositivi di terze parti
+++++++
Nel caso in cui si voglia utilizzare questo servizio può essere molto utile avere a disposizione un tasto (con campo lampade) che consenta di verificare lo stato dell'interno su cui vogliamo effettuare il prelievo.
Per quanto riguarda il monitoraggio, il KalliopePBX invia dei messaggi SIP NOTIFY per comunicare i cambi di stato dell'interno. Il telefono dovrà inviare una SIP SUBSCRIBE per richiedere l’invio delle informazioni di stato. Questa operazione è normalmente effettuata configurando un tasto funzione di tipo BLF.
Oltre a monitorare lo stato dell'interno molti telefoni consentono con lo stesso tasto di effettuare anche il prelievo di chiamata sull'interno. In questo caso nella configurazione del tasto deve essere indicato il codice di prelievo chiamata

Esempi di configurazione
+++++

**Su SNOM** -> Operando tramite la web gui di configurazione configurare Function keys con:

.. code-block:: console

   Account: selezionare dalla tendina l’account che stiamo utilizzando (se c’è un solo account configurato sul telefono è il primo della lista)
   Type: BLF
   Value: <interno>|**
  
In alternativa modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   <fkey idx="%%id%%" context="%%line_id%%" label="" perm="">blf sip:<interno>@%%KPBX_IP_ADDRESS%%;user=phone|**</fkey>

dove %%id%% è l’identificativo del tasto da configurare e %%line_id%% è l’identificativo dell’account associato (il valore è 1 se sul telefono è presente un solo account).

Esempio:

.. code-block:: console

   <fkey idx="0" context="1" label="INTERNO103" perm="">blf sip:103@192.168.23.190;user=phone|**</fkey>
   
**Su YEALINK** -> Operando tramite la web gui di configurazione configurare DSS Key con: 

.. code-block:: console

   Type: BLF
   Value: <interno>
   Line: La linea associata all’account che stiamo utilizzando (Line 1 se sul telefono è presente un solo account)
   Extension: **
   
Oppure modificando direttamente il file di configurazione o il template in questo modo:

.. code-block:: console

   memorykey.%%id%%.line=%%line_id%%
   memorykey.%%id%%.value=<interno>
   memorykey.%%id%%.type=16
   memorykey.%%id%%.pickup_value=**

Dove %%id%% è l’identificativo del tasto da configurare e %%line_id%% è l’identificativo dell’account associato il valore è 1 se sul telefono è presente un solo account).

Esempio:

.. code-block:: console

   memorykey.1.line = 1
   memorykey.1.value = 103
   memorykey.1.type = 16
   memorykey.1.pickup_value=**

Nel caso si intenda configurare il prelievo con invito è necessario sostituire il codice di prelievo diretto (**) con quello di prelievo con invito (#*).









