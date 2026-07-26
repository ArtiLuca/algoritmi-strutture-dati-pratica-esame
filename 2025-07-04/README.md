# Appello 2025-07-04 — Algoritmi e Strutture Dati

[← Torna alla raccolta](../README.md)

## Stato delle soluzioni

| Problema | Argomento principale | Stato |
|---|---|---|
| Domanda A | Ricorrenza con metodo di sostituzione | [Completata](domanda_a.md) |
| Domanda B | Alberi binari di ricerca, inserimento e cancellazione | [Completata](domanda_b.md) |
| Esercizio 1 | Ricerca binaria di un indice stabile | [Completata](esercizio_1.md) |
| Esercizio 2 | Memoizzazione e complessità al caso migliore | [Completata](esercizio_2.md) |

---

## Testo dell'appello

## Domande

### Domanda A

**Domanda A (6 punti)**

Si dimostri che la ricorrenza che segue ha soluzione $T(n)=\Theta(n)$:

```math
T(n)=\frac{2}{3}T(n-1)+2n.
```

### Domanda B

**Domanda B (7 punti)**

Dare la definizione di albero binario di ricerca.

Specificare l'albero ottenuto inserendo, con la procedura vista a lezione, a
partire da un albero vuoto, i nodi aventi le seguenti chiavi:

```text
10, 5, 3, 15, 7, 12
```

Si supponga che dall'albero così ottenuto si cancelli il nodo con chiave `5` e
si indichi l'albero ottenuto.

Sia per gli inserimenti che per la cancellazione, motivare sinteticamente il
risultato ottenuto.

---

## Esercizi

### Esercizio 1

**Esercizio 1 (10 punti)**

Dato un array `A[1..n]` di interi, un indice `i` si dice *stabile* se
`A[i] = i`.

Realizzare una procedura `stab(A, n)` che, dato in input un array `A[1..n]` di
interi *distinti*, ordinato in modo crescente, ritorna un indice stabile, se
esiste, e ritorna `0` altrimenti.

Dimostrarne la correttezza e valutarne la complessità.

### Esercizio 2

**Esercizio 2 (9 punti)**

Data una stringa `X = x_1, x_2, ..., x_n`, si consideri la seguente quantità
`l(i, j)`, definita per `1 <= i <= j <= n`:

```text
l(i, j) =
    1                                    se i = j
    2                                    se i = j - 1
    2 + l(i + 1, j - 1)                  se i < j - 1 e x_i = x_j
    sum_{k=i}^{j-1}(l(i,k) + l(k+1,j))   se i < j - 1 e x_i != x_j
```

**(1)** Scrivere una coppia di algoritmi `INIT_L(X)` e `REC_L(i, j)` per il
calcolo memoizzato di `l(1, n)`.

**(2)** Si determini la complessità al caso migliore `T_best(n)` supponendo che
le uniche operazioni di costo unitario e non nullo siano i confronti tra
caratteri.
