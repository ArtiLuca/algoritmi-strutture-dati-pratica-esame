# Esercizio 32 — Sottoarray contiguo di somma massima

## Traccia

Realizzare, con tecniche di programmazione dinamica, un algoritmo che dato un array $A[1 \dots n]$, non vuoto, trova un sottoarray non vuoto di somma massima, ovvero due indici $i$ e $j$ con $1 \le i \le j \le n$ tali che $A[i]+A[i+1]+\dots+A[j]$ sia massima.

Ad esempio per `[-10, 4, 1, -1, 2, -1]` il sottoarray di somma massima è `[4, 1, -1, 2]`.

Più precisamente:

- **i.** indicata con $l_j$ la somma massima di un sottoarray di $A[1 \dots n]$ che termini con $A[j]$ (quindi del tipo $A[i \dots j]$), darne una caratterizzazione ricorsiva;
- **ii.** tradurre tale definizione in un algoritmo bottom-up o top-down con memoization che determina la somma massima;
- **iii.** trasformare l'algoritmo in modo che fornisca anche il sottoarray, non solo la sua somma;
- **iv.** valutare la complessità dell'algoritmo.

## Nota

Prima di scrivere la soluzione volevo annotare che il PDF della raccolta dice:

> Inoltre il documento è di recente redazione e può contenere sviste e piccoli errori. Segnalazioni in questo senso sono benvenute.

Per il punto **i**, la notazione $l_j$ potrebbe far pensare alla lunghezza del sottoarray. Tuttavia, per coerenza con la richiesta e con il successivo punto **ii**, definisco $l_j$ come la somma massima di un sottoarray di $A[1 \dots n]$ che termina esattamente all'indice $j$, ovvero del tipo $A[i \dots j]$ per un qualche $i \le j$ ottimale.

## Idea

Possiamo dare una caratterizzazione ricorsiva in base alle seguenti osservazioni:

- Se il sottoarray è composto da un solo elemento, ovvero $j=1$, allora la somma massima sarà necessariamente $l_1 = A[1]$.
- Se invece $1 < j \le n$, per trovare la somma massima del sottoarray che termina in $A[j]$ si deve valutare se ci conviene estendere il sottoarray ottimo precedente oppure ricominciare da capo.
- Ovvero, se $l_{j-1} > 0$, allora conviene concatenare $A[j]$ con il sottoarray ottimo precedente, perché questo aumenta la somma. In questo caso si ha $l_j = l_{j-1} + A[j]$.
- Se invece $l_{j-1} \le 0$, allora non conviene estendere il sottoarray precedente. In questo caso è meglio ricominciare da $A[j]$, quindi $l_j = A[j]$.

## Caratterizzazione ricorsiva

Quindi, una caratterizzazione ricorsiva per il calcolo della somma massima $l_j$ di un sottoarray $A[i \dots j]$ che termina esattamente in $A[j]$ può essere:

$$
l_j =
\begin{cases}
A[j] & \text{se } j=1, \\
A[j] & \text{se } j \gt 1 \text{ e } l_{j-1} \le 0, \\
A[j] + l_{j-1} & \text{se } j \gt 1 \text{ e } l_{j-1} \gt 0.
\end{cases}
$$

Equivalentemente, per $j > 1$ si può scrivere in forma più compatta:

$$
l_j = \max\{A[j],\ A[j] + l_{j-1}\}
$$

## Algoritmo bottom-up

Per il punto **ii** uso un array `L[1..n]`, dove `L[j]` indica la somma massima del sottoarray che termina esattamente all'indice `j`.

Prima si riempie l'array seguendo la ricorrenza e dopodiché si usa una variabile locale `best` per tenere traccia del massimo trovato. In questo modo, alla fine, si restituisce il massimo globale.

```text
maxSubarray(A, n)
    // allocazione array
    allocate L[1..n]

    // caso base
    L[1] = A[1]

    // valore massimo iniziale
    best = A[1]

    for j = 2 to n

        // se conviene estendere
        if L[j-1] > 0
            L[j] = L[j-1] + A[j]

        // altrimenti ricomincio da A[j]
        else
            L[j] = A[j]

        // aggiorna massimo globale
        if L[j] > best
            best = L[j]

    return best
```

## Ricostruzione del sottoarray

Per il punto **iii**, se vogliamo anche ottenere il sottoarray di somma massima trovato, possiamo aggiornare il codice sopra in modo da utilizzare un array `S[1..n]`.

L'array `S` tiene traccia dell'indice di partenza del sottoarray ottimo che termina in una certa posizione.

In particolare, `S[j]` indica l'indice dal quale parte il sottoarray di somma massima che termina esattamente all'indice `j`.

- Se conviene estendere il sottoarray precedente, allora il punto di partenza rimane lo stesso, quindi `S[j] = S[j-1]`.
- Se invece conviene ricominciare da `A[j]`, allora il sottoarray parte proprio da `j`, quindi `S[j] = j`.

Questo array viene poi passato alla procedura `printMaxSubarray(A,S,bestEnd)`, che stampa il sottoarray trovato.

```text
maxSubarray(A, n)
    // allocazione array
    allocate L[1..n]
    allocate S[1..n]

    // caso base
    L[1] = A[1]
    S[1] = 1

    // valore massimo iniziale e fine del sottoarray migliore trovato
    best = A[1]
    bestEnd = 1

    for j = 2 to n

        // se conviene estendere
        if L[j-1] > 0
            L[j] = L[j-1] + A[j]
            S[j] = S[j-1]

        // altrimenti ricomincio da A[j]
        else
            L[j] = A[j]
            S[j] = j

        // aggiorna massimo globale e dove finisce
        if L[j] > best
            best = L[j]
            bestEnd = j

    // stampa del sottoarray di somma massima trovato
    printMaxSubarray(A, S, bestEnd)

    // restituisco somma massima trovata
    return best


printMaxSubarray(A, S, bestEnd)
    start = S[bestEnd]

    for k = start to bestEnd
        print A[k]
```

## Complessità

Per il punto **iv**, la complessità temporale è:

$$
\Theta(n)
$$

Infatti, l'array viene scandito una sola volta e ogni posizione viene calcolata in tempo costante.

Anche la procedura di stampa del sottoarray richiede tempo lineare nella lunghezza del sottoarray stampato, che nel caso peggiore può essere $\Theta(n)$.

La complessità spaziale è:

$$
\Theta(n)
$$

Infatti, usiamo gli array `L[1..n]` e `S[1..n]`, entrambi di dimensione lineare.

Se volessimo calcolare soltanto la somma massima, senza ricostruire il sottoarray, si potrebbe anche ottimizzare lo spazio a $\Theta(1)$ mantenendo solo il valore precedente e il massimo globale.
