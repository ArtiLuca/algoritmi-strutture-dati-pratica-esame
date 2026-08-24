# Domanda 26

Dato un albero nel quale i nodi contengono una chiave, si definisca costo di un cammino dalla radice ad una foglia, come la somma delle chiavi dei nodi che compaiono nel cammino. Scrivere una funzione `MaxPath(T)` che opera nel modo seguente. Prende in input un albero binario $T$, con radice $T.root$, e nodi $x$ che hanno come campi $x.k$, $x.l$ e $x.r$, ovvero una chiave, il puntatore al figlio sinistro e destro, rispettivamente. Restituisce il costo del cammino di costo massimo dalla radice ad una foglia. Valutarne la complessità.

---

### i. Idea e Logica

Per un albero generico $T$ possiamo fare delle osservazioni sul costo di un cammino $x \to \text{foglia}$ per un dato nodo $x \in T$:

- **(Caso 1)** Se $x == \text{nil}$, ovvero è un nodo "nullo", allora possiamo restituire $0$ essendo che questo non contribuisce al costo del cammino massimo.
- **(Caso 2)** Altrimenti, se $x.l == \text{nil}$, allora si esplora solo il sottoalbero destro, essendo che è l’unico che può contribuire al costo lungo il cammino per arrivare a una foglia.
- **(Caso 3)** Altrimenti, se $x.r == \text{nil}$, allora in modo analogo si esplora ricorsivamente solo il sottoalbero sinistro.
- **(Caso 4)** In ogni altro caso (entrambi i figli presenti), bisogna prendere il massimo tra il costo trovato ricorsivamente nel sottoalbero sinistro e quello trovato nel sottoalbero destro.

*Nota:* Nei casi (2), (3) e (4) bisogna sempre sommare la chiave del nodo corrente $x.k$ al risultato delle chiamate ricorsive, per mantenere correttamente aggiornato il costo totale del cammino.

---

### ii. Pseudocodice

Una possibile soluzione utilizza una funzione `MaxPath(T)` che agisce da semplice wrapper per la funzione ricorsiva `MaxPathRec(x)` che restituisce il costo massimo $x \to \text{foglia}$ per un dato nodo $x$. In questo caso per il nodo $x = T.root$.

```text
MaxPath(T)
    return MaxPathRec(T.root)

MaxPathRec(x)

    // caso 1
    if x == nil
        return 0

    // caso 2
    else if x.l == nil
        return x.k + MaxPathRec(x.r)

    // caso 3
    else if x.r == nil
        return x.k + MaxPathRec(x.l)

    // caso 4
    else
        return x.k + max(MaxPathRec(x.l), MaxPathRec(x.r))								
```

---

### iii. Complessità

- **Complessità Temporale:** Si tratta di una visita in profondità (DFS) in cui l'algoritmo passa esattamente una volta per ogni nodo dell'albero eseguendo operazioni in tempo costante. Dunque la complessità è $\Theta(n)$.
- **Complessità Spaziale:** Lo spazio di memoria ausiliario è dominato dallo stack delle chiamate ricorsive, pari a $\mathcal{O}(h)$ dove $h$ è l'altezza dell'albero (ovvero $\mathcal{O}(n)$ nel caso pessimo di albero sbilanciato e $\mathcal{O}(\log n)$ nel caso ottimo di albero bilanciato).
