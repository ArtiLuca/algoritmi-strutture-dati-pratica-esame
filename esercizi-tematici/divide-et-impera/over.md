# Esercizio 2 - Elemento strettamente maggiore (Divide et Impera)

Scrivere una procedura di tipo divide et impera `over` che, dato un array di interi distinti $A[1\dots n]$ ordinato in modo crescente e un intero $x$, restituisce l'indice del più piccolo elemento in $A$ strettamente maggiore di $x$. Se nessun elemento di $A$ soddisfa la condizione, si restituisca $n + 1$. Valutare la complessità dell'algoritmo.

---

### Idea e Ragionamento

Per questo esercizio è importante tenere a mente il fatto che l’array $A[1\dots n]$ sia composto da interi distinti (senza ripetizioni) e ordinato in senso crescente.

Questo significa che possiamo operare in stile Divide et Impera (ricerca binaria) in base al confronto con il valore $x$ dato in input. Ovvero, se abbiamo un sottoarray $A[p\dots r]$, lo suddividiamo in due parti usando:

$$ q = \lfloor \frac{p+r}{2} \rfloor $$

Facendo il confronto $A[q] \le x$, si presentano due casi:

1. Se $A[q] \le x$, allora possiamo scartare la metà sinistra, essendo che ogni elemento che appartiene al sottoarray $A[p\dots q]$ sarà anch'esso minore o uguale a $x$. Limitiamo quindi lo spazio di ricerca al sottoarray $A[q+1\dots r]$.
2. Se invece $A[q] > x$, allora abbiamo trovato un possibile candidato. Poiché potrebbe essercene uno più piccolo alla sua sinistra, scartiamo la metà destra $A[q+1\dots r]$ e limitiamo lo spazio di ricerca al sottoarray $A[p\dots q-1]$. (L'indice $p$ che viene trasportato nelle chiamate successive farà da "memoria" per questo candidato).

Come caso base usiamo la condizione $p > r$ e restituiamo direttamente l’indice $p$. Esso rappresenterà l'indice del primo elemento di $A$ strettamente maggiore di $x$.

Nel caso tale elemento non esista, l’indice $p$ slitterà naturalmente fino a superare il limite dell'array, equivalendo a $n+1$ e restituendo correttamente questo valore come richiesto dal testo.

---

### Pseudocodice

```text
// restituisce indice di elemento piu piccolo di A strettamente maggiore di x
// altrimenti, restituisce n+1
Over(A, x)
    return OverRec(A, 1, n, x)

OverRec(A, p, r, x)
    if p > r
        return p
    else
        q = floor((p+r)/2)

        if A[q] <= x
            return OverRec(A, q+1, r, x)
        else
            return OverRec(A, p, q-1, x)
```

---

### Complessità

La complessità è data dalla seguente ricorrenza:

$$ T(n) = T\left(\frac{n}{2}\right) + \Theta(1) $$

Grazie al Master Theorem, troviamo che il lavoro costante fatto per l'operazione di confronto, pari a $\Theta(1)$, cresce in modo asintoticamente equivalente alla "watershed function":

$$ n^{\log_b a} = n^{\log_2 1} = n^0 = 1 $$

Poiché $f(n) = \Theta(n^{\log_b a})$, ci troviamo nel **Caso 2** del Master Theorem. Possiamo quindi concludere che la complessità temporale è:

$$ T(n) = \Theta(n^{\log_b a} \cdot \log n) = \Theta(n^0 \cdot \log n) = \Theta(\log n) $$

La complessità spaziale sarà $\mathcal{O}(\log n)$ dovuta allo stack delle chiamate ricorsive (oppure $\Theta(1)$ se l'algoritmo fosse convertito in forma puramente iterativa).
