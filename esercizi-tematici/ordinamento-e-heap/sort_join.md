## SortJoin

Siano dati due array $A[1 \dots 2n]$ e $B[1 \dots n]$ organizzati a max-heap, entrambi contenenti $n$ elementi (`heapsize=n`).

Realizzare una procedura `SortJoin(A, B, n)` che dati in input array $A$ e $B$ con le proprietà sopra descritte, ritorna in $A$ un array ordinato contenente tutti i $2n$ elementi originariamente presenti in $A$ e $B$.

L'array $B$ può essere modificato durante l'esecuzione della procedura, se necessario, ma l'algoritmo dovrà operare in *spazio costante*.

Dare lo pseudocodice della procedura, motivarne la correttezza e valutarne la complessità. Se si utilizzano operazioni sui max-heap andranno definite esplicitamente.

---

### i. Idea e Pseudocodice

Per operare in spazio costante, possiamo notare che $A$ e $B$ sono entrambi *max-heap* composti da $n$ elementi, ovvero $\text{A.heapsize} = \text{B.heapsize} = n$. Essendo che $A[1\dots 2n]$ è in grado di contenere entrambi, possiamo riempire l’array $A[1\dots 2n]$ da destra verso sinistra, inserendo il massimo estratto da uno dei due *max-heap*.

Ovvero, durante il riempimento:
- Se $\text{A.heapsize} = 0$ allora bisogna necessariamente usare un elemento del *max-heap* $B$.
- Se $\text{B.heapsize} = 0$ allora bisogna necessariamente usare un elemento del *max-heap* $A$.
- Altrimenti, si confrontano i massimi di ciascun *max-heap* (situati in $A[1]$ e $B[1]$ essendo organizzati come *max-heap*) e si inserisce il massimo trovato.

In questo modo, alla fine del riempimento da destra verso sinistra, l’array $A[1\dots 2n]$ conterrà tutti gli elementi originari di $A$ e $B$ ordinati in senso crescente.

Come richiesto dall’esercizio, vanno esplicitate le due procedure utilizzate sui *max-heap*.
Queste sono `ExtractMax(H)` che estrae il massimo dal *max-heap* e poi ripristina le proprietà che lo rendono *max-heap* utilizzando una seconda procedura `MaxHeapify(H, i)`. La procedura `MaxHeapify(H, i)` aggiusta una possibile violazione verso il basso e assume che i nodi figli del sottoalbero radicato al nodo $i$ siano già dei *max-heap* validi prima della sua esecuzione.
In particolare, serve una versione **iterativa** per `MaxHeapify(H, i)` per soddisfare la richiesta di *spazio costante* del testo dell’esercizio.

Le due procedure utilizzate per i *max-heap* sono riportate sotto:

```text
// estrae massimo e ripristina proprieta max-heap
ExtractMax(H)
    max = H[1]
    H[1] = H[H.heapsize]
    H.heapsize = H.heapsize - 1
    MaxHeapify(H, 1)
    return max

// Procedura iterativa per mantenimento proprieta max-heap
// pre: assume che i figli di i siano radici di max-heap gia validi
MaxHeapify(H, i)		
    n = H.heapsize
    while true
        left = 2 * i
        right = 2 * i + 1
        max = i

        if (left <= n) and (H[left] > H[max])
            max = left

        if (right <= n) and (H[right] > H[max])
            max = right		

        if max == i
            return  // break, la proprieta' e' ripristinata

        swap H[i] with H[max]
        i = max												
```

La procedura principale `SortJoin(A, B, n)` invece:

```text
SortJoin(A, B, n)
    for i = 2*n downto 1
        if A.heapsize == 0
            A[i] = ExtractMax(B)
        else if B.heapsize == 0
            A[i] = ExtractMax(A)
        else
            if A[1] >= B[1]
                A[i] = ExtractMax(A)
            else
                A[i] = ExtractMax(B)

    return A[1...2n]												
```

---

### ii. Correttezza

Per dimostrare la correttezza di `SortJoin(A, B, n)` utilizzo la seguente invariante di ciclo:

*All’inizio di ciascuna iterazione del ciclo con indice* $i$, $A[1\dots A.heapsize]$ *e* $B[1\dots B.heapsize]$ *sono dei max-heap validi e contengono tutti gli elementi non ancora inseriti nella parte ordinata finale.* $A[i+1\dots 2n]$ *contiene i* $2n - i$ *elementi più grandi tra quelli originari in* $A$ *e* $B$, *ordinati in senso crescente.*

**Inizio ($i = 2n$):** Si ha $A[1\dots A.heapsize]$ e $B[1\dots B.heapsize]$ max-heap validi e la parte finale ordinata $A[i+1\dots 2n]$ è vuota, quindi contiene zero elementi ordinati e l’invariante è vacuamente vera.

**Mantenimento:** Ad ogni iterazione viene estratto e inserito in $A[i]$ l’elemento massimo tra i due max-heap, utilizzando la procedura `ExtractMax` che a sua volta invoca `MaxHeapify` per ripristinare la proprietà di max-heap sul max-heap da cui si prende il massimo, essendo che dopo l’estrazione può avvenire una violazione. `MaxHeapify` funziona correttamente e quindi dopo una estrazione l'heap torna ad essere un max-heap valido. Inoltre, `ExtractMax` decrementa il suo numero effettivo di elementi correttamente e quindi $A[i]$ corrisponde sempre a uno spazio "libero" sicuro per l’inserimento.
L’elemento inserito in $A[i]$ è il massimo tra gli elementi di $A$ e $B$ non ancora ordinati e, poiché $A[i+1\dots 2n]$ conteneva già gli elementi massimi inseriti in precedenza, $A[i\dots 2n]$ rimane ordinato in senso crescente.

**Fine ($i = 0$):** L’algoritmo termina quando ogni elemento di $A$ e $B$ è stato inserito in $A[1\dots 2n]$, confrontando e inserendo il massimo tra i due max-heap. Dopo tutti gli inserimenti $A$ e $B$ sono dei max-heap triviali (vuoti) e, avendo estratto e inserito il massimo globale fra i due ad ogni iterazione, riempiendo da destra verso sinistra, l’array finale $A[1\dots 2n]$ risulta completamente ordinato in senso crescente.

---

### iii. Complessità

Il costo di `ExtractMax` deriva dal costo di `MaxHeapify`, ovvero $\mathcal{O}(\log n)$, e si fanno esattamente $2n$ chiamate, una per ciascuna estrazione. Quindi la complessità temporale complessiva è:

$$
T(n) = 2n \cdot \mathcal{O}(\log n) = \Theta(n \log n)
$$

Come richiesto dall’esercizio, l’algoritmo opera in spazio costante, in quanto non alloca array ausiliari e si usa esplicitamente una versione iterativa della procedura `MaxHeapify` (evitando così lo spazio dello stack per la ricorsione). Quindi lo spazio complessivo utilizzato è, come richiesto:

$$
S(n) = \Theta(1)
$$
