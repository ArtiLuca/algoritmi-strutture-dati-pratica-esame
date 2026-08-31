# Esercizio 1 — Ordinamento usando Strutture Note

Sia dato un array $A[1..n]$ che rappresenta un max-heap valido.
Realizzare un algoritmo che stampi tutti gli elementi di $A$ in ordine decrescente senza modificare $A$.
Fornire pseudocodice, dimostrazione di correttezza, complessità temporale e complessità spaziale ausiliaria.

---

### i. Idea e Pseudocodice

Poiché è esplicitamente richiesto di non modificare l'array originale $A$, la strategia più semplice ed efficace è quella di creare una copia locale dell'array, che chiameremo $H$.
Essendo $A$ un max-heap valido, anche la sua esatta copia $H$ sarà immediatamente un max-heap valido. A questo punto, possiamo sfruttare le procedure note sugli heap (`ExtractMax` e `MaxHeapify`) per estrarre e stampare ripetutamente il massimo dalla copia $H$, finché non si svuota, assicurando il ripristino delle proprietà strutturali dopo ogni estrazione.

```text
// Procedura principale
PrintHeapDescending(A, n)
    // 1. Creazione della copia (spazio ausiliario)
    allocate H[1...n]
    for i = 1 to n
        H[i] = A[i]
    H.size = n

    // 2. Estrazione e stampa
    for i = 1 to n
        x = ExtractMax(H)
        print x			

// Procedure ausiliarie note
ExtractMax(H)
    max = H[1]
    H[1] = H[H.size]
    H.size = H.size - 1
    MaxHeapify(H, 1)
    return max

MaxHeapify(H, i)
    l = 2i
    r = 2i + 1
    max = i

    if l <= H.size and H[l] > H[i]
        max = l

    if r <= H.size and H[r] > H[max]
        max = r

    if max != i
        swap H[i] with H[max]
        MaxHeapify(H, max)								
```

---

### ii. Correttezza

La correttezza dell'algoritmo si dimostra analizzando il comportamento della copia e le proprietà del max-heap:

1. **Invariante strutturale iniziale:** La procedura inizia copiando elemento per elemento l'array $A$ in $H$. Poiché per ipotesi $A$ è un max-heap valido, la sua copia $H$ gode nativamente della proprietà del max-heap (per ogni nodo $i$, $H[\text{parent}(i)] \ge H[i]$).
2. **Estrazione del massimo:** La funzione `ExtractMax(H)` preleva sempre l'elemento in $H[1]$. In un max-heap valido, la radice $H[1]$ contiene per definizione il valore massimo assoluto tra tutti gli elementi correnti.
3. **Ripristino dell'invariante:** Dopo aver prelevato il massimo, `ExtractMax` sostituisce la radice con l'ultima foglia, decrementa la dimensione logica dell'heap e invoca `MaxHeapify(H, 1)`. La procedura `MaxHeapify` fa "scendere" la nuova radice fino alla sua posizione corretta, ripristinando in modo garantito la proprietà del max-heap per i restanti $n-1$ elementi.
4. **Ordinamento decrescente:** Iterando questo processo esattamente $n$ volte, ad ogni passo $k$ viene stampato il massimo tra gli $n-k+1$ elementi rimanenti. Estraendo sempre il massimo corrente, la sequenza prodotta in output sarà per forza di cose monotonicamente non crescente (ordinata in modo decrescente).
5. **Integrità dell'input:** Tutte le operazioni distruttive (scambi di elementi e decremento della variabile `size`) avvengono unicamente sull'array ausiliario $H$. L'array $A$ viene unicamente letto durante il ciclo di copia iniziale, garantendo il pieno rispetto del vincolo posto dal problema.

---

### iii. Complessità

- **Complessità Temporale:** La fase di copia iniziale dell'array richiede tempo $\Theta(n)$. Successivamente, viene eseguito un ciclo `for` di $n$ iterazioni. Ad ogni iterazione viene invocata `ExtractMax(H)`. Poiché l'altezza dell'heap è logaritmica rispetto al numero di elementi, `MaxHeapify` opera in tempo $\mathcal{O}(\log n)$. Il ciclo costa quindi $\mathcal{O}(n \log n)$. La complessità temporale totale è dominata dalle estrazioni, risultando in:

$$
T(n) = \Theta(n \log n)
$$

- **Complessità Spaziale Ausiliaria:** L'algoritmo richiede l'allocazione di un array secondario $H$ di dimensione $n$ per non alterare l'array originale. Questo costa $\Theta(n)$ spazio. Inoltre, se `MaxHeapify` è implementata ricorsivamente (come in questo pseudocodice), lo stack delle chiamate richiede ulteriore spazio $\mathcal{O}(\log n)$. Lo spazio ausiliario totale allocato dall'algoritmo è dunque dominato dall'array copia:

$$
S(n) = \Theta(n)
$$
