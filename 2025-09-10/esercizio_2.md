# Esercizio 2 — Ricorrenza memoizzata

[← Torna all'appello](README.md)

## Testo

**Esercizio 2 (9 punti)**

Sia $n>0$ un intero. Si consideri la seguente ricorrenza $M(i,j)$, definita su
tutte le coppie $(i,j)$ con $1\le i\le j\le n$:

```math
M(i,j)=
\begin{cases}
1 & \text{se } i=j,\\
2 & \text{se } j=i+1,\\
M(i+1,j-1)\cdot M(i+1,j)\cdot M(i,j-1)
& \text{se } j>i+1.
\end{cases}
```

### Punto (a)

Scrivere una coppia di algoritmi `INIT_M(n)` e `REC_M(i, j)` per il calcolo
memoizzato di:

```math
M(1,n).
```

### Punto (b)

Calcolare il numero esatto $T(n)$ di moltiplicazioni tra interi eseguite per il
calcolo di:

```math
M(1,n).
```

---

## Soluzione

### Punto (a)

Per il punto (a), usiamo una tabella `M[1...n, 1...n]`, dove `M[i, j]`
rappresenta il valore della ricorrenza $M(i,j)$.

Osserviamo che la dimensione del sottoproblema può essere letta come:

```math
j-i+1.
```

Infatti:

- se $i=j$, allora $j-i+1=1$ e vale il primo caso base;
- se $j=i+1$, allora $j-i+1=2$ e vale il secondo caso base;
- se $j>i+1$, allora il sottoproblema ha dimensione almeno `3` e si applica il
  caso ricorsivo.

Inizializziamo quindi:

- `M[i, i] = 1`;
- `M[i, i + 1] = 2`;
- tutte le altre celle utili a `0`, usato come valore sentinella per indicare
  che il sottoproblema non è ancora stato calcolato.

La scelta di `0` come valore sentinella è sicura perché tutti i valori della
ricorrenza sono positivi.

## Pseudocodice

```text
INIT_M(n)
    if n == 1
        return 1

    if n == 2
        return 2

    allocate M[1...n, 1...n]

    // inizializzazione dei casi base
    for i = 1 to n - 1
        M[i, i] = 1
        M[i, i + 1] = 2

    M[n, n] = 1

    // inizializzazione dei casi ricorsivi come "non ancora calcolati"
    for i = 1 to n - 2
        for j = i + 2 to n
            M[i, j] = 0

    return REC_M(1, n)


REC_M(i, j)
    if M[i, j] == 0
        M[i, j] =
            REC_M(i + 1, j - 1) *
            REC_M(i + 1, j) *
            REC_M(i, j - 1)

    return M[i, j]
```

La procedura `INIT_M(n)` prepara la tabella e poi avvia il calcolo di `M(1, n)`.
La procedura `REC_M(i, j)` calcola un valore solo se non è già presente nella
tabella, ottenendo così una versione memoizzata della ricorrenza.

---

## Punto (b): numero esatto di moltiplicazioni

Le moltiplicazioni vengono eseguite solo quando viene calcolato per la prima
volta un sottoproblema ricorsivo, cioè un valore della forma:

```math
M(i,j)
=
M(i+1,j-1)\cdot M(i+1,j)\cdot M(i,j-1).
```

Per calcolare il prodotto di tre termini sono necessarie esattamente `2`
moltiplicazioni.

Dobbiamo quindi contare quante coppie $(i,j)$ corrispondono al caso ricorsivo:

```math
j>i+1.
```

Queste coppie sono esattamente quelle con:

```math
i=1,\dots,n-2
\qquad\text{e}\qquad
j=i+2,\dots,n.
```

Quindi il numero totale di moltiplicazioni è:

```math
2\cdot
\left(
\sum_{i=1}^{n-2}\sum_{j=i+2}^{n}1
\right).
```

Per un fissato valore di $i$, la somma interna contiene:

```math
n-i-1
```

termini. Dunque:

```math
2\cdot
\left(
\sum_{i=1}^{n-2}\sum_{j=i+2}^{n}1
\right)
=
2\cdot
\left(
\sum_{i=1}^{n-2}(n-i-1)
\right).
```

Ponendo:

```math
k=n-i-1,
```

la somma diventa:

```math
\sum_{k=1}^{n-2}k.
```

Quindi:

```math
T(n)
=
2\cdot\sum_{k=1}^{n-2}k
=
2\cdot\frac{(n-2)(n-1)}{2}
=
(n-2)(n-1).
```

Il numero esatto di moltiplicazioni è quindi:

```math
\boxed{T(n)=(n-2)(n-1)}.
```

Per $n=1$ e $n=2$ non viene eseguita alcuna moltiplicazione, e la formula dà
correttamente valore `0`.
