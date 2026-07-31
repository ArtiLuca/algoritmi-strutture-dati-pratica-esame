# Soluzione - Esercizio 1

Per questo esercizio, anche solo per pratica, ho deciso di mostrare due soluzioni. Una ispirata all'algoritmo `CountingSort` visto a lezione che opera "in-loco", e una seconda più "standard" basata sull'algoritmo di Dijkstra chiamato *Dutch National Flag*.

## Approccio 1: Ispirato da CountingSort

Il primo approccio nasce dall'osservazione che il dominio dei valori è molto ristretto $\{0, 1, 2\}$, suggerendo un approccio basato sul conteggio, come quello del `CountingSort` visto a lezione. Tuttavia, la versione standard di `CountingSort` richiede spazio supplementare. Quindi, per rispettare il vincolo dello spazio $\Theta(1)$ e l'uso esclusivo dell'operazione di scambio $A[i] \leftrightarrow A[j]$, ho deciso di implementare l'algoritmo usando due macro-fasi logiche.

1. **Prima fase:** si scansiona interamente l'array per determinare le frequenze assolute dei valori 0 e 1. Conoscendo queste frequenze, è possibile calcolare a priori i confini esatti delle tre partizioni nell'array finale ordinato.
2. **Seconda fase:** conoscendo la collocazione definitiva dell'array finale, si iterano gli indici delle prime due partizioni. Se si trova un elemento $A[i]$ con valore "fuori posto", si usa una procedura ausiliaria per cercare in avanti da quella posizione dell'array un valore corretto da inserire tramite un'operazione di scambio.

Per garantire che la complessità temporale rimanga $\Theta(n)$ serve cura nella gestione dei puntatori di ricerca della procedura ausiliaria: essi avanzano in modo sempre crescente, non venendo mai ripristinati all'indietro. Quindi il numero totale di avanzamenti dei puntatori resta lineare.

L'operazione di ricerca e riposizionamento viene gestita dalla procedura ausiliaria `findAndSwap`, che prende come parametri un indice `ind` (la posizione dell'elemento correntemente "fuori posto" che stiamo cercando di sistemare), un puntatore di partenza `ptr` (l'indice da cui iniziare la ricerca), il valore target `val` di cui abbiamo bisogno (ad esempio 0 o 1), e un limite superiore `lim` per delimitare l'area di ricerca.

La procedura restituisce una coppia `(swapped, newPtr)`, dove `swapped` agisce da flag booleano per indicare se la ricerca e scambio è avvenuto oppure no, mentre `newPtr` rappresenta il valore aggiornato del puntatore di ricerca, avanzato di una posizione se è avvenuto lo scambio, altrimenti invariato.

### Pseudocodice

    // Cerca ed esegue scambio, restituendo coppia (swapped, newPtr)
    findAndSwap(A, ind, ptr, val, lim)
        while ptr <= lim and A[ptr] != val
            ptr = ptr + 1

        if ptr <= lim
            A[ind] ↔ A[ptr]
            return (true, ptr + 1)

        // altrimenti
        return (false, ptr)


    // Ordina A in senso crescente
    TriSort(A)
        n = A.length

        // variabili di conteggio (degli 0 e 1)
        c0 = 0
        c1 = 0

        // fase di conteggio
        for i = 1 to n
            if A[i] == 0
                c0 = c0 + 1
            else if A[i] == 1
                c1 = c1 + 1

        // fase gestione dei valori 0
        ptr1 = c0 + 1
        ptr2 = c0 + c1 + 1

        for ptr0 = 1 to c0
            if A[ptr0] != 0
                // cerco uno 0 nella zona degli 1, se non c'è lo cerco nella zona dei 2
                (swapped, ptr1) = findAndSwap(A, ptr0, ptr1, 0, c0 + c1)

                if swapped == false
                    (swapped, ptr2) = findAndSwap(A, ptr0, ptr2, 0, n)

        // fase gestione dei valori 1
        // ptr1 riparte dall'inizio della sua zona solo se non ha già superato il limite
        ptr1 = max(ptr1, c0 + 1)

        for i = c0 + 1 to c0 + c1
            if A[i] != 1
                (swapped, ptr2) = findAndSwap(A, i, ptr2, 1, n)

### Correttezza

La correttezza si basa sulle seguenti osservazioni:

- La prima fase calcola le frequenze esatte $c_0$ e $c_1$ in modo da garantire che nell'array finale ordinato, il sottoarray $A[1\dots c_0]$ conterrà solo valori 0 e che il sottoarray $A[c_0+1\dots c_0+c_1]$ conterrà solo valori 1.
- Durante la "sistemazione" degli 0, all'iterazione $k$-esima, il sottoarray $A[1\dots k-1]$ contiene solo 0.
- Se $A[k] \ne 0$, l'algoritmo cerca uno 0 "fuori posto" usando i puntatori `ptr1` e `ptr2` e, poiché abbiamo già contato esattamente quanti 0 esistono nell'intero array, la procedura `findAndSwap` funziona correttamente trovandone uno da scambiare prima di raggiungere la fine.
- Ripetendo la logica per la "sistemazione" degli 1, i sottoarray degli 0 e degli 1 saranno correttamente popolati e quindi gli elementi rimanenti del sottoarray $A[c_0+c_1+1 \dots n]$ saranno necessariamente tutti e soli 2.

Quindi alla fine, l'intero array $A[1\dots n]$ risulta ordinato in senso crescente.

### Complessità e Costi

- **Complessità temporale:** è $\Theta(n)$. La prima fase scansiona l'array una volta per contare i valori. Nella seconda fase, i puntatori di ricerca `ptr1` e `ptr2` avanzano sempre in avanti e non vengono mai riportati indietro. Quindi il numero totale di avanzamenti dei puntatori resta lineare.
- **Spazio:** si usa uno spazio $\Theta(1)$ in quanto le uniche variabili usate sono quelle di conteggio e pochi puntatori.
- **Numero di confronti:** nel caso peggiore è $O(n)$, più precisamente limitato superiormente da una costante per $n$. Una possibile stima è al più $5n$: $2n$ confronti per la fase di conteggio e al più $3n$ per gli avanzamenti incrociati di `ptr0`, `ptr1` e `ptr2`.
- **Numero di scambi:** nel caso peggiore è $O(n)$, più precisamente al più $n$. Ogni scambio posiziona definitivamente almeno un elemento, con il valore corretto spostato all'indice `ind`.

---

## Approccio 2: Ispirato dall'algoritmo di Dijkstra (Dutch National Flag)

Un secondo approccio si basa sull'algoritmo di Dijkstra noto come *Dutch National Flag*. Questo approccio risulta più efficiente in termini di costanti in quanto richiede una singola scansione dell'array. L'idea principale è di costruire le partizioni dinamicamente anziché calcolare le loro dimensioni a priori, facendole convergere verso il centro.

L'algoritmo utilizza tre indici per mantenere quattro regioni logiche nell'array:

- `low`: per delimitare la partizione degli 0;
- `high`: per delimitare la partizione dei 2;
- `mid`: che agisce come un puntatore di ricerca per gli elementi non ancora analizzati.

Ad ogni iterazione, si valuta il valore in $A[\text{mid}]$. Se è un valore 0 o 2, si spinge immediatamente nella sua regione definitiva tramite uno scambio rispettivamente con `low` o `high`. Se è un valore 1, viene semplicemente "scavalcato" da `mid`. Questo processo garantisce il mantenimento dei vincoli "in-place" e termina quando la regione degli elementi da esplorare si esaurisce, ovvero $\text{mid} > \text{high}$.

### Pseudocodice

    TriSort(A)
        n = A.length
        low = 1
        mid = 1
        high = n

        while mid <= high
            if A[mid] == 0
                A[low] ↔ A[mid]
                low = low + 1
                mid = mid + 1
            else if A[mid] == 1
                mid = mid + 1
            else // A[mid] == 2
                A[mid] ↔ A[high]
                high = high - 1

### Correttezza

All'inizio di ogni iterazione, l'array è logicamente diviso in 4 regioni contigue:

- $A[1\dots \text{low}-1]$: composto solo da valori 0;
- $A[\text{low}\dots \text{mid}-1]$: composto solo da valori 1;
- $A[\text{mid}\dots \text{high}]$: composto da elementi non ancora analizzati, ovvero "sconosciuti";
- $A[\text{high}+1 \dots n]$: composto solo da valori 2.

Ad ogni passo viene esaminato l'elemento $A[\text{mid}]$. A seconda del valore, cioè 0, 1, oppure 2, l'elemento viene scambiato nella rispettiva regione e si aggiornano i puntatori, riducendo di 1 la dimensione della regione degli elementi sconosciuti:

$$\text{high} - \text{mid} + 1$$

Il ciclo termina quando $\text{mid} > \text{high}$, nel qual caso la regione dei valori da analizzare risulta vuota e quindi l'array finale risulta ordinato in senso crescente.

### Complessità e Costi

- **Complessità temporale:** è $\Theta(n)$ in quanto ogni iterazione esegue lavoro costante su un elemento e si eseguono al massimo $n$ cicli.
- **Spazio:** si usa uno spazio aggiuntivo $\Theta(1)$.
- **Numero di confronti:** nel caso peggiore, si eseguono due controlli ad ogni iterazione, e quindi al più $2n$ confronti sui valori.
- **Numero di scambi:** ogni volta che eseguiamo uno scambio per uno 0 o un 2, l'elemento viene posizionato nella sua regione definitiva. Poiché l'array potrebbe non contenere alcun valore 1, il numero di scambi nel caso peggiore è dunque pari ad $n$, ovvero dipende dall'istanza del problema.
