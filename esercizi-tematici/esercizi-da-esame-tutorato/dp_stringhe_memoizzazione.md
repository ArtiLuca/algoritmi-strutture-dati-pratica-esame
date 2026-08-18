# Esercizio 2 - DP su stringhe con Memoization

Data una stringa $X = x_1, x_2, \dots, x_n$, si consideri la seguente quantità $\ell(i, j)$, definita per $1 \le i \le j \le n$:

$$
\ell(i, j) =
\begin{cases}
1 & \text{se } i = j \\
2 & \text{se } i = j - 1 \\
2 + \ell(i + 1, j - 1) & \text{se } i \lt j - 1 \text{ e } x_i = x_j \\
\sum_{k=i}^{j-1}(\ell(i,k) + \ell(k+1,j)) & \text{se } i \lt j - 1 \text{ e } x_i \ne x_j
\end{cases}
$$

- **(1)** Scrivere una coppia di algoritmi `INIT_L(X)` e `REC_L(i, j)` per il calcolo memoizzato di $\ell(1, n)$.
- **(2)** Si determini la complessità al caso migliore $T_{\text{best}}(n)$ supponendo che le uniche operazioni di costo unitario e non nullo siano i confronti tra caratteri.

---

### 1. Algoritmi per il calcolo memoizzato

Di seguito la procedura di inizializzazione e la routine ricorsiva top-down.
Si assume che la matrice $L$ sia accessibile globalmente (o passata per riferimento).

```text
// Procedura di inizializzazione
INIT_L(X)
    n = length(X)

    // Ottimizzazione per stringhe molto corte
    if n == 1
        return 1
    if n == 2
        return 2

    allocate L[1...n, 1...n]

    // Gestione dei casi base (diagonali)
    for i = 1 to n - 1
        L[i, i] = 1
        L[i, i+1] = 2

    L[n, n] = 1		

    // Riempimento della tabella con valore di default (0 = non calcolato)
    // per i sottoproblemi di lunghezza >= 3
    for i = 1 to n - 2
        for j = i + 2 to n
            L[i, j] = 0

    // Invocazione della routine ricorsiva
    return REC_L(X, 1, n)

// Routine ricorsiva
REC_L(X, i, j)
    // Verifica se il sottoproblema deve ancora essere risolto
    if L[i, j] == 0
        // Confronto tra caratteri esterni
        if X[i] == X[j]
            L[i, j] = 2 + REC_L(X, i+1, j-1)
        else
            for k = i to j - 1
                L[i, j] = L[i, j] + REC_L(X, i, k) + REC_L(X, k+1, j)

    return L[i, j]																	
```

---

### 2. Complessità al caso migliore $T_{\text{best}}(n)$

Per determinare il caso migliore $T_{\text{best}}(n)$, assumiamo che le uniche operazioni di costo unitario e non nullo siano i confronti tra caratteri, cioè i test del tipo `X[i] == X[j]`.

Il caso migliore si ha quando ogni confronto effettivamente eseguito lungo la catena ricorsiva risulta `true`, ad esempio quando la stringa è palindroma.

In questo caso l'algoritmo non entra mai nel ramo `else`, evitando quindi il ciclo `for` della sommatoria. Ad ogni chiamata viene effettuato un solo confronto tra caratteri e poi si passa al sottoproblema interno:

$$
L[1,n] \to L[2,n-1] \to L[3,n-2] \to \dots
$$

Ad ogni passo la dimensione dell'intervallo diminuisce di 2. Quindi la ricorrenza per il numero di confronti nel caso migliore è:

$$
T_{\text{best}}(n)=T_{\text{best}}(n-2)+1
$$

con casi base:

$$
T_{\text{best}}(1)=0
\qquad
T_{\text{best}}(2)=0.
$$

Da questa ricorrenza otteniamo:

$$
T_{\text{best}}(n)=\left\lfloor \frac{n-1}{2} \right\rfloor.
$$

Quindi:

$$
T_{\text{best}}(n)=\Theta(n).
$$
