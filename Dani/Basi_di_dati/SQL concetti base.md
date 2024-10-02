		Capitolo 4 del libro di Atzeni

### Domini Elementari
Character permette di rappresentare  stringhe o singoli caratteri
![[Pasted image 20240612163559.png]]

Tipi numerici esatti
![[Pasted image 20240612163908.png]]
scala per numeric è opzionale al contrario che per decimal
La precisione indica da quante cifre è composto il numero

Per i numeri reali usiamo invece questi
![[Pasted image 20240612164009.png]]

Lo standard SQL fornisce anche dei tipi per la rappresentazione di dati temporali, sia di intervalli sia di istanti.
![[Pasted image 20240612164117.png]]
![[Pasted image 20240612164127.png]]

Altri tipi introdotti in SQL 3 sono:
- Booleani (true o false)
- Bigint 
- BLOB e CLOB che sono utile per dei file binary molto estesi o stringhe molto estese (tipo un capitolo di un libro). Rispettivamente **Binary Large Object** e **Character large object**. Il sistema lo memorizza solo senza poterci eseguire query.

### Create tables e create schema

Lo schema è una collezzione di oggetti, tra cui tabelle, domini e viste.

![[Pasted image 20240612164837.png]]

Per creare una tabella invece usiamo questa funzione in cui andiamo poi a specificare quale sia l'attributo della primary key, i vincoli sugli attributi ecc
![[Pasted image 20240612164950.png]]

Più in generale questa è la sua sintassi
![[Pasted image 20240612165003.png]]

#### Domini
Possiamo specificare noi un dominio tramite una funzione SQL
![[Pasted image 20240612165213.png]]

questo ci permette di ripetere senza definire ogni volta i vincoli un dominio su attributi simili.

Vediamo anche come il valore di default lo possiamo definire noi
![[Pasted image 20240612165358.png]]
![[Pasted image 20240612165412.png]]


### Vincoli intrarelazionali
#### Not Null
Il valore nulla è un particolare valore assegnato quando mancano informazioni, e supera determinati vincoli di attributo. Quando un valore ha come vincolo *not null* vogliamo intendere che il valore non potrà assumere il valore nullo
#### Unique
Si applica un vincolo di unique su un attributo o su più attributi  per intenderli come (super)chiave. Il valore *null* non viola questo vincolo e può comparire su più righe.
Esempio:
![[Pasted image 20240612165801.png]]

#### Primary key
Va ad indicare un attributo o più attributi come chiave primaria ed implica un vincolo di *not null*. Può essere espressa come nella sintassi di prima con 
	primary key (Attr1, Attr2)

### Vincoli Interrelazionali

IL più comune dei vincoli interrelazionali è il vincolo di *foreign key* o chiave esterna, ovvero un attributo che referenzia dei valori di un'altra tabella. I valori referenziati devono essere parte della chiave primaria.
![[Pasted image 20240613093230.png]]

Dobbiamo definire cosa avviene quando il valore referenziato dalla tabella cambia
![[Pasted image 20240613094026.png]]
queste si applicano sia che il valore venga eliminato o modificato
![[Pasted image 20240613094140.png]]
### Interrogazioni base in sql
Una interrogazione in sql è solitamente formata da queste tra clausale:
- select
- from
- where
![[Pasted image 20240613094720.png]]
*as* indica che stiamo rinominando lo stipendio e lo mostriamo come Salario

#### Clausola select
Select specifica gli elementi/attributi dello schema che mostriamo nel risultato. 
*select* 'asterisco' indica che selezione tutti gli attributi della tabella nella clausola from

Nella select possono comparire delle espressioni generiche sul valore degli attributi.
![[Pasted image 20240613095036.png]]

#### Clausola from
Per interrogazione che richiedono dati da più tabelle le andiamo a specificare nella *from* .
![[Pasted image 20240613095622.png]]
Nella *select* andiamo a specificare prima del nome dell'attributo da quale tabella viene estratto il dato.

#### Clausola where
Ammette come argomento uno espressione composta dagli operatori *and, not, or* e dalle uguaglianze e disuguaglianze.
![[Pasted image 20240613100003.png]]
Oltre a questi predicati di confronto relazionali, SQL fornisce il predicato *like* per il confronto di stringhe. Nel predicato like compaiono i caratteri speciali "underscore" e "%" che rispettivamente rappresentano un qualsiasi carattere e una stringa qualsiasi 
![[Pasted image 20240613100442.png]]
indica una qualsiasi stringa che inizia con "ab" seguito da una qualsiasi stringa (anche nulla) e prima dell'ultimo carattere (segnato dal trattino) è preceduto da ba


### Altri concetti di sql
#### Distinct
Al contrario dell'algebra relazione in cui elementi duplici non possono comparire, in sql questo non è automatico. Se vogliamo mostrare valori non duplicati di una tabella mettiamo nella *select* prima dell'attributto il *distinct* 
![[Pasted image 20240613100949.png]]
![[Pasted image 20240613100959.png]]
![[Pasted image 20240613101010.png]]
a sinistra cosa accade senza il distinct e a destra con distinct.

#### Join interni e esterni
Al posto di specificare il join nella clausala di where si può usare direttamente una sintassi che la esplicita nella *from*

![[Pasted image 20240613101310.png]]
I tipi di join sono i seguenti:
- right/left (outer) join
- inner join (sarebbe il theta join nell'algebra relazionale)
- full  (outer)
#### Ordinamento
![[Pasted image 20240613101900.png]]

#### Operatori aggregati
Gli operatori aggregati non possono essere utilizzati sullo stesso attributo e sono:
- count conta tutte il numero di istanze
- max e min restituiscono il massimo o il minimo di un attributo che compare
- sum somma tutti i valori
- avg fa la media (difatto divide il sum per il count)


#### Raggrupamento e *having* 
Se vogliamo raggruppare secondo un attributo abbiamo la operazione di group by.
Se poi volessimo operare per estrarre un certo tipo di dato sul raggruppamento dobbiamo usare la clausala having
![[Pasted image 20240613102700.png]]
![[Pasted image 20240613102713.png]]
![[Pasted image 20240613102800.png]]
![[Pasted image 20240613102847.png]]
risultato intermedio del group by

Se volessimo selezionare solo la somma degli stipendi maggiore di 100 (quindi Amministrazione e direzione da sopra) avremmo bisogno di operare sul risultato finale tramite la clausola *having*
![[Pasted image 20240613103040.png]]
![[Pasted image 20240613103047.png]]

Se al posto di selezionare la somma degli stipendi per dipartimento avessimo voluto fare la somma degli stipendi maggiore di 41 e raggrupparli per dipartimento avremmo semplicemente messo la clausola 
*where Stipendio>41* 

#### Riassunto di una query sql base
![[Pasted image 20240613104358.png]]

### Interrogazioni di tipo insiemistico in SQL
Sono gli operatori di *union, execpt, intersect* che sono analoghi pari pari agli operatori insiemistici in algebra relazionale mantenendo anche la proprietà di eliminazione dei duplicati per essere più affine al loro significato insiemistico. 
![[Pasted image 20240613104814.png]]
![[Pasted image 20240613104829.png]]
aggiungendo *all* manteniamo anche i duplicati.

### Interrogazioni nidificate
Per query nidificate intendiamo query che per ottenere un risultato richiedono il confronto con un'altra query. Per fare ciò estendiamo l'uso degli operatori *all e any* nella clausola where che andranno rispettivamente a significare che la query restituisce un risultato se la riga soddisfa la condizione per tutti gli elementi della query nidificata, mentre any indica che  per almeno un elemento della query nidificata è soddisfatta la condizione.
![[Pasted image 20240613105803.png]]
![[Pasted image 20240613105836.png]]
Stessa risultato prima usando un aggregato e dopo esprimendolo con una singola query
#### Query nidificate complesse
Se andiamo a introdurre delle variabili nelle nostre query queste hanno una certa visibilità. 
![[Pasted image 20240613110747.png]]
D1.città non è visibile nella seconda query nidificata perchè definita in quella prima.
Query: estrarre le persone che hanno degli omonimi
![[Pasted image 20240613110843.png]]
Esempio sia di visibilità sia di uso dell'operatore exists. P è visibile alla query nidificata perchè di un livello "superiore". Viene anche detto passaggio di binding, quando la query nidificata fa riferimento al contesto di una sua query esterna.

Exists è un operatore logico che accetta un'interrogazione nidificata e restituisce il valore vero solo se l'interrogazione fornisce un risultato non vuoto. Ha significato solo quando esiste un passaggio di binding.

La query precedente poteva essere eseguita anche tramite un join tra due istanze della stessa tabella.
![[Pasted image 20240613111339.png]]
Esempio della query senza la query nidificata

Fare la query in cui si ricercano le persone che non hanno omonimi ci fa usare l'operatore not exists
![[Pasted image 20240613111534.png]]

### Modificati dei dati
Sono ovvi...
![[Pasted image 20240613111707.png]]
![[Pasted image 20240613111717.png]]

![[Pasted image 20240613111756.png]]
Cancella TUTTE le entry in Dipartimanto
![[Pasted image 20240613111812.png]]
Ha lo stesso effetto della precendente ma cambia anche lo schema della base di dati eliminando tutto ciò che referenzia Dipartimanto

![[Pasted image 20240613111937.png]]
Esempi di update
![[Pasted image 20240613111956.png]]
