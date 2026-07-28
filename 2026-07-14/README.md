# Algoritmi e Strutture Dati — Appello del 14 luglio 2026

Questa cartella contiene le mie soluzioni personali all'appello del  
**14 luglio 2026** del corso di Algoritmi e Strutture Dati.

## Fonte

Il testo dell'appello è disponibile nella pagina ufficiale del corso.
Le soluzioni presenti in questa cartella sono personali e non costituiscono
materiale ufficiale del corso.

## Stato delle soluzioni

| Problema | Argomento principale | Stato |
|---|---|---|
| Domanda A | Ricorrenze e classi O e Ω | [Da completare](domanda_a.md) |
| Domanda B | Ricorrenza per Longest Common Subsequence (LCS) | [Da completare](domanda_b.md) |
| Esercizio 1 | Ordinamento in loco (TriSort) | [Da completare](esercizio_1.md) |
| Esercizio 2 | Algoritmo greedy per il resto delle monete | [Da completare](esercizio_2.md) |

---

## Domanda A — Ricorrenze e classi O e Ω

**6 punti**

Data la ricorrenza:

$$ T(n) = \frac{3}{2}T(n-1) + 2 $$

mostrare che la soluzione è $O(2^n)$.

Vale anche $T(n) = \Omega(2^n)$? Motivare la risposta.

**[Vai alla soluzione](domanda_a.md)**

---

## Domanda B — Longest Common Subsequence (LCS)

**6 punti**

Scrivere la ricorrenza sulle lunghezze $\ell(i,j)$ per il problema della longest
common subsequence (LCS).

**[Vai alla soluzione](domanda_b.md)**

---

## Esercizio 1 — Ordinamento in loco (TriSort)

**10 punti**

Realizzare una procedura `TriSort(A)` che dato un array $A[1 \dots n]$ di $n$
elementi, con valori in $\{0, 1, 2\}$, lo ordina in modo crescente.

L'unica operazione ammessa per modificare l'array è:

$$ A[i] \leftrightarrow A[j] $$

il cui effetto è quello di scambiare gli elementi in posizione $i$ e $j$.

Dare lo pseudocodice e motivarne la correttezza. Valutare la complessità asintotica,
indicando anche il numero di confronti e di scambi nel caso peggiore.

**[Vai alla soluzione](esercizio_1.md)**

---

## Esercizio 2 — Algoritmo greedy per il resto delle monete

**9 punti**

Supponiamo di avere un numero illimitato di monete di ciascuno dei seguenti
valori: $\{50, 20, 1\}$. Dato un numero intero positivo $n$, l'obiettivo è selezionare il
più piccolo numero di monete tale che il loro valore totale sia $n$. Consideriamo
l'algoritmo greedy che consiste nel selezionare ripetutamente la moneta di
valore più grande possibile.

### Punto (a)

Fornire un valore di $n$ per cui l'algoritmo greedy non restituisce una
soluzione ottima.

### Punto (b)

Supponiamo ora che i valori delle monete siano $\{10, 5, 1\}$. In questo caso
l'algoritmo greedy restituisce sempre una soluzione ottima: dimostrare che ogni
insieme ottimo $M^\star$ di monete di valore totale $n$ contiene la scelta greedy.

**[Vai alla soluzione](esercizio_2.md)**
