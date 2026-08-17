# Esercizio 23 - Verifica Max-Heap

Scrivere una funzione `IsMaxHeap(A)` che dato in input un array di interi $A[1\dots n]$ verifica se $A$ è organizzato a max-heap e ritorna un corrispondente valore booleano. Valutarne la complessità.

---

### i. Idea e Ragionamento

Un max-heap è valido se per ogni nodo $i$ si ha che $A[i] \ge \text{Left}(i)$ e $A[i] \ge \text{Right}(i)$, dove $\text{Left}$ e $\text{Right}$ sono, rispettivamente, il figlio sinistro e destro del nodo radicato in $i$.

In particolare, possiamo notare che i nodi foglia non sono di importanza per questi confronti, non avendo figli.
Ovvero, se $n = A.size$, allora tutti i nodi agli indici $i \in [\lfloor\frac{n}{2}\rfloor+1 \dots n]$ sono nodi foglia che non serve verificare.

Quindi, il controllo per verificare se $A$ è un max-heap valido inizia dal primo nodo non foglia, ovvero all’indice $\lfloor\frac{n}{2}\rfloor$.
In questo modo possiamo iterare su ciascun nodo non foglia a ritroso fino alla radice, verificando che non violino la proprietà di max-heap con i propri figli (se esistono). Se si trova una violazione restituiamo immediatamente `false`.
Se la procedura termina senza incontrare nessuna violazione per alcun nodo non foglia, allora si restituisce `true`.

---

### ii. Pseudocodice

```text
// restituisce true se l'array è un max-heap valido, false altrimenti
IsMaxHeap(A)
    n = A.size

    // controllo solo i nodi non foglia, dal basso verso la radice
    for i = floor(n/2) downto 1
        left = 2 * i
        // verifico il figlio sinistro
        if (left <= n) and (A[i] < A[left])
            return false

        right = 2 * i + 1
        // verifico il figlio destro
        if (right <= n) and (A[i] < A[right])
            return false		

    // se non ho trovato violazioni, è un max-heap
    return true				
```

---

### iii. Complessità

La complessità temporale si basa sul numero di iterazioni effettuate dal ciclo `for`, che sono esattamente $\lfloor\frac{n}{2}\rfloor$. Poiché le operazioni interne al ciclo (calcoli matematici e confronti) costano $\Theta(1)$, il tempo impiegato è asintoticamente lineare rispetto al numero di elementi dell'array.

- **Complessità Temporale:** $T(n) = \Theta(n)$
- **Complessità Spaziale:** $\mathcal{O}(1)$ (utilizzo di sole variabili scalari locali)
