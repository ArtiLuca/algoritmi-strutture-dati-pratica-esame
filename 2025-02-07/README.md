# Appello 2025-02-07 — Algoritmi e Strutture Dati

[← Torna alla raccolta](../README.md)

## Stato delle soluzioni

| Problema | Argomento principale | Stato |
|---|---|---|
| Domanda A | Ricorrenza con Master Theorem | [Completata](domanda_a.md) |
| Domanda B | Hashing con doppio hash | [Completata](domanda_b.md) |
| Esercizio 1 | Heap e ordinamento in spazio costante | [Completata](esercizio_1.md) |
| Esercizio 2 | Selezione di attività compatibili | [Completata](esercizio_2.md) |

---

## Testo dell'appello

## Domande

### Domanda A

**Domanda A (5 punti)**

Si determini la soluzione asintotica della seguente equazione di ricorrenza:

```math
T(n)=3T(n/3)+n^2+1.
```

**[Vai alla soluzione](domanda_a.md)**

### Domanda B

**Domanda B (7 punti)**

Si consideri una tabella hash di dimensione $m=7$, e indirizzamento aperto con
doppio hash basato sulle funzioni:

```math
h_1(k)=k \bmod m
```

e

```math
h_2(k)=1+k \bmod (m-2).
```

Si descriva sinteticamente come avviene l'inserimento degli elementi e si
specifichi il risultato dell'inserzione della sequenza di chiavi:

```math
10,20,34,35,48.
```

Sarebbe appropriato lavorare con una tabella di dimensione $m=8$ e le stesse
funzioni hash?

**[Vai alla soluzione](domanda_b.md)**

---

## Esercizi

### Esercizio 1

**Esercizio 1 (10 punti)**

Siano dati due array `A[1..2n]` e `B[1..n]` organizzati a max-heap, entrambi
contenenti $n$ elementi (`heapsize=n`).

Realizzare una procedura `SortJoin(A, B, n)` che dati in input array `A` e `B`
con le proprietà sopra descritte, ritorna in `A` un array ordinato contenente
tutti i $2n$ elementi originariamente presenti in `A` e `B`.

L'array `B` può essere modificato durante l'esecuzione della procedura, se
necessario, ma l'algoritmo dovrà operare in *spazio costante*.

Dare lo pseudocodice della procedura, motivarne la correttezza e valutarne la
complessità. Se si utilizzano operazioni sui max-heap andranno definite
esplicitamente.

**[Vai alla soluzione](esercizio_1.md)**

### Esercizio 2

**Esercizio 2 (10 punti)**

Si consideri il problema di selezione di attività compatibili, con $n$ attività
$a_1,\ldots,a_n$ che ci vengono date attraverso due vettori **s** e **f** di
tempi di inizio e fine, e ordinate per tempo di *inizio*, cioè:

```math
0<s_1\le s_2\le\cdots\le s_n.
```

**(a)** Scrivere un algoritmo greedy iterativo che implementa la scelta greedy
di selezionare l'attività che inizia per ultima.

**(b)** Determinare l'insieme di attività restituito dall'algoritmo al punto
(a) quando eseguito sul seguente insieme di 6 attività, caratterizzate dai
seguenti vettori **s** e **f** di tempi di inizio e fine:

```math
\mathbf{s}=(1,2,3,5,7,10),
```

```math
\mathbf{f}=(3,9,10,7,11,12).
```

**(c)** Dimostrare la proprietà di scelta greedy, cioè che esiste soluzione
ottima che contiene l'attività che inizia per ultima.

**[Vai alla soluzione](esercizio_2.md)**
