## Astrazione procedurale
Visto che questo è un esame di merda salterò le prime lezioni in cui spiega Java e passerò direttamente alla ragione per cui non ho passato sto schifo, documentazione e astrazione.
L'astrazione **procedurale** è la combinazione dell'astrazione per **specificazione** (sottile riferimento alla teoria degli insiemi) e per **parametrizzazione.**

    public static float sqrt(float x) {
	    // REQUIRES: x > 0
	    // EFFECTS: returns the square root of x
	    
		// code here...
    }
Il punto dell'astrazione è sfanculare completamente l'implementazione stessa e concentrarsi su alcuni pilastri principali da comunicare a chi ha bisogno di utilizzare la funzione.

    public static void sort(int[] array) {
	    // MODIFIES: array
	    // EFFECTS: sorts the array
    }
L'ultimo pilastro sarebbe la clausola **"MODIFIES"** che specifica I parametri che vengono modificati, ma non come vengono modificati. Quest'ultimo fa sempre parte dei compiti della clausola "EFFECTS"
Nota: Se non ci sono requisiti particolari per i parametri, quindi finché il tipo è corretto allora il metodo funziona e restituisce un risultato valido, allora il metodo si dice metodo **totale**. Un esempio è il metodo **sort** che abbiamo definito prima. Al contrario, se ci sono dei requisiti il metodo viene detto **parziale**, come col metodo **sqrt**. 
C'è anche da ricordarsi che nella clausola effects si dà per scontato che i requirements vengano soddisfatti.

Quando si crea un'astrazione procedurale bisogna fare attenzione a non esagerare. Nel senso che non tutto magari sarà abbastanza importante da meritare una procedura a parte, specie se non è facile specificare la funzione del pezzo di codice che si sta isolando.
Anche il contrario è pericoloso, se fai un solo metodo che fa ogni singola cosa va a finire che aggiungere funzionalità diventerà un inferno. Cerca di limitare gli input di una funzione piuttosto che farne 10 per ogni errore particolare.
Ricordiamoci che le procedure devono essere **generali.** L'esempio che fa il libro è la differenza tra la ricerca di uno specifico numero in una lista e di un numero n.

    public static int search(int[] array, int n) {
	    for (int i = 0; i < array.length; i++) if (array[i] == n) return i;
	    return -1;
    }
   Rispetto a questo codice è generalizzato:

    public static int searchSeven(int[] array) {
	    for (int i = 0; i < array.length; i++) if (array[i] == 7) return i;
	    return -1;
    }
   Ovviamente non è sempre il caso di generalizzare, ma se la generalizzazione non introduce nessuna assunzione dannosa potrebbe convenire farlo.
   Implementando un'astrazione è legale controllare se i requirements del metodo vengono soddisfatti, e nel caso in cui non lo fossero è consigliato lanciare un'**exception**.
## Eccezioni
NON FARÒ L'INTRODUZIONE TECNICA A COSA SIANO. Quel che farò invece è riassumere le note dei libri (PDJ, EJ) sul design delle exception, come usarle al meglio.
La prima cosa che fa notare il libro della Liskov, è che le eccezioni potrebbero non essere necessariamente errori, vengono "lanciate" in casi eccezionali, e questi sono relativamente arbitrari.
Un esempio che viene fatto è lanciare un'eccezione in un metodo di ricerca nel caso in cui ciò che si sta cercando non venga trovato:

    public static int search(int[] haystack, int needle) throws NotFoundException{
	    for (int i = 0; i < haystack.length; i++) {
		    if (haystack[i] == needle) return i;
	    }
	    throw new NotFoundException("Looking for a needle in a haystack is hard");
    }
Ricordiamoci inoltre che le eccezioni non coprono gli **errori logici**, che devono essere evitati come la peste. Quindi, quando usare le eccezioni? La Liskov sostiene che un caso d'uso siano appunto le situazioni eccezionali, invece che codificare nell'oggetto ritornato (e.g. ritornare -1 nella search) la situazione, attirare l'attenzione. La pratica citata poco fa è considerata accettabile però quando per esempio i metodi sono privati.
Sempre secondo Liskov, la funzione principale delle eccezioni è quella di fare in modo di poter omettere la clausola **REQUIRES** (rendendo il metodo totale) ed inserire eventuali eccezioni nella clausola **EFFECTS** (che in javadoc si traduce in **@throws**). Questo non vuol dire che vada fatto sempre però.

> Sidebar 4.1 Rules for Using Exceptions
When the context of use is local, you need not use exceptions because you can easily verify
that requires clauses are satisfied by calls and that special results are used properly.
However, when the context of use is nonlocal, you should use exceptions instead of special
results. And you should use exceptions instead of requires clauses unless a requirement
cannot be checked or is very expensive to check.

**Checked vs unchecked.**

Prima di tutto specifichiamo: un'exception checked deve essere gestita o tramite **try catch** o esplicata tramite **throws** alla dichiarazione del metodo. La Liskov ci insegna che le exception unchecked dovrebbero essere destinate agli errori di programmazione (quindi in produzione non dovrebbero mai capitare, mentre una checked potrebbe essere prevista).

> Sidebar 4.2 Checked versus Unchecked Exceptions
You should use an unchecked exception only if you expect that users will usually write code
that ensures the exception will not happen, because
• There is a convenient and inexpensive way to avoid the exception.
• The context of use is local.
Otherwise, you should use a checked exception.

Il professore ha parlato di livelli di astrazione, tramite la reflection, se abbiamo una exception di un certo tipo in una funzione di search per esempio, ma questa funzione è stata chiamata in un determinato contesto in cui abbiamo più informazioni, è accettabile fare un try e nella clausola catch sollevare una nuova eccezione (penso che questo convenga farlo anche per passare da un'eccezione checked ad un'unchecked)

**Defensive programming**

In questo paragrafo la Liskov parla di cosa fare quando in un metodo parziale una clausola requires non viene rispettata, in particolare, suggerisce la creazione di un'eccezione (col nome fittizio di **FailureException**) che deve rimanere unchecked. Questo solo nel caso in cui controllare la correttezza dei parametri sia semplice.
Supponiamo di dover fare la ricerca di un elemento in un array, in un contesto in cui dovremmo essere al 100% sicuri che l'elemento sia presente in esso; se l'elemento non dovesse fare effettivamente parte della lista allora c'è stato un errore logico o di programmazione, è giusto che l'eccezione sia unchecked.

**Items di Bloch sulle eccezioni**

Il prof definisce il libro di Bloch come una lista di ingredienti di merendine (molto meno discorsivo della Liskov) ed è materiale utile per prendere un voto alto all'esame (ho bisogno di alzare la media). Quindi vi fornirò una lista ez degli item (usatela come reference mentre fate il progetto magari:

- Item 69: non abusare delle eccezioni (qui va contro la Liskov perché lei dice che è accettabile usare le eccezioni per effettuare flow control, una boiata assurda).
- Item 70: è convenzioni che le eccezioni unchecked create da noi ereditino dalla classe RuntimeException, e che la classe Error sia riservata alla JVM, detto questo, utilizzare le checked quando la situazione è recuperabile.

> To summarize, throw checked exceptions for recoverable conditions and
unchecked exceptions for programming errors. When in doubt, throw unchecked
exceptions. Don’t define any throwables that are neither checked exceptions nor
runtime exceptions. Provide methods on your checked exceptions to aid in
recovery.

- Item 71: quando il caso è semplice, cercare di evitare il sollevamento di eccezioni checked, a favore del ritorno di un'opzione vuota (e.g. null), se questo non dà abbastanza informazioni, solleva un'eccezione. Come detto prima, è accettabile trasformare un'eccezione checked in unchecked, anche per non intasare la API.
- Item 72: favorire l'utilizzo delle eccezioni già definite. In breve no clutter.
- Item 73: cambia il livello di astrazione delle eccezioni ove necessario.
- Item 74: documenta ogni eccezione checked una per una con la clausola @throws di javadoc, non fare @throws Exception per esempio.
- Item 75: dai più informazioni possibili nei messaggi d'errore (ma non dati critici come password o numeri di conti corrente).
- Item76: atomicità degli errori, anche se viene sollevata un'eccezione idealmente l'oggetto che la lancia deve rimanere utilizzabile (se questa è unchecked... beh non c'è più un contesto in cui utilizzarla XD).
- Item 77: non ignorare le eccezioni.


