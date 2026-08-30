# Esercizio 14 — Costruzione ABR di altezza minima

Realizzare una procedura `BST(A)` che dato un array $A[1..n]$ di interi, ordinato in modo crescente, costruisce un albero binario di ricerca di altezza minima che contiene gli elementi di $A$ e ne restituisce la radice. Per allocare un nuovo nodo dell'albero si utilizzi una funzione `mknod(k)` che dato un intero $k$ ritorna un nuovo nodo con $x.key = k$ e figlio destro e sinistro $x.left = x.right = \text{nil}$. Valutarne la complessità.

---

### i. Idea e Logica

Per ottenere un Albero Binario di Ricerca di altezza minima, l'albero deve essere il più bilanciato possibile. Questo coincide con un'altezza pari a $h = \lfloor\log_2 n\rfloor$.

Essendo l'array $A[1\dots n]$ già ordinato in senso crescente, la strategia ottimale consiste nell'usare un approccio *divide et impera*, scegliendo sempre l'elemento centrale dell'array (o del sottoarray corrente) come radice. Ovvero, usiamo l'elemento all’indice $q = \lfloor\frac{n}{2}\rfloor$. In questo modo, tutti gli elementi alla sua sinistra saranno strettamente minori e formeranno il sottoalbero sinistro, mentre quelli alla sua destra saranno maggiori e formeranno il sottoalbero destro, garantendo così il rispetto della proprietà dell'ABR e il perfetto bilanciamento.

Assumiamo che la procedura ausiliaria `mknod(k)` funzioni correttamente con costo costante $\Theta(1)$:
```text
mknod(k)
    allocate x
    x.key = k
    x.left = nil
    x.right = nil
    return x
```

Possiamo quindi operare ricorsivamente sull’intervallo $A[p\dots r]$. Se $p > r$ (sottoarray vuoto), restituiamo semplicemente `nil`. Altrimenti, calcoliamo l'indice centrale $q$, allochiamo un nuovo nodo $x$ usando `mknod(A[q])`, e ricorsivamente leghiamo il figlio sinistro calcolato su $A[p\dots q-1]$ e il figlio destro calcolato su $A[q+1\dots r]$.

---

### ii. Pseudocodice

Uso `BST(A)` come "wrapper" per inizializzare la procedura ricorsiva `recBST(A, p, r)`.

```text
// funzione "wrapper"
BST(A)
    // restituisce nil se A e' vuoto, oppure la radice del nuovo ABR
    return recBST(A, 1, A.length)

// procedura ricorsiva, restituisce la radice del sottoalbero creato
recBST(A, p, r)

    // caso base: intervallo non valido / vuoto
    if p > r
        return nil		

    // passo ricorsivo
    else
        // calcolo indice centrale e alloco il nodo radice
        q = floor((p + r) / 2)
        x = mknod(A[q])

        // ricorro a sinistra per costruire il sottoalbero sx
        x.left = recBST(A, p, q - 1)

        // ricorro a destra per costruire il sottoalbero dx
        x.right = recBST(A, q + 1, r)

        return x		
```

---

### iii. Complessità

- **Complessità Temporale:** L'algoritmo effettua due chiamate ricorsive su istanze di dimensione dimezzata ed esegue un lavoro di costo costante $\Theta(1)$ per calcolare l'indice e allocare il nodo. La relazione di ricorrenza è:

$$
T(n) = 2T(n/2) + \Theta(1)
$$

Possiamo risolverla utilizzando il **Master Theorem**, con i parametri $a = 2$, $b = 2$ e $f(n) = 1$. Calcoliamo lo spartiacque asintotico:

$$
n^{\log_b a} = n^{\log_2 2} = n^1 = n
$$

Essendo $f(n) = 1$, si verifica facilmente che $f(n) = \mathcal{O}(n^{\log_b a - \varepsilon})$ per una costante $\varepsilon = 1$. Siamo quindi nel **CASO 1** del Master Theorem, in cui il costo è dominato dalle foglie dell'albero della ricorsione. La complessità temporale esatta è:

$$
T(n) = \Theta(n^{\log_b a}) = \Theta(n)
$$

*(Questo è anche logicamente sensato: l'algoritmo visita e crea esattamente una volta ciascuno degli* $n$ *nodi).*

- **Complessità Spaziale:** Lo spazio ausiliario è dato esclusivamente dallo stack delle chiamate ricorsive. Essendo garantito che l'albero prodotto è perfettamente bilanciato, la profondità massima della ricorsione (e quindi lo spazio in memoria) sarà pari all'altezza dell'albero, ovvero $\mathcal{O}(\log n)$.
