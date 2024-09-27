	nota: capitolo 3 del libro 

Sono tutte quelle operazioni definite su relazioni che ritornano a loro volta delle relazioni.

### Operatori di unione intersezione  e differenza
Sono i classici operatori dell'insiemistica. 

**Unione** su due relazioni r1 e r2 la loro unione è tutti quei oggetti appartenenti a r1 oppure r2, o appartenenti a entrambi.

**intersezione** su due relazioni r1 e r2 è una relazione r3 i cui componenti sono appartenenti sia a r1 sia a r2. 

**Differenza** una differenza tra r1 - r2 conterrà le tuple che appartengono a r1 e non appartenenti a r2

### Operatori di ridenominazione
Ci aiuta, come dice il nome, a rinominare il nome degli attributi di una relazione per poi comporre delle unioni.
![[Pasted image 20240611105542.png]]

![[Pasted image 20240611105714.png]]Esempio di ridenominazione poi seguita da un unione.

### Operatore di selezione
Indicato dall'operatore sigma, è un operatore che prende una relazione e ne selezione un sottoinsiemi di tuple (facendo una sorta di taglio orrizontale). La selezione può essere espressa da una formula sugli attributi tramite gli operatori logici *and, not, or* e da un insieme di operazioni X definite sulle ugualianze e le disuguaglianze (maggiore, minore, uguale) che torni un valore di verità.
![[Pasted image 20240611110318.png]]
Selezione di tutti gli impiegati che hanno età maggiore di 30 e stipendio superiore a 4000 dalla relazione impiegati

### Operatore di proiezione
La proiezione segnato con il simbolo di Pi-greco definisce una operazione su una relazione in cui si vanno a selezionare un sottoinsieme di attributi della relazione, attuando una sorta di taglio verticale. L'operazione produce al più tante tuple quante ne contiene la relazione originale (caso in cui il sottoinsieme che stiamo proiettando è **superchiave**).
![[Pasted image 20240611110937.png]]



#### Considerazione tra proiezione e selezione
![[Pasted image 20240611111021.png]]
Come si può vedere la proiezione effettua una decomposizione verticale sugli attributi, mentre la selezione restituisce un sottoinsieme della relazione di partenza.

### Join, join naturale e theta-join

Il join ci permette di correlare dati in relazioni diverse tra di loro. Ne esistono due varianti il join naturale e il theta-join 

Theta-join, ergo join con condizione. Equi join è un join in cui la condizione è una ugualianza tra due valori. Il join naturale può essere ricondotto ad un theta join in cui essenzialmente si verificano che alcuni valori siano uguali.

Il join naturale lavora su i VALORI simili tra due relazione e li mette in correlazione.
Si può usare un outer join per includere anche le n-uple non correllate con i valori null che completano. I right e i left join vanno ad indicare quale  delle due relazioni vogliamo considerare e un  full considera entrambe.
![[Pasted image 20240613122137.png]]

### Divisione
Divisione La divisione di applica solo a relazioni r(Z), s(X) in cui X ⊆ Z. Dato l’insieme di attributi Y = Z − X, la divisione r ÷ s e una relazione ` T(Y ) contenente tutte le tuple t tali che: - vi siano tuple tr in r con tr[Y ] = t, e - tr[X] = ts per ogni tupla ts di s. Intuitivamente, la divisione verifica una condizione o una corrispondenza fra una o piu tuple di ` r e tutte le tuple di s.

![[Pasted image 20240613122332.png]]
x "soddisfa sia a che b"
