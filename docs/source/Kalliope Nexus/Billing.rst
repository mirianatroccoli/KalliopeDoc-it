Billing
=====

Attraverso il modulo Kalliope Billing, la piattaforma Kalliope Nexus è in grado di gestire la documentazione addebiti e multi servizio.

Tariffazione
+++++++++
Il modulo "Voip Tariffazione" è diviso in due sezioni:

- Tariffazione: sezione dedicata all'impostazione delle tariffe che vengono applicate alle chiamate
- Dashboard: sezione che calcola e mostra il totale dei costi delle chiamate in base ai filtri inseriti

Struttura
...........
La sezione in questione permette di andare a creare, modificare ed eliminare tariffe che associano un valore ad ogni chiamata. Quest'ultimo punto avviene grazie alla presenza del tempo di fatturazione presente su ogni chiamata e in base alle regole impostate nella tariffa, come:

- azienda
- prefisso
- paese
- gateway
- limite gratuito
- stato
Il successivo atto di calcolo di questi costi è completamente automatico grazie all'utilizzo di cron schedulati.

La sezione possiede due principali maschere: una di visualizzazione di tutte le tariffe create ed una per la creazione o il dettaglio di ogni tariffa.

Elenco
...........
L'elenco delle tariffe mostra:

- descrizione
- data inizio e fine validità
- nome del gateway in entrata/uscita
- prefisso
- tariffa in/out
- scatto
- stato
- limite gratuito annuale (minuti)
Tariffazionetab1.png

Dettaglio:

Tariffaziontab2.png

Crea nuova tariffazione
...........
Per poter creare e configurare nuove tariffe, le quali andranno poi a dare un valore alle chiamate interessate, dalla pagina "Tariffazione" cliccare sul tasto verde "+" in basso a destra.

Successivamente, verrà visualizzata la maschera di creazione in cui dovranno essere inseriti tutti i dati necessari per la corretta applicazione della tariffa sulle chiamate, come:

- Azienda: l'azienda per cui vale la tariffa (se l'azienda è diversa o non riconosciuta, questa tariffa non sarà applicata)
- Descrizione: breve titolo che rende riconoscibile la tariffazione nell’elenco della pagina principale
- Gateway di ingresso/uscita per cui la tariffa viene applicata
- Data inizio/fine validità: periodo di validità della tariffa
- Stato: stato attuale
- Scatto alla risposta (in €)
- Tariffa uscita/entrata al minuto (in €)
- Limite gratuito annuale (minuti)
- Prefisso
- Paese: per cui vale la tariffa
Nuova triffaz.png

Una volta che tutti i campi ritenuti necessari sono stati riempiti, salvare la tariffa tramite l'apposito tasto in basso a destra.

Dopo aver salvato, le specifiche della tariffazione sono visibili ed è possibile visualizzare il consumo giornaliero diviso per:

- Chiamate in entrata
- Chiamata in uscita
- Totale
Di ognuna è possibile analizzare il tempo speso per le chiamate in entrata, il costo e il costo ipotetico (senza tariffa gratuita). In fondo si visualizza anche un rapporto tra i minuti utilizzati e i minuti totali:

Consumo tariff.jpg

Filtri
.........
Disponibili nella maschera principale, filtri (cliccare sul tasto "Ricerca") e metodi di export/import. I filtri permettono una selezione per:

- Azienda
- Range data inizio validità
- Gateway
Filtri tariff.JPG

Dashboard
+++++++++++
Una volta che le tariffazioni sono state create e attivate, l'attenzione si può spostare sulla sezione dedicata alla Dashboard dove, man mano che le chiamate entrano nel CDR e vengono valorizzate, i costi totali sono calcolati e visualizzati in base ai filtri inseriti tramite il tasto "Ricerca".

Questa sezione è strutturata in una prima parte (sopra i grafici) dove vengono visualizzati i totali di quantità, tempo e costi in modo generico. Ciò consente all'utente di avere subito le informazioni indispensabili a disposizione.

Subito dopo, sono presenti due grafici con suddivisione mensile e giornaliera.

Dashboard tariff.jpg

Per un'analisi più dettagliata dei costi generati dalle chiamate fatte/ricevute, nella seconda parte di questa sezione vengono riportate quantità, tempi e costi con suddivisione per:

- mese
- data
- organizzazione
- ente
- gateway
- operatore
- centro di costo
- divisione

A seguire alcuni esempi:

Tabella dashboard1.jpg

Tabella dashboard2.jpg

Multiservice
++++++++++
Il modulo Multiservice nasce dall'esigenza di gestire la valorizzazione delle chiamate fatturate ai propri clienti come se venisse offerto un servizio. Grazie a ciò, sarà possibile utilizzare la piattaforma contemporaneamente per:

- gestire gli addebiti per ogni chiamata attraverso il modulo "Tariffazione"
- gestire il valore delle chiamate che andranno fatturate al cliente come servizio tramite il modulo in questione
Le sezioni all'interno di questo sono due e consentono di:

- gestire manualmente i servizi offerti nel contratto
- visualizzare un report contenente le quantità e i prezzi dei servizi utilizzati, comprese le chiamate (che verranno calcolate automaticamente dal sistema)

Fatturazione
...........
In questa sezione è possibile visualizzare il report riguardante i vari servizi e le chiamate in ingresso e uscita, con i relativi costi totali che vengonp fatturati ad ogni cliente.

Struttura
..........
Il report è strutturato in modo tale che ogni azienda abbia la sua riga dedicata, con quantità e costi di ogni servizio utilizzato.

Tab 1 multiservice.png

Osservando la tabella in alto, nella prima colonna è visualizzata la ragione sociali dell'azienda, nella seconda il periodo di competenza del contratto su cui sono indicati i servizi offerti, mentre nelle colonne successive si trovano i vari servizi utilizzati:

- Totale: la quantità totale del servizio utilizzato (nel caso delle chiamate, sarà il numero totale di chiamate offerte che sono state fatte e quindi utilizzate)
- Tempo: il tempo totale di tutte le chiamate indicate nel totale
- Costo: il costo complessivo calcolato sul servizio utilizzato o sui minuti di chiamata effettuati (nel caso di chiamate)
Alla fine della visualizzazione di tutti i servizi utilizzati, si trova il costo complessivo che il cliente indicato all'inizio della riga dovrà sostenere.

Configurazione
...........
Per poter iniziare ad utilizzare questo modulo, è necessario indicare, nei vari contratti che si vanno a creare, i servizi che vengono offerti con i relativi costi. Per fare ciò, nel momento in cui si crea il contratto, alla fine di questo si troverà un tasto ( [+] nuova riga ) che dovrà essere premuto per aggiungere un servizio a quel contratto.

Una volta fatto, nei vari campi dovrà essere indicato:

- il servizio
- la tariffa del servizio
- il limite massimo di "prodotti" del servizio che il cliente non dovrà pagare
- per quanto riguarda le chiamate, anche lo scatto alla risposta
Tab 2 multiservice.png

Una volta completata questa prima configurazione, basterà indicare manualmente per ogni servizio (eccetto le chiamate) le quantità utilizzate dai vari clienti. Tutto il resto, compresa la valutazione di ogni chiamata, sarà effettuato automaticamente.

Filtri
.............
Utilizzando il sistema di filtraggio si riesce ad ottenere il meglio da questo modulo, riuscendo ad indicare facilmente, attraverso 3 campi, le aziende che si vogliono visualizzare e il periodo di tempo in cui si vuole che i calcoli vengono fatti. Si potranno trovare in alto a destra, cliccando sul tasto di ricerca.

