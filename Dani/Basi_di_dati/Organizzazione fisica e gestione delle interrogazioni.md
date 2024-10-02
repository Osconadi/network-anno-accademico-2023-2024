 La base di dati sfrutta certe componenti del file system fornito dal sistemi operativo. Esistono delle possibilità in cui in futuro più funzioni del sistema operativo possano essere già orientate alle basi di dato.

La cosa importante da ricordare è il fatto che le tabelle non possono essere caricate tutte in memoria centrale essendo essa limitata ma quindi dovranno risiedere in memoria secondaria  in strutture a blocchi(dischi, ssd ecc) ed è quindi importante utilizzare al meglio il **buffer** che trasporta i blocchi necessari in cui risiedono i dati. Possiamo dire che una volta che i dati sono arrivati in memoria centrale il costo delle operazione è trascurabile rispetto al tempo che impiega la memoria secondaria nel trovare il blocco giusto e copiarlo nel buffer. (Ricorda: le operazioni più costose in termini di interrogazioni sono le select e i join)

#### In breve il buffer
La struttura del buffer è gestita a pagine, che corrispondono alla dimensione di un numero intero di blocchi. La sua gestione è simile alle politiche di gestione della memoria centrale dei sistemi operativi. Per mantenere il numero di cambi di pagine al minimo si mantiene il principio di località dei dati in cui si assume che i dati recentemente usati saranno probabilmente richiamati in futuro, facendo in modo da avere solamente le pagine maggiormente usate all'interno del buffer.

### La gestione dei dati fisici
Quando portiamo un blocco in buffer nella pagina andiamo a prendere sia i dati veri e propri sia dei dati di controllo, che discrovono come arrivare ad ottenere i dati veri.
Qui descritto la struttura di una pagina:
![[Pasted image 20240613162800.png]]
Il block header e il block trailer, rispettivamente all'inizio e alla fine della pagina contengono informazioni di controllo utilizzate dal file system.
Il page header e il Page trailer contengono informazioni sulla struttura fisica, ovvero descrive come è fatta la struttura fisica dell'oggetto o strutture dati associate per accedere ai dati.
Il bit di parità che indica se la pagina è correntemente valida o meno.

##### Blocking factor
Un fatttore importante da ricordare è il blocking factor (bfr)
![[Pasted image 20240613163219.png]]
dal bfr possiamo ricavarci il numero di blocchi necessari per un file invertendo la formula

#### Strutture primarie per l'organizzazione dei file
Esistono varie varianti per l'organizzazione dei file:
- sequenziale
- calcolato
- ad albero

Le strutture sequenziali a loro volta si suddividino in dati ordinati, non ordinati e array.
##### La Struttura non ordinata
anche detta **seriale o disordinata** sono le più semplici poichè i record vengono inseriti nel file nell'ordine in cui questi si presentano. Vengono detti **heap***, o mucchi, implicando che i record arrivano senza essere toccati o sistemati secondo un ordine.
**L'inserimento** di nuovi record è molto efficente poichè necessità solamente di un puntatore all'ultimo elemento inserito. 
Il suo svantaggio deriva dalla ricerca, che richiede di scandire alla peggio ogni elemento, il costo della ricerca è lineare al numero di blocchi del file in questo senso. 
Da sole questo strutture possono essere usate ma spesso sono supportate da strutture secondarie per favorire gli accessi.

Per la modifica e l'eliminazione dei dati basta trovare il dato e marcarlo o modificarlo direttamente, senza riorganizzare la struttura stessa.

##### Struttura sequenziale ad array
Possibile solamente se le tuple di una tabella sono di dimensione fissa. Se soddisfatta questa condizione si associa un numero n di blocchi contigui e ciascun blocco è dotato di un numero m di "posizioni" disponibile per le tuple, creando un array n x m in cui ciascuna tupla è associata un indice i all'interno di esso.
Gli inserimenti e le ricerche sono efficienti avendo a disposizione l'indice della tupla che si sta cercando. (Un costo costante)

##### Struttura sequenziale ordinata
Detta anche **clustered**, prevede la memorizzazione dei record secondo un ordinamento fisico coerente con l'ordinamento di un campo detto chiave (in alcuni testi detto **pseudochiave**), che può essere composto da più attributti. Nel caso di parità di ordinamento sul primo si procede al secondo e così via. Seppur queste siano strutture ordinate è difficile fare una ricerca dicotomica perchè non sempre si hanno accesso a tutte le informazioni del file (per intenderci non abbiamo tutti i blocchi caricati), quindi queste strutture sono utilizzate in stretta associazione con indici.
Le selezioni su intervalli sono semplici avendo gli intervalli memorizzati contiguamente, basta trovare il primo membro e poi si hanno di conseguenza gli altri consecutivamente. In modo analogo se si fanno operazioni aggregate e l'ordinamento e sui campi di aggregazione queste sono più semplici.
Le eliminazioni potrebbero portare a spreco di spazio mentre gli inserimenti potrebbero causare la necessità di avere un file di "overflow" in cui non solo si perde la contiguità dell'ordinamento ma richiede spazio aggiuntivo. Per ovviare a questi problemi si fanno delle periodiche riorganizzazioni.

##### Strutture con accesso calcolato (funzioni di hash)
Basandosi sul valore di una pseudochiave si esegue una funzione hash che calcola una chiave, garantendo un accesso associativo ai dati. Un esempio pratico di quando viene utilizzato questo tipo di accesso rispetto ad un array: considerare le matricole degli studenti composte da 6 cifre (TANTI casi possibili), se volessimo memorizzare solo un sottogruppo, una classe ad esempio di 40 persone, sarebbe molto inefficente assegnare un array grande quanto tutti i casi possibili. Si decide quindi di usare meno spazio, ad esempio assegnamo 50 spazi per la memorizzazione e calcoliamo gli indici per su questi 50. Una dei problemi della funzione hash è la possibilità di collisioni di indice che diminuiscono al crescere dello spazio che allochiamo rispetto al numero che ci aspettiamo di riempire (si dice fattore di riempimento nel caso precedente 40/50 = 0.8). Per gestire le eventuali collisioni, che comunque possono accadere, possiamo allocare un blocco aggiuntivo collegato al precendente e il record che causa questa operazione viene messo all'interno. Questa operazione è ricorsiva, si vanno quindi a creare **catene di overflow**.
![[Pasted image 20240614094547.png]]
Accesso puntuale, quello relativo ad uno specifico valore della chiave, lo possiamo considerare con costo quasi unitario , costante, in questo campo è molto vantaggiosa la funzione hash, al contrario degli accessi su intervalli che non è dato che valori simili siano adiacenti nel blocco, anzi molto spesso sono su blocchi differenti.
Una limitazione della struttura hash è la sua scarsa dinamicità, su file che crescono si perde l'efficenza e bisognerà riorganizzare il file allocando un maggior numero di blocchi e o una diversa funzione hash. 

	piccola nota per quanto riguarda il testo che specifica che esistono strutture hash capaci di evolversi dinamicamente ma di cui non è trattato nulla.

#### Struttura ad albero o indici
Le strutture ad albero anche dette indici, sono  strutture che permettono l'accesso in base a un valore di uno o più campi , come per le funzioni hash, mantenendo  l'efficenze negli accessi puntuali ma anche a intervalli di valori.

Distinguiamo gli indici in strutture primarie che contengono i dati (record) e strutture secondarie che favoriscono gli accesso ai dati senza però avere i dati stessi. ( strutture di supporto/ausiliarie)
Gli indici sono formati da una coppia di campi  K, la pseudochiave su cui viene fatto l'ordinamento, ed il valore p che è il puntatore ad un'area di memoria.

##### Indici primari
Negli indici primari il valore p punta o all'inizio del blocco o ad un valore massimo o minimo nel blocco. Sono caratterizzati spesso dall'essere **sparsi**  ovvero non compaiono tutti i valori della pseudochiave ma solo alcuni. 
Se abbiamo n blocchi il nostri indice primario sarà composto da n elementi, uno per ciascun blocco.
![[Pasted image 20240614101302.png]]
![[Pasted image 20240614101438.png]]
Due esempi di indici primari
Può esistere un unico indice primario (pensare ad un indice di un libro)

##### Indici secondari
E' una struttura dati di supporto all'indice primario. Qui le chiavi possono essere non ordinate , ordinate (non rispetto al campo di indicizzazione secondaria) o calcolate tramite hash.
Gli indici secondari devono per forza essere **densi**, ovvero contenere ogni valore del campo che stiamo considerando
Il campo k che stiamo considerando può essere anche su campi non chiave, a quel punto possiamo procedere con tre opzioni per memorizzare:
- inserire più volte il medesimo valore k
- Record a lunghezza variabile con più puntatori
- Un ulteriore livello che contiene 

![[Pasted image 20240614102612.png]]
Esempio con ulteriore livello

Un file può avere più indici secondari (pensare ad esempio a indici analitici  o a diversi indici in guide turistiche, una per i ristoranti una per gli hotel ecc...)

##### Veloci considerazione sugli indici in confronto alle hash
C'è da notare che le funzione hash sono quasi impareggiabili per l'efficenza negli accessi puntuali. Gli indici essendo implementati tramite alberi avranno, ed essendo essi ordinati anche, avranno un tempo di ricerca logaritmico (pensare alla ricerca dicotomica) in base al numero di blocchi, seppur questi permettono dei vantaggi per quanto riguarda accessi su intervalli.

	Nota del libro: viene fatto notare come questa differenza è man mano minore dato la maggior capacità della memoria centrale che permette buffer di grandezza maggiore e quindi riducendo la disparità tra accesso via indici e hash.

Altre considerazioni sono il fatto che gli indici sono di gran lunga più piccoli rispetto al file stesso

##### Le Strutture ad albero, i b-tree e i b-tree+ (balanced tree)
Le strutture ad albero sono caratterizzate dall'essere bilanciati, per mantenere la profondità al minimo e quindi un accesso medio ai dati minore.

Ogni nodo dell'albero deve contenere sia dei puntatori *p* sia dei valori *Ki*
![[Pasted image 20240614104315.png]]

Gli **alberi di ricerca** contengono al massimo p-1 puntatori ( se p = 3 allora ogni nodo potrà avere al massimo 3-1=2 puntatori)
All'interno del nodo i valori Ki sono ordinati in modo per cui K1< K2< K3 ecc..

![[Pasted image 20240614104522.png]]
Albero con p=3 

![[Pasted image 20240614104837.png]]
Esempio di albero con puntatori e file dati a cui puntano
Ogni elemento nel nodo è caratterizzato dai Puntatori dai valori K della chiave contenente il riferimento al blocco a cui si trova il dato

		hP1,(hK1, Pr1i), P2,(hK2, P r2i), . . . ,(hKq−1, P rq−1i), Pqi,

Il problema sorge quando dobbiamo andare ad inserire nuovi valori all'interno dell'albero  che per mantenere il bilanciamento dovrà effettuare eventuali operazioni di divisione sul nodo che si estende ricorsivamente ai livelli superiori.


Gli alberi B-tree+ si differenziano dai b-tree  normali perchè nei livelli intermedi contengono alcuni valori di k mentre i puntatori ai dati si trovano solamente nei nodi foglia dell'ultimo livello. Inoltre nei nodi foglia si hanno dei puntatori che puntano direttamente alla foglia successiva
Apparentemente i B+ possono apparire più svantagiosi visto che non ci sono puntatori diretti ai dati nei nodi intermedi. Questo è controbilanciato dal fatto che nei nodi intermedi sono memorizzati più puntatori che comportano un vantaggio in termini di accesso al disco necessari per attraversare l'albero. Combina i vantaggi di un indice multivello (creare più indici primaria più livelli) con i vantaggi dell'accesso sequenziale indicizzato
![[Pasted image 20240614110126.png]]
esempio di B+

		nota: tutta questa parte sui b-tree non è nelle slide di montanelli ed è preso dal libro


#### Conclusione sulla progetta fisica
La progettazione fisica è l'ultima parte di progettazione e si occupa del decidere come ogni singola relazione viene memorizzata. Per fare ciò si ragione sulla struttura dello schema logico e i tipi di relazione e tipi di dati che abbiamo, ragioanando anche in ottica di quali possibili operazioni possano essere eseguite e il loro carico sul sistema.

Queste sono anche scelte basate sul sistema e quello che ci viene fornito dal DBMS a nostra scelta.
Nello standard SQL non si è ancora rggiunto un accordo su quali comandi fornire o uno standard per la progettazione fisica essendo essa difficilmente uniformabile. A livello commerciale ci vengono forniti questi insieme di comandi
![[Pasted image 20240614110942.png]]
![[Pasted image 20240614110954.png]]
La "ListaAttributi" e quella su cui si eseguono gli ordinamenti, facendo prima l'ordinamento sul primo della lista, in caso di parità sul secondo e così via.