# Esercizio 21 - Coppia con valore doppio

Realizzare una funzione `Double(A, n)` che, dato un array `A[1..n]` ordinato in senso crescente, verifica se esiste una coppia di indici $i, j$ tali che $A[j] = 2 \cdot A[i]$. Restituisce la coppia se esiste e `(0, 0)` altrimenti. Scrivere lo pseudocodice e valutare la complessità.

---

### Soluzione

Il testo dell’esercizio non specifica esattamente quali indici $(i,j)$ dobbiamo cercare, quindi assumo che la soluzione possa avere anche indici non necessariamente distinti, ovvero che sia possibile $i=j$.

Questo caso può avvenire solo se $A[i]=0$, dato che allora vale:

$$
A[i] = 2 \cdot A[i].
$$

Un approccio ingenuo avrebbe complessità quadratica, perché confronta ciascuna possibile coppia $(i,j)$.

Possiamo però sfruttare il fatto che $A[1 \dots n]$ sia ordinato in senso crescente per implementare una scansione con due indici, cercando una coppia $(i,j)$ tale che:

$$
2 \cdot A[i] = A[j].
$$

Ovvero, facciamo una ricerca iniziando con $i=j=1$ e utilizziamo un ciclo che verifica ad ogni iterazione il confronto tra $2 \cdot A[i]$ e $A[j]$.

Se abbiamo:

$$
2 \cdot A[i] > A[j],
$$

allora il valore $A[j]$ è troppo piccolo rispetto a $2 \cdot A[i]$. Quindi incrementiamo $j$ di $1$, cercando un valore più grande.

Se invece abbiamo:

$$
2 \cdot A[i] < A[j],
$$

allora il valore $2 \cdot A[i]$ è troppo piccolo rispetto ad $A[j]$. Quindi incrementiamo $i$ di $1$, cercando un valore più grande per $A[i]$.

Si può uscire dal ciclo se una delle tre condizioni non vale più:

$$
(i \le n) \land (j \le n) \land (2 \cdot A[i] \ne A[j]).
$$

Se esco dal ciclo e valgono ancora le prime due condizioni, cioè:

$$
i \le n
\qquad \text{e} \qquad
j \le n,
$$

allora sono uscito necessariamente perché ho trovato:

$$
2 \cdot A[i] = A[j],
$$

e quindi restituisco la coppia $(i,j)$, che è una soluzione.

Altrimenti, se sono uscito perché almeno uno dei due indici ha superato $n$, allora restituisco correttamente la coppia $(0,0)$, non avendo trovato nessuna soluzione.

---

### Pseudocodice

```text
// restituisce (i,j) tale che 2*A[i] = A[j], oppure (0,0)
Double(A,n)
    i = 1
    j = 1

    // scansiono l'array con due indici
    while i <= n and j <= n and 2*A[i] != A[j]

        // se 2*A[i] e' troppo grande rispetto ad A[j],
        // incremento j per cercare un A[j] piu grande
        if 2 * A[i] > A[j]
            j = j + 1

        // altrimenti 2*A[i] e' troppo piccolo,
        // quindi incremento i per cercare un A[i] piu grande
        else
            i = i + 1

    // quando esco dal while, se i e j sono ancora entrambi validi,
    // allora sono uscito perche ho trovato 2*A[i] == A[j]
    if i <= n and j <= n
        return (i,j)
    else
        return (0,0)
```

---

### Complessità

La complessità deriva dal ciclo `while`, che ad ogni iterazione incrementa uno degli indici $i$ oppure $j$ di $1$.

Gli indici $i$ e $j$ non vengono mai decrementati e ciascuno può essere incrementato al massimo fino a superare $n$.

Quindi, nel caso peggiore, il numero di iterazioni è al più lineare in $n$, ad esempio al più circa $2n$ iterazioni.

Pertanto la complessità temporale complessiva è:

$$
T(n)=\Theta(n).
$$

La complessità spaziale è:

$$
\mathcal{O}(1),
$$

perché usiamo solo un numero costante di variabili ausiliarie.
