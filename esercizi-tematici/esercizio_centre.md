# Centro di array semi-ordinato

Diciamo che un array senza ripetizioni $A[1 \dots n]$ è semi-ordinato se esiste un indice $k$, con:
$$ 1 \leq k < n $$
tale che:
$$ A[k+1 \dots n] \quad \text{e} \quad A[1 \dots k] $$
siano ordinati, ovvero i sottoarray $A[k+1 \dots n]$ e $A[1 \dots k]$ sono ordinati e:
$$ A[n] < A[1] $$

In questo caso l'indice $k$ viene detto il **centro** dell'array.
Ad esempio l'array che segue è semi-ordinato con centro $k=4$:

```text
 1  2   3   4   5  6  7
[4, 9, 12, 18, -1, 1, 2]
```

Scrivere una funzione `centre(A)` che, dato un array $A$ semi-ordinato, ne restituisce il centro. Giustificare la correttezza dell'algoritmo e valutarne la complessità.

---

### Soluzione

Per la definizione di array semi-ordinato data dal testo, abbiamo un array $A[1 \dots k, k+1 \dots n]$ tale che entrambi i sottoarray $A[1 \dots k]$ e $A[k+1 \dots n]$ sono ordinati in senso crescente e senza ripetizioni, ovvero tutti gli elementi sono distinti.

Inoltre, dal testo sappiamo che $A[n] < A[1]$. Segue che per ogni coppia di indici $i,j$ con $i \in [1 \dots k]$ e $j \in [k+1 \dots n]$ vale $A[j] < A[i]$. Quindi, in pratica, stiamo cercando la prima "discesa", ovvero il primo indice $i \ge 1$ tale che $A[i] > A[i+1]$. Questo perché, se tutti gli elementi a destra del centro sono strettamente minori di $A[1]$, il primo elemento che ha un elemento immediatamente successivo minore di sé stesso rappresenta il nostro centro.

Possiamo dunque usare una tecnica *Divide et Impera* operando sul sottoarray $A[p \dots r]$.

Se il sottoarray è composto da un solo elemento, ovvero $p=r$, allora il primo indice candidato come centro sarà l’indice $p$ e quindi si restituisce questo.

Altrimenti si calcola il punto medio $q$ e si va a casi:
- Se $A[q] < A[1]$ allora siamo entrati nel sottoarray destro, quindi si ricorre a sinistra su $A[p \dots q-1]$.
- Altrimenti ($A[q] \ge A[1]$), si controlla se $A[q] > A[q+1]$. Se ciò accade, allora si restituisce $q$ che è il centro. Se il controllo fallisce, allora si ricorre a destra su $A[q+1 \dots r]$.

### Pseudocodice

```text
// Procedura principale
// Restituisce il centro di A se esiste
centre(A)
    n = A.length
    // Controllo per caso base
    if n <= 0
        return 0
    else
        return recCentre(A, 1, n)

// Procedura ricorsiva
recCentre(A, p, r)            
    // Caso base
    if p == r
        // Restituisco l'unico indice candidato per il centro
        return p
    else
        // Midpoint
        q = floor((p+r)/2)

        // Se l'elemento è minore del primo, sono nella seconda metà.
        // Il centro si trova per forza a sinistra.
        if A[q] < A[1]        
            return recCentre(A, p, q-1)

        // Altrimenti, verifico l'indice attuale
        else
            // Se abbiamo una discesa allora abbiamo trovato il centro
            if A[q] > A[q+1]
                return q        
            else
                // Altrimenti, si ricorre a destra
                return recCentre(A, q+1, r)
```

### Correttezza

Per la definizione di array semi-ordinato, possiamo vedere l’array $A[1 \dots n]$ come due sottoarray $A[1 \dots k]$ e $A[k+1 \dots n]$, entrambi ordinati in senso crescente e senza ripetizioni.

Inoltre, come detto nel testo dell’esercizio vale $A[n] < A[1]$. Dal fatto che $A[n] < A[1]$ segue quindi che $A[n]$ è il massimo del sottoarray $A[k+1 \dots n]$ e $A[1]$ è il minimo del sottoarray $A[1 \dots k]$.

Segue che ogni elemento del secondo sottoarray è strettamente minore di ogni elemento del primo sottoarray. Ovvero, per un generico indice $i$ valgono:
- $i \le k \implies A[i] \ge A[1]$
- $i > k \implies A[i] < A[1]$

Quindi possiamo operare in stile *Divide et Impera* (Ricerca Binaria) sull’intervallo $[p,r]$ assumendo che il centro $k$ dell’array si trovi in questo intervallo.

Se abbiamo $p = r$ allora il sottoarray è composto da un solo elemento e quindi l'unico indice che potrebbe contenere il centro è l’indice $p$.
Se poi suddividiamo l’intervallo $[p,r]$ calcolando il midpoint $q$, allora abbiamo due casi:
1. Se $A[q] < A[1]$ allora $q$ appartiene al secondo sottoarray, ovvero abbiamo che $q > k$ e dunque il centro deve stare a sinistra di $q$, cioè il centro $k \in [p, q-1]$. Quindi si ricorre a sinistra.
2. Se invece $A[q] \ge A[1]$ allora $q$ appartiene al primo sottoarray e quindi $q \le k$. Si controlla se $q$ è il centro, cosa che accade se $A[q] > A[q+1]$.
   - Se questo accade, allora c’è una "discesa" tra $q$ e $q+1$, e siccome l’unica discesa dell’array avviene proprio tra $A[k]$ e $A[k+1]$, segue che $q=k$ e quindi abbiamo trovato il nostro centro.
   - Se invece $A[q] < A[q+1]$ allora $q$ non può essere il centro. Poiché $q \le k$, deve valere $q < k$ e quindi il centro sta a destra, ovvero $k \in [q+1, r]$ e quindi si ricorre a destra.

L’algoritmo è corretto in quanto scarta iterativamente o ricorsivamente le metà in cui non è possibile che si trovi il centro, facendo anche un controllo diretto per restituirlo nel caso lo si trovi "strada facendo". Alla fine, se si arriva a una foglia, restituisce l’indice $p$ correttamente.

### Complessità

La complessità si può analizzare con il Master Theorem, impostando la ricorrenza del problema:

$$ T(n) = T\left(\frac{n}{2}\right) + \Theta(1) $$

dove $\Theta(1)$ indica il lavoro costante fatto per i controlli e la divisione all'interno delle chiamate ricorsive (il calcolo di $q$ e i confronti).

Con il Master Theorem abbiamo $a=1, b=2$ e $f(n) = \Theta(1)$. Dato che $n^{\log_b a} = n^{\log_2 1} = n^0 = 1 = \Theta(1)$, il lavoro fatto per combinare le chiamate ricorsive e il termine $n^{\log_b a}$ crescono in modo asintoticamente equivalente. Si conclude quindi, tramite il Caso 2 del Master Theorem, che la complessità è:

$$ T(n) = \Theta(\log n) $$
