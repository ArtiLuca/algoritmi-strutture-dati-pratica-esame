# Esercizio 5 — Array Alternante

Un array $A[1\dots n]$ di numeri si dice **alternante** se non ha elementi contigui identici (ovvero per ogni $i \le n-1$ vale $A[i] \ne A[i+1]$) e inoltre per ogni $i \le n-2$, vale che $a_i < a_{i+1} > a_{i+2}$ oppure $a_i > a_{i+1} < a_{i+2}$. Ad esempio gli array `[1, 2, -1, 3, 2]` e `[5, 1, 2, -1, 3, 2]` sono alternanti, mentre non lo sono `[1, 2, 3]` e `[1, 1, 2]`.

Scrivere una funzione ricorsiva `alt(A, n)` che dato un array $A[1\dots n]$ di numeri verifica se è alternante e valutarne la complessità.

---

### i. Idea e Analisi Logica

Per questo esercizio possiamo analizzare la struttura basandoci su tre array concreti di supporto:
- $A1 = \{10, 5, 20, 2, 8, 4\}$
- $A2 = \{1, 7, 3, 9, 2, 8, 4, 10, 5\}$
- $A3 = \{50, 40, 60, 30, 70, 20, 80, 10, 90, 5, 100, 2\}$

Possiamo notare che la condizione per un array alternante si basa su ogni terna di elementi contigui. Ovvero, dato un indice $i \in \{1 \dots n-2\}$, devono valere le seguenti due condizioni:
1. $A[i] \ne A[i+1]$ e $A[i+1] \ne A[i+2]$ (non possono esserci elementi contigui uguali).
2. ($A[i] < A[i+1]$ e $A[i+1] > A[i+2]$) oppure ($A[i] > A[i+1]$ e $A[i+1] < A[i+2]$).

Quindi, per definizione, un array alternante deve contenere almeno tre elementi, senza duplicati contigui e che sia alternante in uno dei due versi.
In particolare, è utile osservare che se $A[1\dots n]$ contiene almeno tre elementi, possiamo impostare un flag booleano per la direzione dell’alternanza in base al confronto fra i suoi primi due elementi:

- Se $A[1] < A[2] \implies \text{dir} = \text{true}$
- Se $A[1] > A[2] \implies \text{dir} = \text{false}$

Dopodiché, possiamo verificare ricorsivamente che ogni terna soddisfi le condizioni, invertendo il senso dell’alternanza tramite questo flag `dir`.
Ci fermiamo quando $i + 2 > n$ per evitare di sforare i limiti dell'array (*out-of-bounds*).

---

### ii. Pseudocodice

Uso una procedura principale `alt(A, n)` che agisce da wrapper e una procedura ricorsiva `altRec(A, i, n, dir)` per verificare che la terna in $A[i \dots i+2]$ soddisfi la definizione.

```algorithmic
// restituisce true se l'array è alternante, false altrimenti
alt(A, n)
    // se ha meno di tre elementi, non può essere alternante
    if n < 3
        return false

    if A[1] < A[2]
        dir = true  // indica che l'alternanza inizialmente sale
    else
        dir = false // indica che l'alternanza inizialmente scende

    return altRec(A, 1, n, dir)

// procedura ricorsiva per verificare che la terna i..i+2 sia alternante
altRec(A, i, n, dir)
    // caso base: abbiamo verificato tutti gli elementi senza trovare violazioni
    if i + 2 > n
        return true

    // se ci sono elementi contigui uguali, c'è una violazione
    if A[i] == A[i+1] or A[i+1] == A[i+2]
        return false 		

    if dir == true
        if not (A[i] < A[i+1] and A[i+1] > A[i+2])
            return false
    else
        if not (A[i] > A[i+1] and A[i+1] < A[i+2])
            return false		

    // se nessuna violazione, incrementiamo l'indice invertendo la direzione
    return altRec(A, i + 1, n, not dir)								
```

---

### iii. Valutazione della Complessità

- **Complessità Temporale:** La ricorrenza associata all'algoritmo è:

$$
T(n) = T(n-1) + \Theta(1) \implies \Theta(n)
$$

L'algoritmo effettua una singola scansione lineare esaminando gli elementi in tempo costante per ciascun passo ricorsivo.

- **Complessità Spaziale:** Lo spazio utilizzato nel caso peggiore è $\Theta(n)$ a causa della profondità dello stack di ricorsione, che nel caso di array alternanti validi cresce linearmente con la dimensione dell'input $n$.
