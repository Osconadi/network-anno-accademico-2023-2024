#ricerca #ottimale #search
Nella ricerca dei problemi di [[Risoluzione automatica di problemi di search]] abbiamo considerato finora la fattibilità della risoluzione del problema, ovvero se esiste una strada possibile. Ora consideriamo la strada migliore trovabile per arrivare al goal.
Consideriamo da adesso i pesi.

###  Ottimizziamo la BFS per i pesi
La BFS ci trova la soluzione a profondità minima. In un caso ideale in cui tutti i costi sono unitari la bfs è di per se ottima.
#### Uniform Cost Search UCS
Per generalizzare la BFS su costi arbitrari non espanderemo più per profondità minore ma per costo minore. Oltre a questa banalità non faremo più il check sul goal non appena viene trovato, ma quando viene espanso. Ci terremo conto anche del costo totale del percorso ogni volta che generiamo un nodo, cumulandoli.

##### Dimostrazione dell'ottimalità di UCS
Dobbiamo dimostrare che UCS sia valido e risponde alla domanda "porta questo al miglior percorso sempre?".

Ipotesi: 
 1) UCS seleziona per la prima volta dalla [[frontiera]] un nodo V che è stato generato attraverso un percorso p
 2) il percorso p non è il percorso ottimo per raggiungere V

