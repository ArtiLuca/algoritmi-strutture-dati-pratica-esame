# Massimo con Divide et Impera

Realizzare una procedura di tipo *divide et impera* `Max(A, p, r)` per trovare il massimo nell'array `A[p..r]`.

Si assuma che l'array non sia vuoto, ovvero $p \le r$.

Scrivere lo pseudocodice e valutare la complessità con il Master Theorem.

---

### Soluzione

Ho deciso di fare questo esercizio come una sorta di "ripasso" sul funzionamento degli algoritmi *Divide et Impera*, scrivendo prima lo pseudocodice per la procedura `Max(A,p,r)` e valutando la sua complessità, per poi usare un esempio concreto su come andrebbe a funzionare effettivamente.

### Idea

Non abbiamo nessuna informazione sul contenuto dell'array $A[p \dots r]$ oltre al fatto che non sia vuoto, cioè $p \le r$.

Quindi, non sappiamo niente sulla presenza di valori duplicati oppure sul suo ordinamento.

Possiamo comunque operare in stile *Divide et Impera* per trovare l'elemento di valore massimo.

Se $p=r$, allora il sottoarray $A[p \dots r]$ contiene un solo elemento e quindi si restituisce $A[p]$, che è necessariamente il massimo dell'unico elemento del sottoarray.

Altrimenti, si divide il sottoarray $A[p \dots r]$ in due parti circa uguali $A[p \dots q]$ e $A[q+1 \dots r]$ e si calcola ricorsivamente il massimo di ciascuna metà. Dopodiché si restituisce il valore massimo trovato, confrontando i due massimi restituiti dalle due chiamate ricorsive.

### Pseudocodice

```text
// Restituisce l'elemento di A[p..r] con valore massimo
Max(A,p,r)
    // caso base: sottoarray composto da un solo elemento
    if p == r
        return A[p]

    else
        q = floor((p+r)/2)

        // calcolo ricorsivamente il massimo di ciascuna metà
        m1 = Max(A,p,q)
        m2 = Max(A,q+1,r)

        // confronto e restituisco il massimo trovato
        if m1 >= m2
            return m1
        else
            return m2
```

### Complessità

La complessità è data dalle due chiamate ricorsive sui due sottoarray di dimensione circa $\frac{n}{2}$ e dal lavoro costante fatto per confrontare i due valori massimi restituiti.

Quindi possiamo esprimere la complessità mediante la ricorrenza:

$$
T(n) = 2T\left(\frac{n}{2}\right) + \Theta(1)
$$

dove $\Theta(1)$ è il lavoro costante fatto per il confronto tra `m1` e `m2`.

Usando il Master Theorem abbiamo:

$$
a=2,
\qquad
b=2,
\qquad
f(n)=\Theta(1)
$$

e quindi:

$$
n^{\log_b a} = n^{\log_2 2} = n.
$$

Dato che:

$$
f(n)=\Theta(1)=O(n^{1-\varepsilon})
$$

per esempio scegliendo $\varepsilon=1$, siamo nel caso 1 del Master Theorem.

Quindi si conclude che:

$$
T(n)=\Theta(n).
$$

In modo intuitivo, ogni elemento dell'array diventa una foglia dell'albero di ricorsione e ad ogni passo di risalita si confrontano due massimi locali. Quindi il lavoro totale è lineare.

In particolare, se si contano esattamente i confronti tra valori dell'array, l'algoritmo esegue $n-1$ confronti.

---

### Esempio di esecuzione

Non richiesto dall'esercizio, ma utile per entrare nell'ottica del funzionamento ricorsivo degli algoritmi *Divide et Impera*.

Consideriamo l'array:

$$
A = [1,4,9,-1,5,13,2,-5,8]
$$

con indicizzazione da $1$ a $9$.

```text
Indici: [1, 2, 3,  4, 5,  6, 7,  8, 9]
Array:  [1, 4, 9, -1, 5, 13, 2, -5, 8]
```

La chiamata principale è:

```text
Max(A,1,9)
```

### Fase di divisione

L'algoritmo spezza l'array calcolando ricorsivamente:

$$
q = \left\lfloor \frac{p+r}{2} \right\rfloor.
$$

```text
Max(A,1,9)
    q = 5
    sottoproblemi: A[1..5] e A[6..9]

Max(A,1,5)
    q = 3
    sottoproblemi: A[1..3] e A[4..5]

Max(A,6,9)
    q = 7
    sottoproblemi: A[6..7] e A[8..9]

Max(A,1,3)
    q = 2
    sottoproblemi: A[1..2] e A[3..3]

Max(A,4,5)
    q = 4
    sottoproblemi: A[4..4] e A[5..5]

Max(A,6,7)
    q = 6
    sottoproblemi: A[6..6] e A[7..7]

Max(A,8,9)
    q = 8
    sottoproblemi: A[8..8] e A[9..9]
```

Alla fine si raggiungono i casi base, cioè sottoarray composti da un solo elemento.

### Fase di risalita

Ora l'algoritmo confronta i massimi locali restituiti dalle chiamate ricorsive.

```text
Max(A,1,2)
    confronta 1 e 4
    restituisce 4

Max(A,1,3)
    confronta 4 e 9
    restituisce 9

Max(A,4,5)
    confronta -1 e 5
    restituisce 5

Max(A,1,5)
    confronta 9 e 5
    restituisce 9
```

Quindi il massimo della metà sinistra `A[1..5]` è:

```text
9
```

Per la metà destra:

```text
Max(A,6,7)
    confronta 13 e 2
    restituisce 13

Max(A,8,9)
    confronta -5 e 8
    restituisce 8

Max(A,6,9)
    confronta 13 e 8
    restituisce 13
```

Quindi il massimo della metà destra `A[6..9]` è:

```text
13
```

Infine, nella chiamata iniziale:

```text
Max(A,1,9)
    confronta 9 e 13
    restituisce 13
```

Quindi il risultato finale è:

```text
13
```

che corrisponde correttamente al massimo globale dell'array.
