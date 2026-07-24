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

Utilizziamo una tabella `memo[1...n, 1...n]`, dove `memo[i, j]` memorizza il
valore di $M(i,j)$.

I casi base della ricorrenza sono:

- $M(i,i)=1$;
- $M(i,i+1)=2$.

Tutti gli altri valori vengono inizializzati a `0`, che usiamo come valore
sentinella per indicare che la cella non è ancora stata calcolata.

La scelta di `0` come valore sentinella è sicura perché tutti i valori della
ricorrenza sono positivi.

---

## Pseudocodice

```text
INIT_M(n)
    allocate memo[1...n, 1...n]

    for i = 1 to n
        for j = 1 to n
            memo[i, j] = 0

    for i = 1 to n
        memo[i, i] = 1

    for i = 1 to n - 1
        memo[i, i + 1] = 2

    return REC_M(1, n)


REC_M(i, j)
    if memo[i, j] == 0
        memo[i, j] =
            REC_M(i + 1, j - 1) *
            REC_M(i + 1, j) *
            REC_M(i, j - 1)

    return memo[i, j]
```

La procedura `INIT_M(n)` inizializza la tabella e poi avvia il calcolo
memoizzato di $M(1,n)$.

La procedura `REC_M(i, j)` controlla se il valore è già presente nella tabella.
Se non lo è, lo calcola usando la definizione ricorsiva e lo salva. In questo
modo ogni sottoproblema viene calcolato al massimo una volta.

---

## Correttezza

Dimostriamo che `REC_M(i, j)` restituisce correttamente il valore $M(i,j)$ per
ogni coppia $(i,j)$ con $1\le i\le j\le n$.

### Casi base

Durante l'inizializzazione, per ogni indice valido $i$ viene assegnato:

```math
memo[i,i]=1.
```

Quindi, quando $i=j$, `REC_M(i, j)` restituisce correttamente:

```math
M(i,i)=1.
```

Inoltre, per ogni indice valido $i$ con $1\le i<n$, viene assegnato:

```math
memo[i,i+1]=2.
```

Quindi, quando $j=i+1$, `REC_M(i, j)` restituisce correttamente:

```math
M(i,i+1)=2.
```

### Caso ricorsivo

Se $j>i+1$, il valore `memo[i, j]` è inizialmente `0`.

La procedura assegna:

```math
memo[i,j]
=
REC\_M(i+1,j-1)\cdot
REC\_M(i+1,j)\cdot
REC\_M(i,j-1).
```

Per ipotesi induttiva, le tre chiamate ricorsive restituiscono correttamente i
valori:

```math
M(i+1,j-1),\quad M(i+1,j),\quad M(i,j-1).
```

Quindi il valore assegnato a `memo[i, j]` è esattamente:

```math
M(i+1,j-1)\cdot M(i+1,j)\cdot M(i,j-1),
```

cioè il valore definito dalla ricorrenza per $M(i,j)$.

Poiché ogni valore calcolato viene salvato nella tabella, eventuali chiamate
successive allo stesso sottoproblema restituiscono lo stesso valore senza
ricalcolarlo.

Pertanto `INIT_M(n)` restituisce correttamente $M(1,n)$.

---

## Punto (b): numero esatto di moltiplicazioni

Le moltiplicazioni vengono eseguite solo nei casi ricorsivi, cioè quando:

```math
j>i+1.
```

Ogni volta che viene calcolato per la prima volta un valore ricorsivo:

```math
M(i,j)
=
M(i+1,j-1)\cdot M(i+1,j)\cdot M(i,j-1),
```

vengono eseguite esattamente `2` moltiplicazioni tra interi.

Dobbiamo quindi contare quante coppie $(i,j)$ soddisfano:

```math
1\le i\le j\le n
\qquad\text{e}\qquad
j>i+1.
```

Queste sono esattamente le coppie con:

```math
i=1,\dots,n-2
\qquad\text{e}\qquad
j=i+2,\dots,n.
```

Il numero di tali coppie è:

```math
\sum_{i=1}^{n-2}\sum_{j=i+2}^{n}1.
```

Per un fissato $i$, il numero di valori possibili per $j$ è:

```math
n-i-1.
```

Quindi:

```math
\sum_{i=1}^{n-2}\sum_{j=i+2}^{n}1
=
\sum_{i=1}^{n-2}(n-i-1).
```

Ponendo $k=n-i-1$, otteniamo la somma:

```math
\sum_{k=1}^{n-2}k
=
\frac{(n-2)(n-1)}{2}.
```

Ogni sottoproblema ricorsivo richiede `2` moltiplicazioni. Quindi:

```math
T(n)
=
2\cdot \frac{(n-2)(n-1)}{2}
=
(n-2)(n-1).
```

Pertanto, il numero esatto di moltiplicazioni è:

```math
\boxed{T(n)=(n-2)(n-1)}.
```

La formula vale anche per $n=1$ e $n=2$, dove non viene eseguita alcuna
moltiplicazione.
