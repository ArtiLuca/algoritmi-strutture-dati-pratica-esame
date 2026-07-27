# Domanda A — Max-heap, min-heap e minimo

[← Torna all'appello](README.md)

## Testo

**Domanda A (7 punti)**

Dare la definizione di max-heap.

Dato un insieme `S` di elementi, memorizzato in parte in un min-heap `A` e in
parte in un max-heap `B`, entrambi non vuoti, dare un algoritmo `min(A, B)` per
trovare il minimo di `S` nelle due situazioni seguenti:

**(a)** ogni elemento di `A` è minore o uguale a ogni elemento di `B`;

**(b)** ogni elemento di `B` è minore o uguale a ogni elemento di `A`.

In entrambi i casi scrivere lo pseudocodice e valutare la complessità.

---

## Soluzione

## Definizione di max-heap

Un **max-heap** è un albero binario quasi completo, solitamente rappresentato
mediante un array `A[1..n]`, che soddisfa la proprietà di max-heap.

In particolare:

- la radice si trova in posizione `A[1]`;
- il padre del nodo in posizione `i > 1` si trova in posizione `floor(i/2)`;
- il figlio sinistro di `i`, se esiste, si trova in posizione `2i`;
- il figlio destro di `i`, se esiste, si trova in posizione `2i + 1`;
- per ogni nodo `i`, se i figli esistono, vale:

```text
A[i] >= A[2i]
A[i] >= A[2i + 1]
```

Quindi, in un max-heap, l'elemento massimo si trova sempre nella radice.

Un **min-heap** è definito in modo analogo, ma con le disuguaglianze invertite.
Quindi, in un min-heap, l'elemento minimo si trova sempre nella radice.

---

## Caso (a)

Nel caso (a), ogni elemento di `A` è minore o uguale a ogni elemento di `B`.

Quindi il minimo dell'intero insieme `S` deve trovarsi in `A`.

Poiché `A` è un min-heap, il minimo di `A` si trova nella radice.

Quindi:

```text
min(A, B)
    return A[1]
```

La complessità è:

```text
Theta(1)
```

---

## Caso (b)

Nel caso (b), ogni elemento di `B` è minore o uguale a ogni elemento di `A`.

Quindi il minimo dell'intero insieme `S` deve trovarsi in `B`.

Tuttavia `B` è un max-heap, quindi la radice contiene il massimo, non il minimo.

In un max-heap, un minimo deve trovarsi tra le foglie. Infatti, se un nodo non è
foglia, allora i suoi figli sono minori o uguali a lui, quindi il nodo non può
essere l'unico candidato minimo.

Le foglie di un heap di dimensione `n_b` si trovano nelle posizioni:

```text
floor(n_b / 2) + 1, ..., n_b
```

Dobbiamo quindi scorrere tutte le foglie di `B` e restituire la più piccola.

```text
min(A, B)
    n_b = B.heapsize

    firstLeaf = floor(n_b / 2) + 1
    minimum = B[firstLeaf]

    for j = firstLeaf + 1 to n_b
        if B[j] < minimum
            minimum = B[j]

    return minimum
```

Il numero di foglie è lineare nella dimensione di `B`, quindi la complessità è:

```text
Theta(n_b)
```

Se indichiamo con `n` la dimensione complessiva rilevante dell'input, possiamo
scrivere:

```text
Theta(n)
```
