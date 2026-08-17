# Esercizio 21 - Coppia con valore doppio

Realizzare una funzione `Double(A, n)` che, dato un array $A[1\dots n]$ ordinato in senso crescente, verifica se esiste una coppia di indici $i, j$ tali che $A[j] = 2 \cdot A[i]$. Restituisce la coppia se esiste e $(0, 0)$ altrimenti. Scrivere lo pseudocodice e valutare la complessità.

---

### i. Idea e Ragionamento

Il testo dell'esercizio non specifica esplicitamente se gli indici $(i,j)$ debbano essere distinti, quindi assumiamo che la soluzione possa essere trovata anche con $i=j$.

Questo caso può verificarsi solo se $A[i]=0$, perché allora vale:

$$
A[i] = 2 \cdot A[i].
$$

Un approccio ingenuo avrebbe complessità quadratica $\Theta(n^2)$, perché confronta tutte le possibili coppie $(i,j)$.

Tuttavia, possiamo sfruttare il fatto che $A[1\dots n]$ sia ordinato in senso crescente per implementare un algoritmo basato sulla tecnica dei **due puntatori** in tempo lineare.

L'idea è confrontare le due sequenze ordinate:

$$
A[1], A[2], \dots, A[n]
$$

e

$$
2A[1], 2A[2], \dots, 2A[n].
$$

Dato che moltiplicare per $2$ preserva l'ordinamento, anche la sequenza dei valori $2A[i]$ è ordinata in senso crescente.

Iniziamo con $i=1$ e $j=1$. Ad ogni passo confrontiamo $2 \cdot A[i]$ con $A[j]$:

- se $2 \cdot A[i] = A[j]$, abbiamo trovato una coppia soluzione e restituiamo $(i,j)$;
- se $2 \cdot A[i] > A[j]$, allora $A[j]$ è troppo piccolo, quindi incrementiamo $j$;
- se $2 \cdot A[i] < A[j]$, allora $2 \cdot A[i]$ è troppo piccolo, quindi incrementiamo $i$.

Il ciclo termina quando troviamo una coppia oppure quando uno dei due indici supera $n$.

Se esauriamo l'array senza trovare una coppia valida, restituiamo $(0,0)$.

---

### ii. Pseudocodice

```text
// restituisce (i,j) tale che 2*A[i] = A[j], oppure (0,0)
Double(A, n)
    i = 1
    j = 1

    // scansiono con due puntatori
    while i <= n and j <= n and 2*A[i] != A[j]
        // se il doppio è più grande, cerco un A[j] maggiore spostando j a destra
        if 2 * A[i] > A[j]
            j = j + 1
        // altrimenti, cerco un A[i] maggiore spostando i a destra
        else
            i = i + 1

    // quando esco dal while, se i e j sono entrambi validi ho trovato la soluzione
    if i <= n and j <= n
        return (i,j)
    else
        return (0,0)
```

---

### iii. Correttezza

L'algoritmo mantiene due indici $i$ e $j$ che scorrono rispettivamente la sequenza dei valori $2A[i]$ e la sequenza dei valori $A[j]$.

Poiché $A$ è ordinato in senso crescente, anche la sequenza $2A[1],2A[2],\dots,2A[n]$ è ordinata in senso crescente.

Ad ogni iterazione vale una delle seguenti situazioni:

- se $2A[i] = A[j]$, allora la coppia $(i,j)$ soddisfa la richiesta dell'esercizio;
- se $2A[i] > A[j]$, allora il valore $A[j]$ è troppo piccolo rispetto a $2A[i]$. Poiché gli elementi successivi di $A$ sono maggiori o uguali ad $A[j]$, l'unica possibilità è aumentare $j$;
- se $2A[i] < A[j]$, allora il valore $2A[i]$ è troppo piccolo rispetto ad $A[j]$. Poiché i valori successivi $2A[i+1],2A[i+2],\dots$ sono maggiori o uguali a $2A[i]$, l'unica possibilità è aumentare $i$.

Quindi, ad ogni passo, l'algoritmo scarta correttamente valori che non possono più partecipare ad una soluzione con l'altro indice corrente.

Se il ciclo termina con $i \le n$ e $j \le n$, allora deve essere terminato perché vale $2A[i] = A[j]$, e quindi restituisce correttamente una coppia soluzione.

Se invece uno dei due indici supera $n$, allora una delle due sequenze è stata esaurita senza trovare uguaglianze, e quindi non esiste alcuna coppia valida. In questo caso l'algoritmo restituisce correttamente $(0,0)$.

---

### iv. Complessità

La complessità temporale deriva dal ciclo `while`.

Ad ogni iterazione, uno dei due indici $i$ o $j$ viene sempre incrementato di $1$.

Poiché gli indici non vengono mai decrementati e il limite massimo per entrambi è $n$, nel caso peggiore ci sono al massimo $2n$ iterazioni.

La complessità temporale complessiva è quindi:

$$
T(n)=\Theta(n).
$$

La complessità spaziale è:

$$
\mathcal{O}(1),
$$

poiché vengono utilizzate solo variabili scalari per scorrere l'array.
