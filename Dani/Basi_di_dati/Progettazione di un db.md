### Metodologie  per i modelli 
	nota: capitolo 6 del libro di testo Paolo Atzeni
Un principio dell'ingegneria su cui ci basiamo per fare le basi di dati è quello di separare il cosa rappresentare in una base di dati dal "come" farlo.

Ci sono 3 fasi della progettazione
- Progettazione Concettuale: fase in cui si ottiene *schema concettuale* in cui andiamo a rappresentare  ad alto livello di astrazione, senza preoccuparci dell'implementazione, il modello concettuale dei dati e come essi sono organizzati.
- Progettazione Logica: si mantiene un certo livello di astrazione e si trasforma lo schema concettuale in uno *schema logico* basato su un modello logico dei dati (esempio relazionale). Sempre nel contesto del modello relazione si può verificare tramite **[[NORMALIZZAZIONE]]** la qualità dello schema logico ottenuto. E' ad un livello inferiore di astrazione poichè i dbms si basano su un modello logico dei dati come appunto quello relazione, ma ne astriamo dalla sua implementazione effettiva.
- Progettazione fisica: lo schema logico viene ultimato  e implementato, specificandone i parametri fisici di memorizzazione (organizzazione dei file e indici).

Un modello concettuale che usiamo è il modello ER  (Entità Relazione).

# Modello concettuale ER
Si fanno uso di diagrammi per la rappresentazione.
![[Rappresentazione grafica dei costrutti.png]]


**Entità** : Rappresentato da un rettangolo e un nome univoco che lo rappresenta. Rispetto al modello relazionale una entità può esistere anche senza saperne i suoi "attributi". Non è la tupla di attributi che fa un'entità ma è l'entità stessa.

![[Esempio di entità.png]]

**Associazioni:** Rappresentate da un rombo (poi vedremo anche dalle sue cardinalità). Non hanno un "verso" e posso essere  n-arie. Più comunemente le associazioni sono binarie, ricorsive, ternarie. Le associazioni nel modello E-R sono a tutti gli effetti un sottoinsieme del prodotto cartesiano tra le entità, la conseguenza è che non possono esserci delle *occorrenze* di n-uple ripetute.
![[associazione.png]]
in una associazione di questo tipo non si può rappresentare un esame sostenuto più volte ( si dovrebbe modellare una entità Esame)

![[associazione ternaria.png]]
![[associazione ricorsiva.png]]
Esempio di ricorsiva e ternaria


**Attributi:** Rappresentano proprietà elementari di un' entità o un'associazione. Possono essere atomici (esempio Età Nome o Cognome) o composti come ad esempio Indirizzo che è composto da via indirizzo cap civico. Si preferisce non usarli. Ogni attributo ha un suo dominio, i valori possibili, ad esempio Età può essere un numero naturale maggiore di 0 e inferiore a 100, non vengono rappresentati nello schema ma possono essere inclusi nella documentazione associata.
![[Attributi.png]]


### Esempio di schema ER con questi 3 costrutti
![[Esempio di schema ER.png]]


### Altri costrutti del modello ER
**Cardinalità di una associazione:** La cardinalità è un vincolo sull'associazione che descrive quanti entità possono essere in associazione con l'altra, ne descirve quindi il numero minimo e massimo di occorrenze a cui un'entità può partecipare. Possiamo distinguere delle associazioni uno ad uno
(0,1)(1, 1), associazioni uno a molti (1, 1) (0, N) o associazioni molti a molti (1, N) (0, N)
![[cardinalità associazioni.png]]
Questo si basa sulle associazioni binarie perchè le associazione multiple solitamente partecipano con cardinalità massima pari a N.

**Cardinalità degli attributi:** Anche gli attributi possono avere cardinalità. DI norma se non è specificata si intende che la cardinalità sia (1,1) inq uel caso si dice che è un attributo obbligatorio. Nel caso un attributo abbia una cardinalita da (0, n), quindi omettibile, si dice opzionale. Nel caso invece l'attrbuto può assumere più valori si dice multivalore. Si preferisce usarle con cautela i attributi multivalore che possono essere espressi con una associazione tra 2 entità
![[cardinalità attributi.png]]

**Identificatori:** Sono attributi che identificano univocamente un detemrinata occorrenza di un'entità. Può essere un identificatore atomico composto da un singolo attributo oppure da più attributi. Nel caso gli attributi appartengono all'entità si dicono identificatori interno (o chiave). Posso esserci identificatori esterni modellati da cioè da una relazione tra un'entità e un'altra, si dice anche che in questo caso sia una entità debole avendo bisogno di un identificatore esterno.
![[Identificatori o chiavi di un entità.png]]![[Identificatore esterno.png]]
Entità debole e identificatore esterno

**Generalizzazioni:**  Rappresentano legami logici tra entità, detta una genitore e entità figlie. Le generalizzazioni possono essere Totali, nel caso in cui l'occorrenza di entità genitore e almeno occorrenza di un'entità figlia, altrimenti si dice parziale.  Si dice anche esclusiva se l'occorenza genitore è al massimo 1 occorenza di un'entità figlia, sovrapposta al contrario
![[Generalizzazioni.png]]

La caratteristica dei genitori vengono trasferite al entità figlia senza bisogno di specificarle. Le entità figlie in più hanno attributi aggiuntivi. Si può sempre rendere una generalizzazione totale esprimendo tutti gli altri casi.

Nel capitolo 7 si mostrano molti esempi e uno schema da seguire per la proggettazione di basi di dati.

# Progettazioen Logica

La parte importante della progettazione logica è il ristrutturare lo schema ER ottenuto nella fase di modellazione concettuale. Poi si deve passare dal modello ristrotturato al modello logico.

## Ristrotturazione del  modello concettuale
Si può riassumere in queste fasi:
- Analisi delle ridondanze
- Eliminazione delle generalizzazioni
- Partizionamento/accorpamento di entità e associazioni
- Scelta degli identificatori principali

### Analisi delle ridondanze
Le ridondanze in uno schema concettuale corrisponde alla presenza di un dato che può essere derivato da altri dati. Un esempio sono dati darivati da altri tramite operazioni, un derivato da un associazione in cui il dato può essere conteggiato e associazioni derivabili dallaa composizione di altre associazioni in presenza di cicli.
![[Schemi con ridondanze.png]]
Esempi di ridondanze. Nella terza si possono contare il numero di persone in associazione per ottenere il numero di abitanti.

### Eliminazione delle generalizzazioni
Le generalizzazioni non esistono un loro corrispettivo nello modello relazionale. Queste perciò devono essere rimodellate tramite entità e relazione e ci sono 3 metodi che si possono utilizzare:
- Accorpamento delle figlie della generalizzazione nel genitore
- Accorpamento del genitore della generalizzazione nelle figlie
- Sostituzione della generalizzazione con associazioni
 ![[Esempio di schema.png]]
PRendendo come esempio lo schema 8.10 queste sono le varie ristrotturazioni 
![[Esmpi di ristroutturazioni di generalizzazioni.png]]
Il caso 1) si può utilizzare e torna comodo quando le oiperazioni eseguite sulle 2 entità non fanno distinzione.
Il caso 2) è possibile unicamente se la relazione è totale (quindi ogni elemento del genitore e almeno 1 elemento delle figlie)  e torna comodo se ci sono operazioni che si eseguono o su una o sull'altra entità.
Il caso 3) conveniente quando la generalizzazione non è totale (non necessario) e ci sono operazioni che si riferiscono solo a certe occorrenze delle entità E1 o E2 facendo distinzione tra le entità figlie e le entità genitore.

### Partizionamento/accorpamento di concetti
Partizionare un'entità in più entita, eliminare attributi multivalore, accorpare entità sono tutte le operazioni in questo punto. Di seguito una serie di esempi con commenti
![[Pasted image 20240610174958.png]]
Questa è una decomposizione verticale che divide un'entità in due sotto entità con i suoi attributi. In questo caso probabilmente nella nostra applicazione non utilizzeremo nelle operazioni tutti i dati dell'impiegato ma solo una sua sottoinsieme di essi. (notare come andiamo ad introdurre una generalizzazione a livello logico)

![[Pasted image 20240610174950.png]]
GLi attributi multivalore come già detto prima non sono presenti nel modello relazionale e quindi vanno rimodellati.

![[Pasted image 20240610175011.png]]
Nella nostra applicazione le operazioni che andremo ad eseguire richiederanno spesso accessi all'entità appartamento quindi per ridurne il carico sul sitema le accorpiamo.

## Traduzione verso il modello relazionale
![[Pasted image 20240610181015.png]]
![[Pasted image 20240610181024.png]]
con rinominazione di PARTECIPAZIONE
![[Pasted image 20240610181037.png]]


![[Pasted image 20240610181045.png]]
![[Pasted image 20240610181052.png]]


![[Pasted image 20240610181106.png]]
![[Pasted image 20240610181113.png]]


![[Pasted image 20240610181134.png]]
Entità con identificatore esterno
![[Pasted image 20240610181148.png]]


![[Pasted image 20240610181211.png]]
![[Pasted image 20240626110332.png]]
Varie opzioni

Questa fase è meccanica una volta completata la ristrotturazione e i sistemi CASE (Computer-aided software engineering) possono farlo in automatico.