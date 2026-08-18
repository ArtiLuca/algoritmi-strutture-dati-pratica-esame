# Esercizio - Minimo tra Min-Heap e Max-Heap

**Domanda A (7 punti)**
Dare la definizione di max-heap.
Dato un insieme $S$ di elementi, memorizzato in parte in un min-heap $A$ e in parte in un max-heap $B$, entrambi non vuoti, dare un algoritmo $\min(A, B)$ per trovare il minimo di $S$ nelle due situazioni seguenti:
(a) ogni elemento di $A$ è minore o uguale a ogni elemento di $B$;
(b) ogni elemento di $B$ è minore o uguale a ogni elemento di $A$.
In entrambi i casi scrivere lo pseudocodice e valutare la complessità.

---

### i. Definizione di Max-Heap

Un max-heap è un albero binario quasi completo, dove per "quasi completo" si intende un albero in cui tutti i livelli sono completamente riempiti tranne possibilmente l’ultimo, nel quale tutte le foglie sono addossate il più possibile a sinistra.

Un max-heap viene tipicamente implementato mediante un array, in cui la radice $A[1]$ contiene il valore massimo dell'intero albero e, per ogni nodo $i$, deve valere la proprietà di ordinamento parziale:
- Ogni nodo $A[i]$ è maggiore o uguale ai suoi figli, se esistono, ovvero: $A[i] \ge A[2i]$ e $A[i] \ge A[2i+1]$.
- Equivalentemente, per ogni nodo $i>1$, vale $A[i] \le A[\lfloor\frac{i}{2}\rfloor]$.

Un min-heap è una struttura dati speculare al max-heap, con la disuguaglianza invertita. In un min-heap, la radice $A[1]$ contiene il valore minimo.

---

### ii. Algoritmo $\min(A, B)$

L'insieme $S$ è composto dall'unione di un min-heap $A$ e un max-heap $B$, entrambi non vuoti.

#### Caso (a): $A \le B$
Se ogni elemento di $A$ è minore o uguale a ogni elemento di $B$ ($\forall x \in A, \forall y \in B \implies x \le y$), allora il minimo globale di $S$ si trova di sicuro all'interno del min-heap $A$.
Essendo $A$ un min-heap, il suo valore minimo corrisponde esattamente al suo primo elemento, ovvero alla sua radice $A[1]$.

```text
min_CasoA(A, B)
    return A[1]
```
**Complessità:** L'accesso alla radice di un array richiede tempo costante. Pertanto, la complessità è $T(n) = \Theta(1)$.

#### Caso (b): $B \le A$
Se ogni elemento di $B$ è minore o uguale a ogni elemento di $A$ ($\forall x \in B, \forall y \in A \implies x \le y$), allora il minimo globale di $S$ si trova necessariamente all'interno del max-heap $B$.
Tuttavia, in un max-heap, gli elementi più piccoli vengono spinti verso il basso. Il valore minimo assoluto si troverà necessariamente in una delle sue foglie.

Pertanto, bisogna trovare il minimo elemento ispezionando tutte e sole le foglie di $B$. In un heap di dimensione $n$, i nodi foglia sono esattamente quelli i cui indici vanno da $\lfloor\frac{n}{2}\rfloor + 1$ fino a $n$.

```text
min_CasoB(A, B)
    n = B.heapsize
    firstLeaf = floor(n/2) + 1
    minimum = B[firstLeaf]

    // Scansiono linearmente tutte le foglie
    for i = firstLeaf + 1 to n
        if B[i] < minimum
            minimum = B[i]

    return minimum				
```
**Complessità:** L'algoritmo esamina linearmente tutte le foglie del max-heap. In un heap binario di dimensione $n$, il numero di foglie è $\lceil \frac{n}{2} \rceil$. Il numero di iterazioni del ciclo è proporzionale a $n$. Di conseguenza, la complessità temporale è lineare rispetto alla dimensione del max-heap, ovvero $T(n) = \Theta(B.heapsize) = \Theta(n)$.
