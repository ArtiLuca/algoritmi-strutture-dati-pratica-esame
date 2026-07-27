# Esercizio 1 — Indice stabile

[← Torna all'appello](README.md)

## Testo

**Esercizio 1 (10 punti)**

Dato un array $A[1 \dots n]$ di interi, un indice $i$ si dice *stabile* se:

$$ A[i] = i $$

Realizzare una procedura `stab(A, n)` che, dato in input un array $A[1 \dots n]$ di
interi *distinti*, ordinato in modo crescente, ritorna un indice stabile, se
esiste, e ritorna $0$ altrimenti.

Dimostrarne la correttezza e valutarne la complessità.

---

## Soluzione

Poiché l'array è ordinato in modo crescente e contiene interi distinti, possiamo
usare una ricerca binaria modificata.

L'obiettivo è trovare un indice $i$ tale che:

$$ A[i] = i $$

A ogni passo consideriamo l'indice centrale $q$.

- Se $A[q] = q$, abbiamo trovato un indice stabile.
- Se $A[q] > q$, allora possiamo scartare la metà destra.
- Se $A[q] < q$, allora possiamo scartare la metà sinistra.

Questo funziona perché l'array è crescente e contiene valori distinti.

---

## Pseudocodice

```text
stab(A, n)
    if n < 1
        return 0

    return stabRec(A, 1, n)


stabRec(A, p, r)
    if p > r
        return 0

    q = floor((p + r) / 2)

    if A[q] == q
        return q

    else if A[q] > q
        return stabRec(A, p, q - 1)

    else
        return stabRec(A, q + 1, r)
```

---

## Correttezza

Dimostriamo che `stabRec(A, p, r)` restituisce un indice stabile contenuto in
$A[p \dots r]$, se esiste, e restituisce $0$ altrimenti.

### Caso base

Se $p > r$, l'intervallo è vuoto. Quindi non può contenere alcun indice stabile
e l'algoritmo restituisce correttamente $0$.

### Passo ricorsivo

Sia:

$$ q = \lfloor (p + r) / 2 \rfloor $$

Se $A[q] = q$, allora $q$ è un indice stabile e l'algoritmo lo restituisce
correttamente.

Supponiamo ora che $A[q] > q$.

Poiché l'array è ordinato in modo crescente e contiene interi distinti, per ogni
indice $k > q$ vale:

$$ A[k] \ge A[q] + (k - q) $$

Dato che $A[q] > q$, otteniamo:

$$ A[k] > q + (k - q) = k $$

Quindi, per ogni $k > q$, vale $A[k] > k$. Nessun indice nella metà destra può
essere stabile. È quindi corretto proseguire solo nell'intervallo $A[p \dots q - 1]$.

Supponiamo invece che $A[q] < q$.

Per ogni indice $k < q$, sempre usando il fatto che l'array è crescente e con
elementi distinti, vale:

$$ A[k] \le A[q] - (q - k) $$

Dato che $A[q] < q$, otteniamo:

$$ A[k] < q - (q - k) = k $$

Quindi, per ogni $k < q$, vale $A[k] < k$. Nessun indice nella metà sinistra può
essere stabile. È quindi corretto proseguire solo nell'intervallo $A[q + 1 \dots r]$.

In entrambi i casi, l'algoritmo scarta solo una parte dell'array che non può
contenere indici stabili. La chiamata ricorsiva avviene su un intervallo più
piccolo, quindi per induzione l'algoritmo è corretto.

Poiché `stab(A, n)` chiama `stabRec(A, 1, n)`, la procedura restituisce un indice
stabile dell'intero array, se esiste, e $0$ altrimenti.

---

## Complessità

A ogni passo l'algoritmo effettua un numero costante di operazioni e continua su
una sola metà dell'intervallo.

La ricorrenza è:

$$ T(n) = T(n/2) + \Theta(1) $$

Per il Master Theorem:

$$ T(n) = \Theta(\log n) $$

La complessità temporale è quindi:

$$ \Theta(\log n) $$

La complessità spaziale è:

$$ O(\log n) $$

a causa dello stack di chiamate ricorsive.

Una versione iterativa avrebbe invece spazio:

$$ O(1) $$
