# Esercizio 2 — Programmazione dinamica (DP 2023)

Per $n > 0$, siano dati due vettori a componenti intere $a, b \in \mathbb{Z}^n$.
Si consideri la quantità $c(i, j)$ con $0 \le i \le j \le n-1$, definita come segue:

$$
c(i, j) =
\begin{cases}
a_i & \text{se } 0 < i \le n-1 \text{ e } j = n-1 \\
b_j & \text{se } i = 0 \text{ e } 0 \le j \le n-1 \\
c(i-1, j-1) \cdot c(i, j+1) & \text{se } 0 < i \le j < n-1
\end{cases}
$$

Si vuole calcolare la quantità:

$$
m = \max \{ c(i, j) : 0 \le i \le j \le n-1 \}
$$

- **(a)** Fornire un algoritmo iterativo bottom-up per il calcolo di $m$.
- **(b)** Valutare la complessità esatta dell’algoritmo, associando costo unitario alla moltiplicazione tra numeri interi e costo nullo a tutte le altre operazioni.

---

### (a) Algoritmo Bottom-Up

Usiamo l’algoritmo `ComputeM(a, b, n)` per il calcolo bottom-up di $m$. Si utilizza una tabella bidimensionale $C[0\dots n-1, 0\dots n-1]$ dove $C[i, j]$ corrisponde al valore $c(i, j)$ come definito dalla ricorrenza.

È fondamentale notare che per calcolare la cella $(i, j)$ abbiamo bisogno di $(i-1, j-1)$ (già calcolata nella riga precedente) e di $(i, j+1)$ (nella stessa riga, ma alla colonna successiva). Dunque, l'indice di colonna $j$ dovrà essere popolato a ritroso.

```text
ComputeM(a, b, n)

    // allocazione tabella bidimensionale
    allocate C[0...n-1, 0...n-1]

    // imposto il valore massimo iniziale ad un valore minimo assoluto
    m = -∞

    // gestisco il primo caso base (l'ultima colonna), aggiornando il massimo
    for i = 1 to n - 1
        C[i, n-1] = a[i]
        m = max(m, C[i, n-1])

    // gestisco il secondo caso base (la prima riga), aggiornando il massimo
    for j = 0 to n - 1
        C[0, j] = b[j]
        m = max(m, C[0, j])

    // riempimento bottom-up rispettando le dipendenze
    // i cresce per le righe, j decresce per le colonne
    for i = 1 to n - 2
        for j = n - 2 downto i
            C[i, j] = C[i-1, j-1] * C[i, j+1]
            m = max(m, C[i, j])

    // restituisco il risultato globale trovato
    return m
```

---

### (b) Complessità Esatta

Per calcolare la complessità esatta $T(n)$, associamo un costo unitario solamente all'operazione di moltiplicazione e costo nullo a tutte le altre operazioni. Notiamo che le operazioni di moltiplicazione avvengono solamente all'interno dei due cicli annidati `i = 1 ... n-2` e `j = n-2 downto i`, ed avviene esattamente una moltiplicazione a ciascuna iterazione.

Quindi, possiamo calcolare la complessità esatta come segue:

$$
T(n) = \sum_{i=1}^{n-2} \sum_{j=i}^{n-2} 1 = \sum_{i=1}^{n-2} (n - 2 - i + 1) = \sum_{i=1}^{n-2} (n - i - 1)
$$

Se effettuiamo una sostituzione di variabile impostando $k = n - i - 1$, possiamo vedere gli estremi della sommatoria:
- Per $i = 1 \implies k = n - 2$
- Per $i = n - 2 \implies k = n - (n - 2) - 1 = 1$

Quindi, riscriviamo la sommatoria in funzione di $k$ e utilizziamo la formula di Gauss per calcolare la somma dei primi $n-2$ interi:

$$
T(n) = \sum_{k=1}^{n-2} k = \frac{(n-2)(n-1)}{2}
$$

La complessità temporale esatta per le moltiplicazioni è dunque $T(n) = \frac{(n-2)(n-1)}{2}$, che corrisponde asintoticamente a $\Theta(n^2)$.
