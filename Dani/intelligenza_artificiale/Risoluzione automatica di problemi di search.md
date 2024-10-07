### Il search 
I problemi di **search** sono tendenzialmente caratterizzati da essere risolvibili tramite delle inferenze, un algoritmo per intenderci.
Qui non intendiamo strettamente "ricerca" ma quanto più il "cercare" un dato oggetto in un set di oggetti. (un problema di lingua che non esprime bene il concetto di **search**)

Assunzioni per questi problemi:
1) Singolo agente
2) Ambiente osservabile (vedi [[Intro agli agenti autonomi]])
3) Ambiente deterministico

##### Come descrivere il problema
S = {s1, s2, s3....} spazio degli stati, assumendo che sia finito
sI è lo stato iniziale e descrive l'ambiente e lo stato dell'agente all'inizio
sg stato di goal (assumiamo sia 1 per semplicità)

A(si) = {a, b. c...} insieme di azioni possibili in uno stato

La funzione f(si, a) rappresenterà lo stato di arrivo a partire da uno stato si e una azione a.

La transizione da uno stato all'altro può causare un costo additivo che descriveremo come una funzione c(si, a, f(si, a)). Chiameremo questa tripletta *transizione*. 

Possiamo rappresentare il tutto con dei grafi e dei nodi in cui da un nodo partono gli archi pari alle possibili azioni.

##### I tipi di problemi
Una volta descritto il problema analizziamo se esistono delle soluzioni e quali tipi di soluzioni.

Classifichiamo 3 classi di problemi:
1) Fattibilità: esiste un percorso di uscita? 
2) Ottimizzazione: esiste un percorso di uscita? Quale è quello con il minimo numero di azioni?
3) Approssimazione: accetto qualsiasi soluzione valida che sia al più *p* volte peggiore di quella migliore


Certi problemi non possiamo descriverli del tutto e quindi utilizzeremo un approccio implicito, ovvero specifichiamo lo stato iniziale e la funzione di transizione in una forma compatta. Il grafo degli stati sarà "svelato" man mano che le azioni vengono valutate. Questo è un esempio sul cubo di rubick che ha una quantità di stati nell'ordine dei quintilioni quindi impossibili da rappresentare in modo **esaustivo**.

### Algoritmi di ricerca: caratteristiche generali
Definizione: Un algoritmo di ricerca esplora il grafo degli stati fino a quando non trova la soluzione desiderata

L'algoritmo deve restituire il percorso che ha fatto per arrivare al goal. Lo rappresenterà attraverso un sotto grafo detto albero di ricerca (un albero è un grafo aciclico)

#### Proprietà e come valutare
Si valuta l'algoritmo di ricerca su :
1) Correttezza. L'algoritmo deve restituire una soluzione a ciò che sto cercando sempre.
2) Completezza o Sistematicità.  Garanzia che se una soluzione esiste allora l'algoritmo la trova **sempre**. Per dimostrarlo dobbiamo dimostrare che dato un tempo arbitrariamente lungo l'algoritmo visiti tutto il grafo negli stati possibili. Se lo spazio degli stati è infinito, non si parla di completezza ma di sistematicità.
3) Complessità in termini di spazio
4) Complessità in termini di tempo (o passi)
Sono caratteristiche generali che non si applicano esclusivamente agli algoritmi di ricerca.

#### Come funzionano
In generale un algoritmo di ricerca risponde a questa domanda :
"Dato quello che ho ispezionato fino ad ora, dove proseguire con la ricerca?"

Diversi algoritmi hanno diverse "regole" per rispondere a questa domanda

##### Depth First Search
Una ricerca DFS, sceglie il nodo più profondo non ancora esplorato nell'albero di ricerca.
Si espande tramite il modello di transizione dell'ambiente. Se ci troviamo in un caso di tie-break, si ripete il processo ma arbitrariamente. (esempio ordine lessicografico)
Concediamo la possibilità di backtracking.

Complessità spaziale O(d)
Complessità temporale O(b^d) (esponenziale in base a d, profondità massima di una soluzione e b numero massimo di azioni disponibili in uno stato.)
