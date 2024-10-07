#Agenti 
prev : [[Intro agli agenti autonomi]]

Come abbiamo visto gli agenti sono immersi in un ambiente, con diverse proprietà e caratteristiche, con cui l'agente può interagire.

In base al tipo di goal, obbiettivo, che l'agente is pone e come lo vuole raggiungere avremo diversi tipi di modello agente, dove per modello intendo una architettura per rappresentare l'agente.

### Agenti reattivi (reflex)

![[Agente reflex.png]]
Un agente reattivo determina la propria azione in base a ciò che percepisce ad un determinato tempo t. Questo agente opera spesso con un set di regole molto semplici determinate da if-else-then.

### Agenti reattivi con modello
Questo agente mantiene una serie di percezioni in memoria, determinando una stima dello stato in cui si trova mischiando ciò che conosceva a priori e le informazioni ottenute a runtime.  Un esempio è un agente che gioca a poker che tiene conto delle carte uscite in precedenza per decidere la sua azione.
![[Pasted image 20241004152948.png]]

### Agenti con modello orientati a goal
Fissiamo un'insieme s1 di stati in cui l'agente si sente soddisfatto, chiameremo questi stati goal. 
L'agente stima lo stato in cui si trova in base alle percezioni, effettua una previsione di ciò come la sua azione possa influenzare lo stato in modo tale da portarlo più vicino al suo goal.
![[Pasted image 20241004153143.png]]
### I goals
Come facciamo a capire quale stato desideriamo di più? 
Il nostro agente è incapace di stabilire questa cosa lavorando in linguaggio binario dobbiamo quindi stabilire una gerarchia o un altro metodo per quantificarli.

Per poter quantificare quale scelta ci convenga possiamo utilizzare le probabilità.
Ricordo che le probabilità sono definite, in modo formale, come la (inserire la frase di basilico quando ne parla)
Informalmente è la possibilità che un evento positivo avvenga.

Calcoliamo a questo punto il nostro valore atteso (probabilità di un certo evento che accada per il suo valore)

Ci stiamo a questo punto avvicinando ad un modo per far capire alla macchina cosa sia meglio scegliere. Non è un metodo infallibile, ci manca stabilire quanto un evento possa essere desiderabile.

Un esempio: due lotterie binarie (o si vince o si perde). Nella prima lotteria si vince sempre una quantità x di denaro. La seconda si vince una quantità y di denaro molto maggiore ma con una percentuale molto bassa. Se calcoliamo il valore atteso di entrambe la seconda lotteria sembrerà più favorita per la nostra macchina corrente basata sul valore atteso.

#### Desirebilità tramite utilità
Possiamo introdurre matematicamente un fattore di rischio per la macchina.
Ci focalizziamo però su un metodo economico che funziona particolarmente bene sul denaro, ma che possa essere generalizato: l'utlità

Tramite l'utilità cerchiamo di tenere conto sia del valore atteso sia del nostro agente.

Generalizziamo e utiliziamo il concetto di preferenza stretta, indifferenza e preferenza.
Con questi tre concetti possiamo dire al nostro agente quale degli stati esso preferisca. Estendiamo ulteriormente a delle lotterie di stati in cui abbiamo una coppia di probabilità assegnata a ciascuno stato.

Abbiamo il linguaggio con cui comunicare con l'agente. Ci manca la grammatica, fondamentale per non avere casi che ci farebbero ritrovare in situazioni impossibili da decidere. (Esempio: preferiamo la macchina al treno, l'autobus alla macchina, il treno all'autobus)

#### Le proprietà fondamentali per le preferenze
![[Pasted image 20241004155451.png]]

#### Funzione di utilità
Come facciamo a passare da questi concetti di preferenza, astratti per la macchina ad un valore, ad un intero?
Ci serviamo del teorema di Von Neumann e Morgenstern applicata alle lotterie tale per cui, se abbiamo una lotteria che gode di tutte le proprietà che abbiamo elencato allora il suo valore di utilità non è altro che il valore attesso calcolato sulle utilità di ogni singolo stato. La funzione utilità u(s) ci ritorna un valore su un determinato stato s della sua utilità.

In sintesi: il valore di utilità sulle lotterie è definibile come la sommatoria del valore atteso di ciascuna possibilità
![[Pasted image 20241004155854.png]]

Abbiamo trovato un modo di quantificare tramite numeri la definizione di intelligenza con la massimizzazione di una funzione.


#### Esempio di agenti basati su utilità
![[Pasted image 20241004160013.png]]
Qui vediamo come le due azioni a e b fanno entrare il nostro agente in una lotteria. Definiamo alpha e beta probabilità di una dato passaggio di sato.
Calcolando tramite il teorema abbiamo che le nostre utilità sono dipendenti dalle probabilità. La macchina in base alla probabilità sceglierà o a  o b.