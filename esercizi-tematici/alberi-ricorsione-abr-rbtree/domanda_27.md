# Domanda 27

Realizzare una procedura `Level(T)` che dato un albero binario $T$, con radice $T.root$, e nodi $x$ con campi $x.left$, $x.right$ e $x.key$, rispettivamente figlio destro, figlio sinistro e chiave intera, ritorna il numero di nodi per i quali la chiave $x.key$ è minore o uguale al livello del nodo (la radice ha livello 0, i suoi figli livello 1 e così via). Valutare la complessità.

---

### i. Idea e Logica

Abbiamo un albero binario generico $T$ e vogliamo trovare il numero di nodi $x \in T$ che hanno un valore di chiave minore o uguale al livello a cui sono situati. Si può usare una funzione `Level(T)` che agisce da “wrapper” per una procedura ricorsiva `LevelRec(x, lvl)` che calcola ricorsivamente il numero di nodi del sottoalbero radicato in $x$ tali che $x.key \le \text{lvl}$. Serve quindi passare come parametro di input la variabile `lvl` essendo che prima di ogni chiamata ricorsiva per un nodo $x$, serve conoscere il livello corrente per aggiornare correttamente il risultato.

In particolare:
- Se $x == \text{nil}$ allora si restituisce $0$ per non contribuire erroneamente al conteggio.
- Altrimenti si ricorre sui sottoalberi radicati in $x.left$ e $x.right$ incrementando `lvl+1` e salvando i loro risultati in variabili temporanee `left` e `right`.
- Poi si verifica il nodo corrente: se si trova che $x.key \le \text{lvl}$ allora si restituisce il risultato aggiornato come `left + right + 1`.
- Altrimenti, se il nodo corrente non ha chiave $\le \text{lvl}$, allora si restituisce semplicemente `left + right`.

---

### ii. Pseudocodice

```text
// funzione "wrapper"
Level(T)
    return LevelRec(T.root, 0)

// procedura ricorsiva
LevelRec(x, lvl)

    // caso base
    if x == nil
        return 0

    // altrimenti, si ricorre sui sottoalberi
    else
        left = LevelRec(x.left, lvl + 1)
        right = LevelRec(x.right, lvl + 1)

        // se la chiave del nodo corrente e' <= al livello corrente, si conta
        if x.key <= lvl
            return left + right + 1

        // altrimenti, non si aggiunge nulla al conteggio
        else
            return left + right		
```

---

### iii. Complessità

- **Complessità Temporale:** Essendo che si tratta di una visita completa di ciascun nodo di $T$ con operazioni che richiedono tempo costante, la complessità temporale risulta:

$$
T(n) = \Theta(n)
$$

- **Complessità Spaziale:** Lo spazio ausiliario impiegato dallo stack delle chiamate ricorsive è proporzionale all'altezza dell'albero, ovvero $\mathcal{O}(h)$. Nel caso pessimo di un albero sbilanciato (degenere a lista) lo spazio sarà $\mathcal{O}(n)$, mentre nel caso ottimo di un albero bilanciato sarà $\mathcal{O}(\log n)$.
