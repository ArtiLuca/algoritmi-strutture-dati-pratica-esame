# Esercizio 28 — Longest Increasing Subsequence

## Traccia

Data una sequenza di numeri $X = x_1 x_2 \dots x_n$ si vuole determinare una sottosequenza:

$$
x_{i_1} x_{i_2} \dots x_{i_k}
$$

di $X$, crescente, ovvero tale che:

$$
x_{i_1} \le x_{i_2} \le \dots \le x_{i_k}
$$

e di lunghezza massima.

Ad esempio, se:

```text
X = [77, 69, 70, 19, 71, 25, 52, 26, 28, 64]
```

una sottosequenza crescente di lunghezza massima è:

```text
[19, 25, 26, 28, 64]
```

Più precisamente:

- **i.** fornire una caratterizzazione ricorsiva della lunghezza $l_i$ di una sottosequenza crescente di lunghezza massima che abbia come primo carattere $x_i$;
- **ii.** tradurre tale definizione in un algoritmo `LIS(X,n)` bottom-up o top-down con memoization che determina la lunghezza di una sottosequenza crescente di lunghezza massima della sequenza $X[1 \dots n]$;
- **iii.** trasformare l'algoritmo in modo che individui anche la sottosequenza, non solo la sua lunghezza;
- **iv.** valutare la complessità dell'algoritmo.

## Idea

Per il punto **i** possiamo definire $\ell_i$ come la lunghezza della sottosequenza crescente di lunghezza massima che inizia esattamente all'indice `i`, ovvero che ha come primo elemento il valore $x_i$.

Data la sequenza:

$$
X = \langle x_1, x_2, \dots, x_n \rangle
$$

una *Increasing Subsequence* che parte da $x_i$ si può estendere solo aggiungendo un elemento successivo $x_j$, con $j > i$, tale che:

$$
x_i \le x_j
$$

Di conseguenza, il problema di trovare la LIS che parte da $x_i$ consiste nel guardare in avanti, verso destra, per cercare un elemento $x_j$ compatibile che faccia partire la sottosequenza più lunga possibile, e aggiungerci `1`, cioè il carattere $x_i$ stesso.

Possiamo dare una caratterizzazione ricorsiva in base alle seguenti osservazioni:

- Se $i > n$, abbiamo superato i limiti della sequenza e non possiamo costruire una sottosequenza. Quindi la lunghezza in questo caso è `0`.
- Se $1 \le i \le n$, la lunghezza della LIS considerata sarà `1`, per il carattere $x_i$, più il massimo tra le lunghezze delle sottosequenze che partono da un indice $j \in [i+1 \dots n]$, a patto che $x_j$ sia crescente rispetto a $x_i$, ovvero $x_i \le x_j$.
- Se non ci sono elementi successivi compatibili, l'insieme del massimo è vuoto, che per convenzione vale `0`, e quindi la lunghezza sarà semplicemente `1`.

## Caratterizzazione ricorsiva

Riassumendo, possiamo definire una ricorrenza per $\ell_i$ come segue:

$$
\ell_i =
\begin{cases}
0 & \text{se } i \gt n, \\
1 + \max\{\ell_j \mid i \lt j \le n \text{ e } x_i \le x_j\} & \text{se } i \le n.
\end{cases}
$$

Nota: si assume che il massimo di un insieme vuoto sia `0`.

## Algoritmo con memoization

Per quanto riguarda il punto **ii**, possiamo implementare un algoritmo ricorsivo top-down con memoization utilizzando un array $L[0..n]$, dove $L[i]$ rappresenta il valore $\ell_i$ come definito dalla ricorrenza sopra.

Per trovare la soluzione globale seguo la seguente convenzione: si usa un elemento sentinella $x_0 = -\infty$, in modo tale che la LIS dell'intera sequenza $X$ sarà uguale alla LIS della sequenza estesa che inizia esattamente in $x_0$, meno `1`, per non contare l'elemento sentinella.

Si usa un algoritmo di inizializzazione `initLIS(X)` per il riempimento iniziale e l'impostazione della convenzione sopra su $x_0$.

Poi viene chiamata la routine ricorsiva `recLIS(X,n,i,L)` per calcolare ricorsivamente la soluzione.

```text
// Procedura di inizializzazione
initLIS(X)
    n = length(X)

    // allocazione array
    allocate L[0..n]

    // impostazione convenzione sul minimo globale
    X[0] = -∞

    // riempimento array con valore di default
    for i = 0 to n
        L[i] = -1

    // invocazione routine ricorsiva partendo dall'elemento sentinella
    // si sottrae 1 perché non vogliamo contare X[0] nella lunghezza finale
    return recLIS(X, n, 0, L) - 1


// Routine ricorsiva
recLIS(X, n, i, L)

    // se sottoproblema non è stato ancora risolto
    if L[i] == -1
        maxLen = 0

        // si cerca l'estensione migliore possibile
        for j = i + 1 to n

            // se trovo un elemento compatibile
            if X[i] <= X[j]
                q = recLIS(X, n, j, L)

                // aggiorno il massimo se ho trovato un'estensione migliore
                if q > maxLen
                    maxLen = q

        // si salva il risultato trovato
        L[i] = maxLen + 1

    // restituisco il risultato trovato
    return L[i]
```

## Ricostruzione della sottosequenza

Per quanto riguarda il punto **iii**, possiamo modificare l'algoritmo sopra in modo da utilizzare un array $S[0..n]$, dove $S[i]$ indica l'indice `j` con cui abbiamo ottenuto un valore di $\ell_j$ massimo.

Ovvero, $S[0..n]$ contiene tutti i successori, partendo dal nostro elemento sentinella $S[0]$, che abbiamo trovato per costruire la soluzione ottima finale.

Quindi alla fine basta passare `S` ad una procedura iterativa per eseguire la stampa della soluzione con un'unica scansione lineare dell'array $S[0..n]$.

Inoltre, si cambia la routine ricorsiva `recLIS(X,n,i,L,S)` in modo che prenda `S` come parametro di input.

```text
// Procedura di inizializzazione
initLIS(X)
    n = length(X)

    // allocazione array
    allocate L[0..n]
    allocate S[0..n]

    // impostazione convenzione sul minimo globale
    X[0] = -∞

    // riempimento array con valore di default
    // usiamo 0 per S per indicare l'assenza di successore
    for i = 0 to n
        L[i] = -1
        S[i] = 0

    // invocazione routine ricorsiva, restituisce lunghezza massima trovata
    maxLength = recLIS(X, n, 0, L, S) - 1

    // stampo solo se risultato non è 0
    if maxLength > 0
        printLIS(X, n, S)

    // restituisco come prima
    return maxLength


// Routine ricorsiva
recLIS(X, n, i, L, S)

    // se sottoproblema non risolto
    if L[i] == -1
        maxLen = 0

        // uso una variabile per ricordare il miglior successore j
        best = 0

        for j = i + 1 to n

            if X[i] <= X[j]
                q = recLIS(X, n, j, L, S)

                // se trovo un'estensione migliore, aggiorno le variabili
                if q > maxLen
                    maxLen = q
                    best = j

        L[i] = maxLen + 1

        // salvo permanentemente la scelta ottima per l'indice i
        S[i] = best

    return L[i]


// Procedura per stampa della soluzione
printLIS(X, n, S)
    i = 0

    // continuo finché abbiamo successori validi
    while S[i] != 0
        print X[S[i]]

        // passo al prossimo successore
        i = S[i]
```

## Complessità

Per quanto riguarda il punto **iv**, la complessità temporale complessiva è quadratica, ovvero:

$$
O(n^2)
$$

Questo si può vedere dal fatto che, per ogni indice `i`, il ciclo `for` esamina tutti gli indici successivi $j > i$.

Nel caso peggiore, il numero totale di confronti è  
  
  $\sum_{i=1}^{n} (n-i) = \frac{n(n+1)}{2}$

e quindi il costo complessivo è:

$$
\Theta(n^2)
$$

Ovvero, abbiamo solo `n` sottoproblemi principali, ma ciascun sottoproblema può richiedere una scansione lineare degli elementi successivi.

Inoltre, il costo per la stampa è:

$$
\Theta(n)
$$

e viene quindi assorbito da $\Theta(n^2)$.

Per quanto riguarda la complessità spaziale, questa è data dalla dimensione degli array $L[0..n]$ e $S[0..n]$, che sono entrambi lineari.

Inoltre, le chiamate ricorsive occupano spazio ulteriore sullo stack che, nel caso peggiore, è $O(n)$.

Quindi la complessità spaziale complessiva si può esprimere come:

$$
O(n)
$$
