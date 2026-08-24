# Domanda 26

Dato un albero nel quale i nodi contengono una chiave, si definisca costo di un cammino dalla radice ad una foglia, come la somma delle chiavi dei nodi che compaiono nel cammino. Scrivere una funzione `MaxPath(T)` che opera nel modo seguente. Prende in input un albero binario $T$, con radice $T.root$, e nodi $x$ che hanno come campi $x.k$, $x.l$ e $x.r$, ovvero una chiave, il puntatore al figlio sinistro e destro, rispettivamente. Restituisce il costo del cammino di costo massimo dalla radice ad una foglia. Valutarne la complessità.

---

### i. Idea e Logica

In questo esercizio abbiamo un albero generico (quindi nessun dettaglio sul suo ordinamento tra genitore e figlio sinistro e destro). Vogliamo calcolare il costo massimo globale dell’albero $T$ tra tutti i cammini dalla radice ad una foglia, dove per costo si intende la somma delle chiavi dei nodi che si trovano lungo un dato cammino.

In particolare, possiamo vedere che il costo massimo per un nodo $x$ sarà dato dalla sua chiave sommata al costo del cammino più lungo nel tratto $x \to \text{foglia}$. Quindi, per gestire correttamente la ricorsione serve il caso base per gestire i nodi foglia.
Ovvero, se $x$ è un nodo foglia, allora si restituisce come valore semplicemente $x.k$, essendo questa l’unica chiave che andrà a contribuire ulteriormente alla somma per il suo dato cammino.

Se invece $x$ non è un nodo foglia, allora bisogna valutare quale dei due sottoalberi contiene il cammino di costo massimo. Per fare ciò, si usa una variabile locale `costo` inizialmente impostata a $-\infty$. Dopodiché si hanno due casi:
- Se $x.l \ne \text{nil}$ allora si imposta `costo` al massimo tra `costo` e il cammino massimo trovato ricorrendo sul sottoalbero sinistro di $x$.
- Se $x.r \ne \text{nil}$ allora in modo analogo si imposta `costo` al massimo tra `costo` e il cammino massimo trovato ricorrendo sul sottoalbero destro di $x$.

Infine si restituisce la somma tra il valore `costo` restituito dalle due chiamate ricorsive e la chiave del nodo corrente $x.k$.

---

### ii. Pseudocodice

```text
// restituisce la somma del cammino massimo
// altrimenti sentinella -∞
MaxPath(T)
    // guard
    if T.root == nil
        return -∞

    return MaxPathRec(T.root)

// procedura ricorsiva
MaxPathRec(x)

    // se x e' foglia, si restituisce solo la sua chiave
    // essendo l'unico valore che puo' ulteriormente contribuire a questo cammino
    if x.l == nil and x.r == nil
        return x.k

    // altrimenti, si calcola il cammino di costo massimo ricorrendo sui due sottoalberi
    costo = -∞

    // se esiste sottoalbero sinistro
    if x.l != nil
        costo = max(costo, MaxPathRec(x.l))

    // se esiste sottoalbero destro
    if x.r != nil
        costo = max(costo, MaxPathRec(x.r))

    // restituisco somma aggiornata del costo massimo
    return x.k + costo					 				
```

---

### iii. Complessità

- **Complessità Temporale:** $\Theta(n)$ in quanto si tratta di una visita completa (DFS) in cui ciascun nodo dell'albero viene visitato esattamente una volta e per ogni nodo viene eseguito un numero costante $\Theta(1)$ di operazioni.
- **Complessità Spaziale:** $\mathcal{O}(h)$ dove $h$ è l'altezza dell'albero, per via dello spazio di memoria impiegato dallo stack delle chiamate ricorsive. Nel caso pessimo (albero degenere a lista) sarà $\mathcal{O}(n)$, nel caso ottimo (albero bilanciato) sarà $\mathcal{O}(\log n)$.
