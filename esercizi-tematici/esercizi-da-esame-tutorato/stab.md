# Esercizio 1 — Indice stabile

Dato un array $A[1 \dots n]$ di interi, un indice $i$ si dice stabile se $A[i] = i$.
Realizzare una procedura `stab(A, n)` che, dato in input un array $A[1 \dots n]$ di interi distinti, ordinato in modo crescente, ritorna un indice stabile, se esiste, e ritorna $0$ altrimenti.
Dimostrarne la correttezza e valutarne la complessità.

---

### i. Idea e Pseudocodice

Essendo l'array ordinato e composto da elementi distinti, possiamo sfruttare un approccio *divide-et-impera* simile alla ricerca binaria.
Uso una funzione `stab(A, n)` che agisce da wrapper per la procedura ricorsiva `stabRec(A, p, r)` che verifica se esiste un indice stabile nell’intervallo $A[p\dots r]$.

```text
// funzione "wrapper"
stab(A, n)
    return stabRec(A, 1, n)

// procedura ricorsiva
stabRec(A, p, r)

    // caso base: intervallo vuoto, indice stabile non trovato
    if p > r
        return 0

    // altrimenti prendo l'indice centrale
    q = floor((p + r) / 2)

    // verifico se e' un indice stabile
    if A[q] == q
        return q

    // se il valore supera l'indice, scarto la meta' destra
    else if A[q] > q
        return stabRec(A, p, q - 1)

    // se il valore e' minore dell'indice, scarto la meta' sinistra
    else // A[q] < q
        return stabRec(A, q + 1, r)
```

---

### ii. Correttezza

Per dimostrare la correttezza, procediamo per induzione sulla lunghezza dell’intervallo $\ell = r - p + 1$. Il predicato da soddisfare per un indice $q$ è $P(q) \iff A[q] == q$.

**Nota fondamentale:** Poiché $A$ contiene interi distinti e ordinati in senso crescente, l'array cresce *almeno* tanto velocemente quanto gli indici. Ovvero, per ogni $k > q$, vale che $A[k] - A[q] \ge k - q$.

- **Caso base ($p > r \implies \ell = 0$):**
  L'intervallo è vuoto. La ricerca è terminata senza trovare l'indice stabile ed è corretto restituire $0$.

- **Passo induttivo ($p \le r \implies \ell \ge 1$):**
  Calcoliamo l’indice centrale $q$. Se vale $P(q)$, allora $A[q] = q$ ed è corretto restituire $q$.
  Altrimenti, si hanno due sottocasi:
  1. Se $A[q] > q$, allora per ogni $k > q$ avremo che $A[k] \ge A[q] + (k - q) > q + k - q = k$. Dunque, $\forall k > q$ vale $A[k] > k$, per cui non esisterà alcun indice stabile a destra di $q$. È quindi corretto scartare l'intera metà destra e chiamare `stabRec(A, p, q - 1)`.
  2. Se $A[q] < q$, in modo speculare, per ogni $k < q$ avremo $A[k] \le A[q] - (q - k) < q - q + k = k$. Dunque, $\forall k < q$ vale $A[k] < k$, per cui non esisterà alcun indice stabile a sinistra di $q$. È corretto scartare la metà sinistra e chiamare `stabRec(A, q + 1, r)`.

In entrambi i casi ci riduciamo a chiamate ricorsive su intervalli di lunghezza $\ell' < \ell$. Per ipotesi induttiva, queste chiamate restituiscono il risultato corretto. L'algoritmo è dunque corretto.

---

### iii. Complessità

L'algoritmo esegue una singola chiamata ricorsiva su un array di dimensione dimezzata, ed esegue un numero costante $\Theta(1)$ di operazioni (calcolo indice e confronti) per ogni attivazione. L'equazione di ricorrenza è:

$$
T(n) = T\left(\frac{n}{2}\right) + \Theta(1)
$$

Possiamo risolverla con il **Master Theorem**, avendo parametri $a = 1, b = 2$ e $f(n) = \Theta(1)$.
Calcoliamo lo spartiacque asintotico:
$$n^{\log_b a} = n^{\log_2 1} = n^0 = 1 = \Theta(1)$$

Poiché $f(n) = \Theta(n^{\log_b a})$, ricadiamo esattamente nel **CASO 2** del Master Theorem. Moltiplicando per $\log n$, la complessità temporale risulta essere:
$$
T(n) = \Theta(n^{\log_b a} \cdot \log n) = \Theta(1 \cdot \log n) = \Theta(\log n)
$$
*(La complessità spaziale ammonta a $\mathcal{O}(\log n)$ per lo stack delle chiamate ricorsive, che può essere abbattuta a $\mathcal{O}(1)$ implementando una variante iterativa).*
