# Divide et Impera e Ricorsione

[← Torna agli esercizi tematici](../README.md) · [Torna alla raccolta principale](../../README.md)

Questa cartella raccoglie esercizi dedicati a tecniche di ricorsione e divide et impera, con particolare attenzione a dimostrazioni induttive, progettazione di procedure ricorsive e analisi della complessità tramite ricorrenze.

Gli esercizi sono pensati per allenarsi su problemi simili a quelli d'esame: non solo scrivere pseudocodice, ma anche motivare la correttezza dell'algoritmo e valutarne il costo.

Ogni esercizio completato contiene una soluzione in stile esame, con idea dell'algoritmo, pseudocodice, dimostrazione di correttezza e analisi della complessità quando richieste.

---

## Stato delle soluzioni

| Esercizio | Stato |
|---|---|
| Esercizio 1 — Gap in un array | Da completare |
| Esercizio 2 — Primo elemento strettamente maggiore di `x` | Da completare |
| Esercizio 3 — Massimo con divide et impera | [Completato](massimo.md) |
| Esercizio 4 — Indice fisso in array ordinato | Da completare |
| Domanda 19 — Sottosequenza ricorsiva | Da completare |
| Esercizio 5 — Array alternante | Da completare |

---

## Testi degli Esercizi


### **Esercizio 1**

Dato un array di interi `A[1..n]`, chiamiamo *gap* un indice $i \in [1, n)$ tale che $A[i + 1] - A[i] > 1$.

- **i.** Mostrare per induzione su $n$ che un array `A[1..n]` tale che $A[n] - A[1] \ge n$ (quindi $n \ge 2$) contiene almeno un *gap*.
- **ii.** Fornire lo pseudocodice di una procedura ricorsiva *divide et impera* `gap` che dato un array `A[1..n]` tale che $A[n] - A[1] \ge n$ restituisce un *gap* in `A`.
- **iii.** Valutare la complessità della funzione, utilizzando il master theorem.

---

### **Esercizio 2**

Scrivere una procedura di tipo *divide et impera* `over` che dato un array di interi distinti `A[1..n]`, ordinato in modo crescente, e un intero $x$ restituisce l'indice del più piccolo elemento in `A` strettamente maggiore di $x$. Se nessun elemento di `A` soddisfa la condizione, si restituisca $n + 1$. Valutare la complessità dell'algoritmo.

---

### **Esercizio 3**

Realizzare una procedure di tipo *divide et impera* `Max(A, p, r)` per trovare il massimo nell'array `A[p..r]`. Si assuma che l'array non sia vuoto ($p \le r$). Scrivere lo pseudocodice e valutare la complessità con il master theorem.

---

### **Esercizio 4**

Sia `A[1..n]` un array di interi distinti ordinato in senso crescente. Dimostrare che dato un qualunque indice $i$, se $A[i] > i$ allora $A[j] > j$ per ogni $j > i$ e analogamente se $A[i] < i$ allora $A[j] < j$ per ogni $j < i$.
Utilizzare l'osservazione per realizzare una funzione `Fix(A)` che dato l'array di interi `A[1..n]` ordinato senza ripetizioni restituisce un indice $i$ tale che $A[i] = i$, se esiste, e 0 altrimenti. Valutarne la complessità.

---

### **Domanda 19**

Scrivere una funzione ricorsiva `subseq(X, Y, m, n)` che date due sequenze `X[1..m]` e `Y[1..n]`, di lunghezza $m$ e $n$ rispettivamente, verifica se `X` è una sottosequenza di `Y` e restituisce un valore booleano conseguente. Valutarne la complessità.

---

### **Esercizio 5**

Un array `A[1..n]` di numeri si dice *alternante* se non ha elementi contigui identici (ovvero per ogni $i \le n-1$ vale $A[i] \ne A[i+1]$) e inoltre per ogni $i \le n-2$, vale che $a_i < a_{i+1} > a_{i+2}$ oppure $a_i > a_{i+1} < a_{i+2}$. Ad esempio gli array `[1, 2, -1, 3, 2]` e `[5, 1, 2, -1, 3, 2]` sono alternanti, mentre non lo sono `[1, 2, 3]` e `[1, 1, 2]`. Scrivere una funzione ricorsiva `alt(A, n)` che dato un array `A[1..n]` di numeri verifica se è alternante. Valutarne la complessità.
