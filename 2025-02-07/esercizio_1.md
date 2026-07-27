# Esercizio 1 — SortJoin con max-heap

[← Torna all'appello](README.md)

## Testo

**Esercizio 1 (10 punti)**

Siano dati due array $A[1 \dots 2n]$ e $B[1 \dots n]$ organizzati a max-heap, entrambi
contenenti $n$ elementi (`heapsize=n`).

Realizzare una procedura `SortJoin(A, B, n)` che dati in input array $A$ e $B$
con le proprietà sopra descritte, ritorna in $A$ un array ordinato contenente
tutti i $2n$ elementi originariamente presenti in $A$ e $B$.

L'array $B$ può essere modificato durante l'esecuzione della procedura, se
necessario, ma l'algoritmo dovrà operare in *spazio costante*.

Dare lo pseudocodice della procedura, motivarne la correttezza e valutarne la
complessità. Se si utilizzano operazioni sui max-heap andranno definite
esplicitamente.

---

## Soluzione

L'idea è sfruttare il fatto che $A$ e $B$ sono già due max-heap.

In un max-heap, il massimo elemento si trova sempre nella radice. Quindi, finché
ci sono elementi nei due heap, il massimo tra tutti gli elementi non ancora
inseriti nell'array finale si trova necessariamente in una delle due radici:

$$ A[1] \quad \text{oppure} \quad B[1] $$

Riempiamo quindi l'array $A$ da destra verso sinistra, cioè dalle posizioni
$2n, 2n-1, \dots, 1$.

A ogni passo:

- se uno dei due heap è vuoto, estraiamo dall'altro;
- altrimenti confrontiamo le due radici;
- estraiamo il massimo tra le due radici;
- lo inseriamo nella posizione corrente di $A$.

In questo modo, gli elementi più grandi vengono messi nelle posizioni finali di
$A$, e alla fine $A[1 \dots 2n]$ risulta ordinato in senso crescente.

Poiché l'array $A$ ha dimensione $2n$, le posizioni oltre `A.heapsize` vengono
usate per costruire l'output. L'algoritmo usa solo un numero costante di
variabili ausiliarie.

---

## Operazioni sui max-heap

Usiamo le seguenti operazioni su max-heap.

La procedura `MaxHeapify` assume che i figli del nodo in posizione $i$, se
esistono, siano già radici di max-heap validi. La procedura ripristina la
proprietà di max-heap scendendo lungo l'albero.

Per rispettare il vincolo di spazio costante, la scriviamo in forma iterativa.

```text
MaxHeapify(H, heapsize, i)
    while true
        left = 2i
        right = 2i + 1
        largest = i

        if left <= heapsize and H[left] > H[largest]
            largest = left

        if right <= heapsize and H[right] > H[largest]
            largest = right

        if largest == i
            break

        swap H[i] with H[largest]
        i = largest
```

La procedura `ExtractMax` estrae il massimo dal max-heap e aggiorna la dimensione
corrente dello heap.

```text
ExtractMax(H, heapsize)
    if heapsize < 1
        error

    max = H[1]

    H[1] = H[heapsize]
    heapsize = heapsize - 1

    if heapsize > 0
        MaxHeapify(H, heapsize, 1)

    return max
```

Qui `heapsize` viene passato per riferimento, cioè la sua modifica rimane valida
anche dopo la chiamata.

---

## Pseudocodice di `SortJoin`

```text
SortJoin(A, B, n)
    heapA = n
    heapB = n

    for i = 2n downto 1
        if heapA == 0
            A[i] = ExtractMax(B, heapB)

        else if heapB == 0
            A[i] = ExtractMax(A, heapA)

        else if A[1] >= B[1]
            A[i] = ExtractMax(A, heapA)

        else
            A[i] = ExtractMax(B, heapB)

    return A[1...2n]
```

---

## Correttezza

Dimostriamo la correttezza tramite il seguente invariante di ciclo.

All'inizio di ogni iterazione del ciclo con indice $i$:

1. $A[1 \dots \text{heapA}]$ è un max-heap;
2. $B[1 \dots \text{heapB}]$ è un max-heap;
3. questi due heap contengono esattamente gli elementi non ancora inseriti nella
   parte ordinata finale;
4. $A[i+1 \dots 2n]$ contiene i $2n - i$ elementi più grandi tra quelli originari di
   $A$ e $B$, ordinati in senso crescente.

### Inizializzazione

All'inizio del ciclo, per $i = 2n$, entrambi gli array sono max-heap per ipotesi:

$$ \text{heapA} = n $$
$$ \text{heapB} = n $$

La parte $A[i+1 \dots 2n]$ è vuota, quindi contiene correttamente zero elementi già
ordinati. L'invariante vale.

### Mantenimento

Supponiamo che l'invariante valga all'inizio di un'iterazione.

Il massimo tra tutti gli elementi non ancora inseriti deve trovarsi in una delle
due radici, perché entrambi gli array ancora attivi sono max-heap. Quindi il
massimo è in $A[1]$ oppure in $B[1]$.

L'algoritmo confronta queste due radici, estrae il maggiore dei doppi elementi e
lo inserisce in $A[i]$.

Dopo l'estrazione, `ExtractMax` richiama `MaxHeapify`, quindi lo heap da cui è
stato rimosso l'elemento torna a soddisfare la proprietà di max-heap. L'altro
heap non viene modificato.

Inoltre, l'elemento inserito in $A[i]$ è il massimo tra quelli non ancora
ordinati. Poiché $A[i+1 \dots 2n]$ conteneva già gli elementi più grandi inseriti in
precedenza, $A[i \dots 2n]$ rimane ordinato in senso crescente.

L'invariante è quindi mantenuto.

### Terminazione

Il ciclo termina dopo avere riempito tutte le posizioni da $2n$ fino a $1$.

Per l'invariante, $A[1 \dots 2n]$ contiene tutti gli elementi originariamente presenti
in $A$ e $B$, ordinati in senso crescente.

Quindi `SortJoin` è corretta.

---

## Nota sullo spazio costante

L'algoritmo scrive il risultato direttamente dentro $A$.

L'assegnazione in $A[i]$ non sovrascrive elementi ancora da estrarre dallo heap
di $A$: infatti, all'inizio di ogni iterazione, gli elementi ancora non ordinati
sono esattamente $\text{heapA} + \text{heapB} = i$.

Se $\text{heapB} > 0$, allora $i > \text{heapA}$, quindi $A[i]$ è fuori dalla porzione di $A$
usata come heap.

Se invece $\text{heapB} = 0$, l'algoritmo estrae prima da $A$, diminuendo $\text{heapA}$, e
solo dopo scrive in $A[i]$.

Quindi l'output può essere costruito in $A$ senza usare memoria aggiuntiva non
costante.

---

## Complessità

La procedura `MaxHeapify` costa:

$$ O(\log n) $$

Anche `ExtractMax` costa:

$$ O(\log n) $$

perché esegue una chiamata a `MaxHeapify`.

Il ciclo principale esegue esattamente $2n$ estrazioni. Quindi il tempo totale è:

$$ \Theta(n \log n) $$

La complessità spaziale è:

$$ O(1) $$

perché l'algoritmo usa solo un numero costante di variabili ausiliarie e
`MaxHeapify` è iterativa.
