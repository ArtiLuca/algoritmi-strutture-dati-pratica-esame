# Esercizio 1 — Missing(A,n)

Sia dato un array $A[1..n]$ ordinato in modo crescente, contenente $n$ interi distinti scelti dall'insieme $\{1, 2, \dots, n+1\}$.
Esattamente un numero dell'insieme non compare in $A$.

Realizzare un algoritmo divide et impera `Missing(A, n)` che restituisca il numero mancante in tempo $\mathcal{O}(\log n)$.
Fornire pseudocodice, dimostrazione di correttezza e complessità.

---

### i. Idea e Logica

Assumendo che l’array $A[1\dots n]$ contenga interi distinti sempre crescenti, stiamo cercando l’elemento $k \in \{1, 2, \dots, n+1\}$ tale che $k \notin A$. Essendo che gli elementi partono idealmente da $1$ e crescono di $+1$, finché non incontriamo l'elemento mancante avremo un allineamento perfetto tra gli indici e i valori, ovvero $A[i] = i$.

Non appena manca un elemento, tutti i valori successivi "scalano" di una posizione rispetto al loro indice ideale, per cui avremo $A[i] > i$. Questo ci fornisce un predicato formidabile per una ricerca binaria:
- Se $A[q] == q$, l'elemento mancante si trova sicuramente alla destra di $q$.
- Se $A[q] > q$, l'elemento mancante è proprio $q$ oppure si trova alla sinistra di $q$.

Operiamo quindi in stile *divide-et-impera* usando una funzione wrapper `Missing(A, n)` e una procedura ricorsiva `MissingRec(A, p, r)`.

---

### ii. Pseudocodice

```text
// funzione "wrapper"
Missing(A, n)
    // Se l'array e' vuoto, l'insieme era {1}, quindi manca l'1
    if n == 0
        return 1
    else
        return MissingRec(A, 1, n)

// procedura ricorsiva
MissingRec(A, p, r)

    // caso base: la ricerca e' terminata
    if p > r
        return p

    q = floor((p + r) / 2)

    // se l'indice e' stabile, il buco e' nella meta' destra
    if A[q] == q
        return MissingRec(A, q + 1, r)

    // se l'indice non e' stabile, il buco e' a q oppure nella meta' sinistra
    else
        return MissingRec(A, p, q - 1)						    
```

---

### iii. Correttezza

La correttezza segue per induzione sulla lunghezza dell’intervallo $\ell = r - p + 1$, assumendo come ipotesi induttiva che la procedura `MissingRec(A, p, r)` funzioni correttamente per intervalli di lunghezza strettamente minore di $\ell$.

- **Caso base ($p > r \implies \ell = 0$):**
  L'intervallo è vuoto. Questo significa che i puntatori si sono appena incrociati proprio nel punto esatto in cui avviene il "salto" tra gli elementi allineati ($A[i] = i$) e quelli disallineati ($A[i] > i$). L'indice `p` punta esattamente all'elemento mancante. L'algoritmo restituisce correttamente `p`.

- **Passo induttivo ($p \le r \implies \ell \ge 1$):**
  Si divide l’array a metà calcolando l'indice centrale $q$.
  1. Se $A[q] == q$, sappiamo con certezza che tutti gli elementi nell'intervallo $A[1\dots q]$ sono contigui e presenti (nessun elemento mancante fino a $q$). Il "buco" deve trovarsi necessariamente alla destra di $q$. È quindi corretto scartare l'intera metà sinistra (incluso $q$) e chiamare `MissingRec(A, q + 1, r)`.
  2. Se $A[q] > q$, significa che l'elemento mancante si trova prima di $q$, oppure è $q$ stesso. Il "buco" non può trovarsi alla destra di $q$. È quindi corretto scartare la metà destra e chiamare `MissingRec(A, p, q - 1)`.

In entrambe le chiamate ricorsive, si opera su sottoarray di lunghezza $\ell' < \ell$. Per ipotesi induttiva, queste chiamate restituiscono l'indice corretto. L’algoritmo è dunque globalmente corretto.

---

### iv. Complessità

L'algoritmo esegue una singola chiamata ricorsiva su un array di dimensione dimezzata, eseguendo un numero costante $\Theta(1)$ di operazioni (calcolo indice e controllo booleano) prima della chiamata. L'equazione di ricorrenza è:

$$
T(n) = T(n/2) + \Theta(1)
$$

Applicando il **Master Theorem** con $a = 1$, $b = 2$ e $f(n) = \Theta(1)$:
L'esponente critico è $n^{\log_b a} = n^{\log_2 1} = n^0 = 1 = \Theta(1)$.
Poiché $f(n) = \Theta(n^{\log_b a})$, ci troviamo nel **CASO 2** del Master Theorem.
Moltiplicando per un fattore logaritmico, si ottiene la complessità finale:

$$
T(n) = \Theta(\log n)
$$
