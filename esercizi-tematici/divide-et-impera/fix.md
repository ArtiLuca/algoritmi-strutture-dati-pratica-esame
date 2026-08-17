# Esercizio 4 - Punto Fisso in Array (Divide et Impera)

Sia $A[1\dots n]$ un array di interi distinti ordinato in senso crescente. Dimostrare che, dato un qualunque indice $i$, se $A[i] > i$ allora $A[j] > j$ per ogni $j > i$ e analogamente se $A[i] < i$ allora $A[j] < j$ per ogni $j < i$.

Utilizzare l'osservazione per realizzare una funzione `Fix(A)` che, dato l'array di interi $A[1\dots n]$ ordinato senza ripetizioni, restituisce un indice $i$ tale che $A[i] = i$, se esiste, e **0** altrimenti. Valutarne la complessità.

---

### i. Dimostrazione

Per la prima parte, possiamo sfruttare il fatto che l'array $A[1\dots n]$ sia composto da interi distinti (quindi senza ripetizioni) e ordinato in senso crescente per dimostrare che $\forall i \in [1\dots n]$ valgono le seguenti proprietà:

- se $A[i] > i \implies A[j] > j$ per ogni $j > i$
- se $A[i] < i \implies A[j] < j$ per ogni $j < i$

Se consideriamo due elementi generici $A[i]$ e $A[j]$, abbiamo che se $j > i$ allora l’elemento $A[j]$ si trova ad una distanza in avanti rispetto ad $A[i]$ equivalente a $(j-i)$. In modo speculare, se $j < i$ allora $A[j]$ si trova ad una distanza all’indietro rispetto ad $A[i]$ equivalente a $(i-j)$. Inoltre, essendo che non ci sono ripetizioni e i numeri sono interi, avremo che $|A[i] - A[j]| \ge |i - j|$.

**Primo caso:**
Se $A[i] > i$, allora abbiamo che per ogni $j > i$ vale la disuguaglianza:

$$ A[j] \ge A[i] + (j - i) $$

Sostituendo l'ipotesi $A[i] > i$ nella disequazione, otteniamo strettamente:

$$ A[j] > i + (j - i) \implies A[j] > j $$

**Secondo caso:**
In modo speculare, se $A[i] < i$, allora abbiamo che per ogni $j < i$ vale la disuguaglianza:

$$ A[j] \le A[i] - (i - j) $$

Sostituendo l'ipotesi $A[i] < i$ nella disequazione, otteniamo strettamente:

$$ A[j] < i - (i - j) \implies A[j] < j $$

---

### ii. Algoritmo

Possiamo utilizzare quanto appena dimostrato per implementare un algoritmo che opera in stile Divide et Impera (ricerca binaria), dimezzando lo spazio di ricerca nell’array per trovare il primo indice $q$ tale che $A[q] == q$, scartando le metà in cui siamo sicuri che tale indice non può trovarsi.

```text
// funzione principale, restituisce l'indice i tale che A[i] == i se esiste
// altrimenti, restituisce 0
Fix(A)
    n = A.length
    return FixRec(A, 1, n)

FixRec(A, p, r)
    // caso base: l'indice non esiste		
    if p > r
        return 0
    else
        q = floor((p+r)/2)

        // Match trovato
        if A[q] == q
            return q

        // Se A[q] > q, tutti i successivi saranno > j. Scarto la metà destra.
        else if A[q] > q
            return FixRec(A, p, q-1)

        // Se A[q] < q, tutti i precedenti saranno < j. Scarto la metà sinistra.
        else
            return FixRec(A, q+1, r)
```

---

### iii. Complessità

La complessità è data dalla ricorrenza tipica della ricerca binaria:

$$ T(n) = T\left(\frac{n}{2}\right) + \Theta(1) $$

Grazie al Master Theorem, sappiamo che la funzione di intermezzo è $n^{\log_2 1} = n^0 = 1$. Essendo il costo locale $\Theta(1)$ asintoticamente equivalente, ci troviamo nel Caso 2 del Master Theorem. La complessità temporale complessiva risulta quindi essere:

$$ T(n) = \Theta(\log n) $$

La complessità spaziale è $\mathcal{O}(\log n)$ dovuta alle chiamate ricorsive sullo stack.
