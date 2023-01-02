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




Descrizione interfaccia
------------




Configurazione servizi
------------


