# Domanda B — Alberi Red-Black 

Enunciare le proprietà degli alberi Red-Black.
Successivamente, spiegare come verificare ricorsivamente se un albero binario di ricerca colorato soddisfa le seguenti proprietà:
1. nessun nodo rosso ha un figlio rosso;
2. ogni cammino da un nodo a una foglia nil discendente contiene lo stesso numero di nodi neri.

La procedura ricorsiva deve restituire entrambe le seguenti informazioni: validità del sottoalbero, e altezza nera del sottoalbero.
Valutare la complessità.

---

### i. Proprietà degli Alberi Red-Black

Possiamo definire un RB-Tree come un ABR in cui ogni nodo ha un ulteriore campo $x.col \in \{R, B\}$ per indicare il colore rosso (RED) oppure nero (BLACK). In particolare, un RB-Tree è valido se soddisfa le seguenti cinque proprietà fondamentali:
1. Ogni nodo $x$ ha un solo colore, RED o BLACK.
2. La radice $T.root$ è BLACK.
3. Le foglie (rappresentate dal nodo sentinella $T.nil$) sono BLACK.
4. I figli di un nodo RED sono necessariamente BLACK (ovvero, un nodo RED non può avere figli RED).
5. Il numero di nodi BLACK lungo qualsiasi cammino da un dato nodo $x$ (escluso) fino a una foglia discendente (inclusa) è lo stesso per ogni cammino del sottoalbero radicato in $x$. Questa quantità è detta *black-height* o altezza nera, e si indica con $bh(x)$.

---

### ii. Idea e Pseudocodice

Uso una funzione `RBTree(T)` per verificare se l'intero albero $T$ è un RB-Tree valido. Per far restituire due informazioni simultaneamente a una singola funzione, si sfrutta il dominio dei numeri interi:
- Un numero $\ge 0$ indicherà che il sottoalbero **è valido**, e il numero stesso rappresenterà il numero di nodi neri riscontrati.
- Il valore `-1` indicherà che il sottoalbero **non è valido** (poiché l'altezza nera non può essere negativa, non c'è rischio di collisione).

La procedura ricorsiva `RBrec(x)` verifica la validità del sottoalbero radicato in $x$. Restituisce la somma dei nodi neri trovati (incluso $x$, in modo che il genitore possa confrontare i due rami) oppure `-1` al primo fallimento.

```text
// funzione "wrapper"
RBTree(T)
    // se l'albero e' vuoto
    if T.root == T.nil
        return 0

    // se la radice e' rossa, viola direttamente la proprieta' 2
    else if T.root.col == R
        return -1

    // altrimenti, invoco la procedura ricorsiva sulla radice
    else
        return RBrec(T.root)				

// procedura ricorsiva, restituisce bh(x) calcolata bottom-up oppure -1 (non valido)
RBrec(x)
    // caso base: la foglia sentinella (T.nil) e' sempre nera,
    // costituisce l'ancora per iniziare a contare l'altezza nera
    if x == T.nil
        return 0

    // violazione proprieta' 4: nessun nodo RED puo' avere figli RED
    if x.col == R and (x.left.col == R or x.right.col == R)
        return -1

    // ricorro sui sottoalberi per trovare la loro black-height
    left = RBrec(x.left)
    right = RBrec(x.right)

    // se uno dei due figli ha riportato un errore (-1),
    // oppure se le altezze nere dei due rami non coincidono (violazione proprieta' 5)
    if left == -1 or right == -1 or left != right
        return -1

    // altrimenti il sottoalbero e' valido
    count = left

    // se il nodo corrente e' BLACK, lo includo nel conteggio da passare al genitore
    if x.col == B
        count = count + 1

    // restituisco il conteggio aggiornato
    return count		 				
```

---

### iii. Complessità

- **Complessità Temporale:** L'algoritmo non fa altro che eseguire una visita completa in profondità (post-order traversal) dell'albero binario. Poiché visita ciascun nodo dell'albero esattamente una volta ed esegue su di esso un numero costante di operazioni (controlli booleani, somme e confronti) di costo $\Theta(1)$, la complessità temporale totale ammonta a:

$$
T(n) = \Theta(n)
$$

dove $n$ è il numero totale di nodi presenti nell'albero.

- **Complessità Spaziale:** Lo spazio ausiliario è determinato dallo stack delle chiamate ricorsive. Nel caso pessimo sarà proporzionale all'altezza dell'albero, ovvero $\mathcal{O}(h)$. (Se l'albero in input risultasse essere un RB-Tree valido, potremmo dire con precisione $\mathcal{O}(\log n)$, ma trattandosi di una funzione di validazione che potrebbe ricevere in input alberi del tutto degeneri, il limite corretto da dichiarare è $\mathcal{O}(h)$.
