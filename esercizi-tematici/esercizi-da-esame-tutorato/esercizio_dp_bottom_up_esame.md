# Esercizio 2 — Programmazione dinamica bottom-up

Date due stringhe $X = \langle x_1, x_2, \dots, x_m \rangle$ e $Y = \langle y_1, y_2, \dots, y_n \rangle$, si consideri la seguente quantità $\ell(i, j)$, definita per ogni coppia di valori $i, j$ con $0 \le i \le m$ e $0 \le j \le n$:

$$
\ell(i, j) =
\begin{cases}
1 & \text{se } i = 0 \text{ oppure } j = 0 \\
3 \cdot \ell(i, j - 1) & \text{se } i, j > 0 \text{ e } x_i = y_j \\
2 \cdot \ell(i - 1, j - 1) - \ell(i - 1, j) & \text{se } i, j > 0 \text{ e } x_i \ne y_j
\end{cases}
$$

Si vuole calcolare la quantità:

$$
q = \max \{ \ell(i, j) : 0 \le i \le m, 0 \le j \le n \}
$$

- **(a)** Scrivere un algoritmo bottom-up per il calcolo di $q$.
- **(b)** Determinare la complessità esatta dell'algoritmo, supponendo che le uniche operazioni di costo unitario e non nullo siano i confronti tra caratteri.

---

### (a) Algoritmo Bottom-Up

Si usa un algoritmo `ComputeQ` per il calcolo di $q$ utilizzando una tabella bidimensionale $L[0\dots m, 0 \dots n]$ dove $L[i,j]$ contiene il corrispondente valore $\ell(i,j)$ come definito dalla ricorrenza.

```text
ComputeQ(X, Y)
    m = length(X)
    n = length(Y)

    // allocazione tabella bidimensionale
    allocate L[0...m, 0...n]

    // imposto il valore massimo iniziale (basato sui casi base)
    q = 1

    // gestisco i casi base
    for i = 0 to m
        L[i, 0] = 1

    for j = 1 to n // inizio da 1 avendo gia' trattato il caso L[0,0]
        L[0, j] = 1

    // riempimento bottom-up
    for i = 1 to m
        for j = 1 to n

            if X[i] == Y[j]
                L[i, j] = 3 * L[i, j-1]
            else
                L[i, j] = 2 * L[i-1, j-1] - L[i-1, j]

            // verifico se ho trovato un nuovo massimo
            if L[i, j] > q
                q = L[i, j]

    // restituisco il risultato trovato
    return q														
```

---

### (b) Complessità Esatta

Se associamo costo unitario solamente all'operazione di confronto fra caratteri, questo vuol dire semplicemente contare quante iterazioni facciamo nei cicli annidati, essendo che ad ogni iterazione si effettua un solo confronto (`X[i] == Y[j]`).

Ovvero, si effettua un confronto tra caratteri esattamente una volta per ogni $i = 1\dots m$ e $j = 1\dots n$.
Quindi, la complessità esatta corrisponde alla doppia sommatoria:

$$
\sum_{i=1}^{m} \sum_{j=1}^n 1 = m \cdot n
$$

Quindi la complessità esatta del numero di confronti è $T(m, n) = m \cdot n$.
