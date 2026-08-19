# Esercizio 20 - Reverse Counting Sort

Realizzare una funzione `RevCountingSort(A, B, n, k)` che, dato un array $A[1\dots n]$ contenente interi nell'intervallo $[0\dots k]$, restituisce in $B[1\dots n]$ una sua permutazione ordinata in modo decrescente utilizzando una variante del counting sort. Valutarne la complessità.

---

### i. Idea e Ragionamento

L’algoritmo `CountingSort(A, B, k)` standard prende in input un array $A[1\dots n]$ tale che $\forall j \in \{1\dots n\}$ si ha $A[j] \in \{0, 1, \dots, k\}$. Il parametro $k$ rappresenta il limite superiore dei valori presenti. Utilizza un array ausiliario $C[0\dots k]$ inizialmente inizializzato a $0$.

Per ordinare in senso **crescente**, l'algoritmo conta le frequenze in $C[x]$ e poi calcola le frequenze cumulative da sinistra a destra ($C[i] = C[i] + C[i-1]$). In questo modo, $C[x]$ indica il numero di elementi $\le x$, ovvero la posizione limite destra in cui inserire $x$ nell'array finale.

Se vogliamo che $B[1\dots n]$ sia ordinato in senso **decrescente**, ci basta notare che, anziché memorizzare il numero di elementi $\le x$, possiamo salvare in $C[x]$ il numero di elementi che sono $\ge x$ nell'array $A$.
Per farlo, modifichiamo la fase di accumulo: scorriamo $C[0\dots k]$ da $k-1$ fino a $0$ (anziché da $1$ a $k$) e salviamo il risultato di $C[i] = C[i] + C[i+1]$. Il resto dello pseudocodice rimane invariato, preservando anche l'importante proprietà di **stabilità** dell'algoritmo.

---

### ii. Pseudocodice

```text
RevCountingSort(A, B, n, k)
    // inizializzazione
    initialize C[0...k] all to 0

    // primo ciclo: calcolo delle frequenze
    for j = 1 to n
        C[A[j]]++

    // secondo ciclo: scorriamo da destra verso sinistra
    // C[i] conterrà il num. di elementi >= i in A		
    for i = k - 1 downto 0
        C[i] = C[i] + C[i+1]

    // terzo ciclo: riempimento array di output
    // scorriamo da n giù fino a 1 per mantenere la stabilità
    for j = n downto 1
        B[C[A[j]]] = A[j]
        C[A[j]]--		
```

---

### iii. Tracciamento (Esempio)

Dato l'array $A = \{1, 4, 2, 0, 1, 2, 0, 2\}$ con $n=8$ e $k=4$:

Prima del secondo ciclo `for` (frequenze pure), abbiamo:
$C = \{2, 2, 3, 0, 1\}$

Dopo il secondo ciclo `for` (frequenze cumulative inverse, elementi $\ge x$):
$C = \{8, 6, 4, 1, 1\}$

Nell’ultimo ciclo, scorrendo $j$ da $8$ giù a $1$:
- $j=8, A[8]=2 \implies B[C[2]] = B[4] = 2$. Aggiorno $C[2] = 4 - 1 = 3$
- $j=7, A[7]=0 \implies B[C[0]] = B[8] = 0$. Aggiorno $C[0] = 8 - 1 = 7$
- $j=6, A[6]=2 \implies B[C[2]] = B[3] = 2$. Aggiorno $C[2] = 3 - 1 = 2$
- $j=5, A[5]=1 \implies B[C[1]] = B[6] = 1$. Aggiorno $C[1] = 6 - 1 = 5$
- $j=4, A[4]=0 \implies B[C[0]] = B[7] = 0$. Aggiorno $C[0] = 7 - 1 = 6$
- $j=3, A[3]=2 \implies B[C[2]] = B[2] = 2$. Aggiorno $C[2] = 2 - 1 = 1$
- $j=2, A[2]=4 \implies B[C[4]] = B[1] = 4$. Aggiorno $C[4] = 1 - 1 = 0$
- $j=1, A[1]=1 \implies B[C[1]] = B[5] = 1$. Aggiorno $C[1] = 5 - 1 = 4$

Alla fine otteniamo $B = \{4, 2, 2, 2, 1, 1, 0, 0\}$, perfettamente ordinato in senso decrescente. Inoltre, l'ordine relativo degli elementi uguali è stato rispettato.

---

### iv. Complessità

La complessità di `RevCountingSort(A, B, n, k)` resta identica a quella del `CountingSort` classico.

- **Complessità Temporale:** L'algoritmo esegue cicli separati non annidati di lunghezza $n$, $k$ e di nuovo $n$. Pertanto il tempo di esecuzione è $\Theta(n + k)$. In particolare, se $k = \mathcal{O}(n)$, la complessità scende a $\Theta(n)$, ovvero tempo lineare.
- **Complessità Spaziale:** È richiesta l'allocazione dell'array di supporto $C$ di dimensione $k+1$ e dell'array di output $B$ di dimensione $n$. Pertanto la complessità spaziale complessiva è $\Theta(n + k)$.
