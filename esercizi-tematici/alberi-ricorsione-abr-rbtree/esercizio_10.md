# Esercizio 10 — Nodi Fair in un Albero Binario

Un nodo $x$ di un albero binario $T$ si dice **fair** se la somma delle chiavi nel cammino che conduce dalla radice dell'albero al nodo $x$ (escluso) coincide con la somma delle chiavi nel sottoalbero di radice $x$ (con $x$ incluso).
Realizzare un algoritmo ricorsivo `printFair(T)` che, dato un albero $T$, stampa tutti i suoi nodi fair. Supporre che ogni nodo abbia i campi $x.left$, $x.right$, $x.p$, $x.key$. Valutare la complessità dell'algoritmo.

---

### i. Idea e Logica

Per questo esercizio abbiamo un albero binario generico $T$ e vogliamo stampare tutti i nodi fair.
Per identificare un nodo fair serve conoscere simultaneamente un'informazione proveniente "dall'alto" (la somma del cammino) e un'informazione proveniente "dal basso" (la somma del sottoalbero).

Quindi, serve un parametro ulteriore, che possiamo chiamare `sumPath`, da passare al nodo $x$ prima di ogni chiamata ricorsiva.
La condizione di stampa di un nodo fair equivale a verificare se `sumTree == sumPath`.
Per farlo:
1. La somma `sumTree` si trova calcolando ricorsivamente la somma dei sottoalberi $x.left$ e $x.right$, a cui viene sommata la chiave corrente $x.key$.
2. Per i figli di $x$, il nuovo `sumPath` da passare in input sarà esattamente il `sumPath` corrente con l’aggiunta della chiave del nodo attuale $x.key$.

Per gestire correttamente la ricorsione, utilizzo come caso base il fatto che se $x == \text{nil}$ (ovvero $x$ è un nodo "nullo"), la funzione restituisce semplicemente $0$.
Utilizzo una funzione `printFair(T)` che agisce da semplice wrapper per la procedura ricorsiva `printFairRec(x, sumPath)`. La prima chiamata dal wrapper passa come valore iniziale di `sumPath` il valore $0$, essendo che per la radice la somma delle chiavi degli antenati (inesistenti) è nulla.

---

### ii. Pseudocodice

```text
// Wrapper
printFair(T)
    return printFairRec(T.root, 0)

// Procedura ricorsiva
// stampa tutti i nodi fair del sottoalbero radicato in x
printFairRec(x, sumPath)

    // caso base: nodo nullo non contribuisce alla somma
    if x == nil
        return 0

    // ricorro sul sottoalbero sinistro, aggiornando la somma del cammino
    leftSum = printFairRec(x.left, sumPath + x.key)

    // ricorro sul sottoalbero destro, aggiornando la somma del cammino
    rightSum = printFairRec(x.right, sumPath + x.key)

    // aggiorno la somma totale del sottoalbero radicato in x
    sumTree = leftSum + rightSum + x.key

    // se la somma del sottoalbero e la somma del cammino coincidono,
    // il nodo e' fair e quindi ne stampo la chiave
    if sumPath == sumTree
        print x.key

    // restituisco la somma del sottoalbero al nodo padre			
    return sumTree
```

---

### iii. Complessità

- **Complessità Temporale:** L'algoritmo effettua una visita completa in profondità (DFS) dell'albero. Poiché ogni nodo viene visitato esattamente una volta e in ogni nodo viene eseguito un numero costante di operazioni $\Theta(1)$ (somme e confronti), avremo una complessità temporale pari a:

$$
T(n) = \Theta(n)
$$

- **Complessità Spaziale:** Lo spazio di memoria ausiliario è determinato dallo stack delle chiamate ricorsive. Nel caso pessimo di un albero degenere lo spazio sarà $\mathcal{O}(n)$, mentre nel caso ottimo o medio di un albero bilanciato sarà $\mathcal{O}(\log n)$. In generale, è proporzionale all'altezza dell'albero $\mathcal{O}(h)$.
