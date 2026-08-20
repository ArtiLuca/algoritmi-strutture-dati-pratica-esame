# Esercizio 8 - Massimo in Array Bi-ordinato

Realizzare un algoritmo `top(A, n)` che dato in input un array $A$ bi-ordinato con elementi distinti ne determina il valore massimo. Ad esempio su $A = (1, 2, 3, 14, 13, 4)$ restituisce $14$. Valutarne la complessità.

---

### i. Idea e Ragionamento

Questo esercizio sfrutta i concetti di ordinamento per applicare la tecnica del *Divide et Impera*.
Sappiamo che $A[1\dots n]$ è bi-ordinato e composto da elementi distinti. Per definizione, esiste un indice $k$ tale che $A[1\dots k]$ è ordinato in senso crescente, mentre $A[k \dots n]$ è ordinato in senso decrescente. Vogliamo trovare il valore massimo, che corrisponde all'elemento $A[k]$.

Possiamo implementare una variante della ricerca binaria per trovare questo picco, operando ricorsivamente sul sottoarray $A[p\dots r]$:
- **Caso base:** Se $p == r$, il sottoarray è composto da un solo elemento. Essendo l'unico rimasto, deve essere il massimo e quindi restituiamo il suo valore ($A[p]$).
- **Passo ricorsivo:** Altrimenti, si divide il sottoarray calcolando il punto medio $q = \lfloor(p+r)/2\rfloor$.
  Si confronta $A[q]$ con il suo elemento successivo $A[q+1]$:
  - Se $A[q] < A[q+1]$, significa che stiamo "salendo". Siamo ancora nella porzione crescente dell'array e il massimo deve trovarsi rigorosamente alla destra di $q$. Si effettua la chiamata ricorsiva su $A[q+1\dots r]$.
  - Altrimenti, $A[q] > A[q+1]$ (gli elementi sono distinti), il che significa che stiamo "scendendo". Il massimo si trova alla nostra sinistra, includendo possibilmente la posizione $q$ stessa. Si effettua la chiamata ricorsiva su $A[p\dots q]$.

---

### ii. Pseudocodice

```algorithmic
// Funzione principale (wrapper)
top(A, n)
    return topRec(A, 1, n)

// Procedura ricorsiva
topRec(A, p, r)
    // caso base: restituisco il valore del massimo
    if p == r
        return A[p]
    else
        q = floor((p + r) / 2)

        // se sto salendo, il picco è a destra
        if A[q] < A[q+1]
            return topRec(A, q + 1, r)
        // se sto scendendo, il picco è a sinistra (incluso q)
        else
            return topRec(A, p, q)						
```

---

### iii. Complessità

Ad ogni chiamata ricorsiva, l'algoritmo calcola il punto medio in tempo costante $\Theta(1)$ ed effettua una singola chiamata ricorsiva su un sottoarray grande esattamente la metà del precedente.
L'equazione di ricorrenza risultante è:

$$
T(n) = T\left(\frac{n}{2}\right) + \Theta(1)
$$

Possiamo risolvere questa ricorrenza con il Master Theorem. Identifichiamo i parametri $a = 1$, $b = 2$ e $f(n) = \Theta(1)$.
Calcoliamo lo spartiacque:

$$
n^{\log_b a} = n^{\log_2 1} = n^0 = 1
$$

Poiché $f(n) \approx n^{\log_b a}$, ricadiamo nel **Caso 2** del Master Theorem. Di conseguenza, la complessità temporale è logaritmica:

$$
T(n) = \Theta(\log n)
$$
