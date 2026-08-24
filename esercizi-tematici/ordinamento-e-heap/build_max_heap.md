# Domanda 25

Dare la definizione di max-heap. Dato un array $A[1\dots 12]$ con sequenza di elementi $[60, 6, 45, 95, 30, 24, 15, 80, 19, 38, 21, 70]$ si indichi il risultato della procedura `BuildMaxHeap` applicata ad $A$. Si descriva sinteticamente come si procede per arrivare al risultato.

---

### i. Definizione di Max-Heap

Un max-heap è un albero binario quasi completo, dove per albero binario quasi completo si intende un albero binario con tutti i livelli completi, tranne che per l’ultimo in cui tutte le foglie sono addossate a sinistra.

Un max-heap è tipicamente implementato mediante un array dove la radice $A[1]$ contiene il massimo, mentre $A.heapsize$ indica il numero di elementi effettivamente in uso. In particolare, per ogni nodo all'indice $i$ devono valere le seguenti condizioni per mantenere la proprietà di max-heap:
- $A[i] \ge A[2i]$ se il figlio sinistro all’indice $2i$ esiste.
- $A[i] \ge A[2i+1]$ se il figlio destro all’indice $2i+1$ esiste.

In modo speculare, si ha che per ogni nodo a un indice $i > 1$ deve valere:

$$
A[i] \le A[\lfloor i / 2 \rfloor]
$$

---

### ii. Procedura BuildMaxHeap

La procedura `BuildMaxHeap(A)` trasforma un array arbitrario in un max-heap in tempo $\Theta(n)$ usando la procedura `MaxHeapify(A, i)`. In particolare, parte dall’indice $i = \lfloor A.heapsize / 2 \rfloor$ e poi scende fino all’indice $i=1$ facendo chiamate a `MaxHeapify(A, i)`, che si occupa di aggiustare possibili violazioni del nodo $i$ con i suoi immediati discendenti.

La procedura `MaxHeapify(A, i)` assume che il nodo radicato in $i$ abbia già sottoalberi che siano dei validi max-heap, ed è per questo motivo che si inizia dal primo nodo non-foglia (essendo che le foglie rappresentano dei max-heap triviali). La procedura `MaxHeapify` verifica se il nodo $i$ viola la proprietà di max-heap con i suoi discendenti ai nodi $2i$ e $2i+1$ (se esistono) e li scambia se trova una violazione. Questo accade solamente quando trova un nodo $i$ con valore più piccolo di uno dei suoi immediati discendenti. Dopo lo scambio, la procedura continua ricorsivamente verso il basso, operando sul nodo appena scambiato in quanto potrebbe ora anche lui violare la proprietà di max-heap.

---

### iii. Esecuzione su Array Specifico

Inizialmente abbiamo:
$A = [60, 6, 45, 95, 30, 24, 15, 80, 19, 38, 21, 70]$

L’indice iniziale del ciclo sarà $i = \lfloor A.heapsize / 2 \rfloor = 6$. Mostriamo il procedimento per le prime chiamate:

- La procedura `MaxHeapify(A, 6)` verifica che il nodo $A[6] = 24$ viola la proprietà di max-heap con il suo figlio sinistro $A[12] = 70$ (il figlio destro non esiste) e quindi li scambia. Dopodiché la chiamata ricorsiva `MaxHeapify(A, 12)` non fa niente in quanto foglia.
- La chiamata `MaxHeapify(A, 5)` verifica che il nodo $A[5] = 30$ viola la proprietà con il figlio destro $A[11] = 21$ e il figlio sinistro $A[10] = 38$. Lo scambia con il massimo ($38$), e poi la chiamata ricorsiva `MaxHeapify(A, 10)` non fa niente.
- La chiamata `MaxHeapify(A, 4)` invece non fa niente, essendo che il nodo $A[4] = 95$ è già il massimo e quindi non viola la proprietà con nessuno dei suoi discendenti $A[8] = 80$ o $A[9] = 19$.

Questo continua a cascata fino alla chiamata `MaxHeapify(A, 1)`.
Dopo il completamento della procedura `BuildMaxHeap(A)`, l’array finale risulta essere:

$$
A = [95, 80, 70, 60, 38, 45, 15, 6, 19, 30, 21, 24]
$$
