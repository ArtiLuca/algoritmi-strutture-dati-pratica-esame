# Esercizio 24 - Estrazione del Minimo in un Min-Heap

Fornire lo pseudocodice della procedura `HeapExtractMin(A)` per estrarre il minimo elemento da un min-heap $A$, realizzato tramite un array come visto a lezione (la dimensione corrente dello heap è data dall'attributo `A.heapsize`). Discuterne la complessità.

---

### i. Idea e Ragionamento

Per estrarre il minimo elemento da un min-heap $A$ possiamo implementare una procedura `HeapExtractMin(A)` che agisce in modo speculare a `ExtractMax(A)` per i max-heap visti a lezione. Il minimo si trova sempre nella radice dello heap ($A[1]$).
Una volta salvato il minimo, lo si sostituisce con l'ultimo elemento dello heap ($A[A.heapsize]$), si riduce la dimensione dello heap di 1 e si ripristina la proprietà dell'albero.

Per il ripristino serve una procedura `MinHeapify(A, i)` per mantenere le proprietà del min-heap. Questa procedura può essere implementata in modo analogo a `MaxHeapify(A, i)`, ma adattata per i min-heap.
La procedura `MinHeapify(A, i)` aggiusta una possibile violazione al nodo $i$ assumendo come pre-condizione che i sottoalberi radicati nei figli sinistro e destro di $i$ siano già min-heap validi.

---

### ii. Pseudocodice

```algorithmic
// aggiusta una possibile violazione in A[i]
// pre: i figli di i sono radici di sottoalberi che sono già min-heap validi
MinHeapify(A, i)
    l = 2 * i
    r = 2 * i + 1

    if (l <= A.heapsize) and (A[l] < A[i])
        min = l
    else
        min = i

    if (r <= A.heapsize) and (A[r] < A[min])
        min = r

    if min != i
        swap A[i] with A[min]
        MinHeapify(A, min)						
```

La procedura per l’estrazione del minimo elemento può quindi essere implementata come segue:

```algorithmic
// estrae e restituisce il minimo elemento
HeapExtractMin(A)
    // controllo underflow
    if A.heapsize < 1
        return ERROR "Heap underflow"

    // il minimo è sempre nella radice
    min = A[1]

    // sposto l'ultima foglia nella radice
    A[1] = A[A.heapsize]
    A.heapsize = A.heapsize - 1

    // ripristino la proprietà di min-heap scendendo dalla radice
    if A.heapsize > 0
        MinHeapify(A, 1)

    return min
```

---

### iii. Complessità

La complessità temporale di `HeapExtractMin(A)` dipende direttamente dal costo della procedura di ripristino `MinHeapify(A, i)`.

Come nel caso dei max-heap, la complessità di `MinHeapify(A, i)` è proporzionale all'altezza $h$ dell'albero. Poiché un heap è un albero binario quasi completo, la sua altezza è $h = \lfloor \log n \rfloor$. Di conseguenza, il costo di `MinHeapify` è $\mathcal{O}(\log n)$.

Le operazioni di swap e aggiornamento degli indici in `HeapExtractMin(A)` costano $\Theta(1)$.
Pertanto, la complessità temporale complessiva per l'estrazione del minimo risulta essere $\mathcal{O}(\log n)$.
La complessità spaziale è $\mathcal{O}(\log n)$ se `MinHeapify` è ricorsiva (per lo stack), oppure $\mathcal{O}(1)$ se implementata in modo iterativo.
