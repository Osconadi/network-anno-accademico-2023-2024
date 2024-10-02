Nella pratica l'agente è un algoritmo. 
Secondo Russel Norvig: un agente che può percepire un ambiente attraverso dei sensori e agire sul ambiente tramite degli attuatori

In teoria questo agente dovrebbe agire "razionalmente".

La parte fondamentale è il doppio flusso di informazioni, in ingresso e in uscita che l'agente percepisce e quindi attua delle azioni sull'ambiente che generano un cambiamento di stato.  L'agente è parte dell'ambiente che possiamo progettare e programmare.


### Differenze tra ambiente parzialmente osservabile e totalmente osservabile
In un ambiente totalmente osservabile conosce tutte le variabili all'interno dell'ambiente (esempio un npc)
In un ambiente parzialmente osservabile si hanno solo parte delle informazioni e spesso queste informazioni potrebbero essere afflitte da "noise". (un robot in una stanza)

### Single agent vs multi agent
In un ambiente ci potrebbero essere uno, single agent, o più agenti, mukti-agent, dove non per forza gli altri agenti possono avere le stessi obbiettivi. (Un gioco con più giocatore, più robot magazzinieri ecc...)

### Ambiente Stocastico o deterministico
Deterministico: dato lo stato corrente e l'azione eseguita dall'agente il prossimo stato è determinato completamente (ESEMPIO: una mossa di uno scacchi)
Si dice che le azioni si possono svolgere in open loop e non bisogna controllarle.

Stocastico: le azioni hanno effetti non certi. Le azioni sono descritte da una distribuzione di probabilità.

### Altri fattori e caratteristiche
Statico vs Dinamico

Tempo discreto vs Tempo continuo

Conosciuto vs sconosciuto