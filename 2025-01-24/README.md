# Appello 2025-01-24 — Algoritmi e Strutture Dati

[← Torna alla raccolta](../README.md)

## Stato delle soluzioni

| Problema | Argomento principale | Stato |
|---|---|---|
| Domanda A | Max-heap, min-heap e ricerca del minimo | [Completata](domanda_a.md) |
| Domanda B | Selezione di attività compatibili | [Completata](domanda_b.md) |
| Esercizio 1 | Divide et impera su sequenza con stabilizzazione | [Completata](esercizio_1.md) |
| Esercizio 2 | Programmazione dinamica bottom-up e conteggio dei confronti | [Completata](esercizio_2.md) |

---

## Testo dell'appello

## Domande

### Domanda A

**Domanda A (7 punti)**

Dare la definizione di max-heap.

Dato un insieme $S$ di elementi, memorizzato in parte in un min-heap $A$ e in
parte in un max-heap $B$, entrambi non vuoti, dare un algoritmo `min(A, B)` per
trovare il minimo di $S$ nelle due situazioni seguenti:

**(a)** ogni elemento di $A$ è minore o uguale a ogni elemento di $B$;

**(b)** ogni elemento di $B$ è minore o uguale a ogni elemento di $A$.

In entrambi i casi scrivere lo pseudocodice e valutare la complessità.

**[Vai alla soluzione](domanda_a.md)**

### Domanda B

**Domanda B (7 punti)**

Si consideri il problema di selezione di attività compatibili:

**(a)** Definire il problema.

**(b)** Descrivere brevemente l'algoritmo ottimo `GREEDY-SEL` visto in classe.

**(c)** Fornire un esempio di algoritmo greedy *non* ottimo, motivandone la non
ottimalità.

**[Vai alla soluzione](domanda_b.md)**

---

## Esercizi

### Esercizio 1

**Esercizio 1 (10 punti)**

Sia dato un array $V[1 \dots n]$ i cui valori rappresentano la variazione giornaliera
del valore di un titolo azionario.

È noto che il titolo è stato prima in perdita, con valori sempre negativi, poi
ha iniziato a oscillare in giorni consecutivi tra valori positivi e negativi, e
infine si è stabilizzato su valori positivi. Dunque nella sequenza non ci
possono essere due giorni positivi seguiti da un negativo.

Realizzare un algoritmo *divide et impera* `Split(V)` che individua il giorno in
cui il titolo ha iniziato a essere stabile su valori positivi, ovvero il minimo
indice $i$ in $[1, n]$ tale che per ogni $j \ge i$ vale $V[j] > 0$.

Se il titolo non si stabilizza su valori positivi, ritornare $0$.

Ad esempio, se l'array è:

$$ V = [-1, -2, 2, -1, 6, 3] $$

l'indice da ritornare sarà $5$, mentre per:

$$ V = [-1, -2, 2, -1, 6, -3] $$

si ritornerà $0$.

Fornire lo pseudocodice di `Split(V)`, motivarne la correttezza e individuarne
la complessità. Si assuma che non ci siano valori nulli.

**[Vai alla soluzione](esercizio_1.md)**

### Esercizio 2

**Esercizio 2 (8 punti)**

Date due stringhe $X = \langle x_1, x_2, \dots, x_m \rangle$ e
$Y = \langle y_1, y_2, \dots, y_n \rangle$, si consideri la seguente quantità $\ell(i, j)$,
definita per ogni coppia di valori $i, j$ con $0 \le i \le m$ e $0 \le j \le n$:

$$
\ell(i, j) =
\begin{cases}
1 & \text{se } i = 0 \text{ oppure } j = 0 \\
3 \cdot \ell(i, j - 1) & \text{se } i, j > 0 \text{ e } x_i = y_j \\
2 \cdot \ell(i - 1, j - 1) - \ell(i - 1, j) & \text{se } i, j > 0 \text{ e } x_i \ne y_j
\end{cases}
$$

Si vuole calcolare la quantità:

$$ q = \max \{ \ell(i, j) : 0 \le i \le m, 0 \le j \le n \} $$

**(a)** Scrivere un algoritmo bottom-up per il calcolo di $q$.

**(b)** Determinare la complessità esatta dell'algoritmo, supponendo che le
uniche operazioni di costo unitario e non nullo siano i confronti tra caratteri.

**[Vai alla soluzione](esercizio_2.md)**
