# Esercizio 31 - Sottosequenza Palindroma Massima

Dare un algoritmo per individuare, all'interno di una stringa $a_1 \dots a_n$, una sottosequenza, quindi una sequenza di caratteri possibilmente non consecutivi, palindroma di lunghezza massima.

Ad esempio, nella stringa `corollario` la sottosequenza palindroma di lunghezza massima è `orllro`.

Più precisamente:

- **i.** dare una caratterizzazione ricorsiva della lunghezza massima $\ell_{i,j}$ di una sottosequenza palindroma di $a_i \dots a_j$;
- **ii.** tradurre tale definizione in un algoritmo bottom-up o top-down con memoization che determina la lunghezza massima;
- **iii.** trasformare l'algoritmo in modo che fornisca anche la sottosequenza, non solo la sua lunghezza;
- **iv.** valutare la complessità dell'algoritmo.

---

## i. Caratterizzazione ricorsiva

Definiamo $\ell_{i,j}$ come la lunghezza massima di una sottosequenza palindroma in $a_i \dots a_j$, dove $len = j-i+1$ indica la lunghezza dell'intervallo considerato.

Possiamo fare le seguenti osservazioni:

- Se $i > j$, allora $len \le 0$ e stiamo considerando la sottosequenza vuota $\varepsilon$, che è palindroma per definizione. In questo caso $\ell_{i,j}=0$.
- Se $i=j$, allora $len=1$ e stiamo considerando una sottosequenza composta da un solo carattere, che è palindroma per definizione. In questo caso $\ell_{i,j}=1$.
- Se $i < j$, allora stiamo considerando una sottosequenza di almeno due caratteri. In questo caso bisogna confrontare gli estremi $a_i$ e $a_j$.
  - Se $a_i=a_j$, possiamo usare questi due caratteri per estendere la sottosequenza palindroma massima della parte interna $a_{i+1}\dots a_{j-1}$. Quindi $\ell_{i,j}=2+\ell_{i+1,j-1}$.
  - Se $a_i\ne a_j$, non possiamo usare entrambi gli estremi insieme, quindi dobbiamo valutare quale estremità scartare per ottenere la lunghezza massima. Quindi $\ell_{i,j}=\max\{\ell_{i+1,j},\ell_{i,j-1}\}$.

Riassumendo, la ricorrenza per il calcolo di $\ell_{i,j}$ è:

$$
\ell_{i,j}=
\begin{cases}
0 & \text{se } i > j, \\
1 & \text{se } i = j, \\
2 + \ell_{i+1,j-1} & \text{se } i < j \text{ e } a_i = a_j, \\
\max\{\ell_{i+1,j},\ell_{i,j-1}\} & \text{se } i < j \text{ e } a_i \ne a_j.
\end{cases}
$$

---

## ii. Algoritmo per la lunghezza massima

Possiamo implementare un algoritmo bottom-up che considera tutti gli intervalli $A[i\dots j]$ di lunghezza crescente, partendo dalla lunghezza $2$ fino a $n$.

Utilizziamo una tabella $L[0\dots n,0\dots n]$, dove $L[i,j]$ rappresenta il valore $\ell_{i,j}$, cioè la lunghezza massima di una sottosequenza palindroma in $a_i\dots a_j$.

Gestiamo prima i casi base $L[i,i-1]$ e $L[i,i]$, e poi riempiamo il resto della tabella seguendo la ricorrenza.

```algorithmic
Palindrome(A)
    n = length(A)

    // allocazione tabella
    allocate L[0..n, 0..n]

    // gestione casi base
    for i = 1 to n
        L[i, i-1] = 0
        L[i, i] = 1

    // riempimento per intervalli di lunghezza almeno 2
    for len = 2 to n
        for i = 1 to n - len + 1
            j = i + len - 1

            if A[i] == A[j]
                L[i,j] = 2 + L[i+1, j-1]
            else
                L[i,j] = max(L[i+1, j], L[i, j-1])

    return L[1,n]
```

---

## iii. Ricostruzione della soluzione

Per ottenere anche la sottosequenza palindroma, presento due opzioni.

La prima usa una tabella aggiuntiva per salvare le scelte fatte durante il riempimento della tabella $L$.

La seconda non usa una tabella aggiuntiva, ma ricostruisce una soluzione navigando direttamente nella tabella $L$.

---

### Opzione 1: tabella delle scelte

Usiamo una seconda tabella $P[0\dots n,0\dots n]$ per memorizzare la scelta ottima presa durante il calcolo.

In particolare:

- `c` indica che scegliamo entrambi gli estremi $a_i$ e $a_j$;
- `l` indica che usiamo $L[i,j-1]$, quindi scartiamo l'estremo destro;
- `r` indica che usiamo $L[i+1,j]$, quindi scartiamo l'estremo sinistro.

```algorithmic
Palindrome_Opt1(A)
    n = length(A)

    allocate L[0..n, 0..n]
    allocate P[0..n, 0..n]

    // casi base
    for i = 1 to n
        L[i, i-1] = 0
        L[i, i] = 1

    // riempimento con tracciamento delle scelte
    for len = 2 to n
        for i = 1 to n - len + 1
            j = i + len - 1

            if A[i] == A[j]
                L[i,j] = 2 + L[i+1, j-1]
                P[i,j] = 'c'
            else
                if L[i, j-1] >= L[i+1, j]
                    L[i,j] = L[i, j-1]
                    P[i,j] = 'l'
                else
                    L[i,j] = L[i+1, j]
                    P[i,j] = 'r'

    return L[1,n], getPalindrome(A, 1, n, P)

getPalindrome(A, i, j, P)
    if i > j
        return ""

    if i == j
        return A[i]

    if P[i,j] == 'c'
        return A[i] + getPalindrome(A, i+1, j-1, P) + A[j]
    else if P[i,j] == 'l'
        return getPalindrome(A, i, j-1, P)
    else
        return getPalindrome(A, i+1, j, P)
```

---

### Opzione 2: traceback implicito senza memoria extra

In questa seconda opzione non usiamo la tabella $P$.

Dopo aver calcolato la tabella $L$, ricostruiamo una soluzione confrontando i valori già presenti in $L$.

```algorithmic
// La procedura Palindrome(A) rimane identica a quella del punto (ii)

getPal(A, i, j, L)
    if i > j
        return ""

    if i == j
        return A[i]

    if A[i] == A[j] and L[i,j] == 2 + L[i+1, j-1]
        return A[i] + getPal(A, i+1, j-1, L) + A[j]

    if L[i,j] == L[i+1, j]
        return getPal(A, i+1, j, L)
    else
        return getPal(A, i, j-1, L)
```

Questa procedura restituisce una delle possibili sottosequenze palindrome massime. In caso di pareggi, la scelta dipende dall'ordine dei controlli nella procedura di ricostruzione.

---

## iv. Complessità

La tabella $L$ contiene $\Theta(n^2)$ stati.

Ogni stato viene calcolato in tempo $\Theta(1)$, perché richiede al massimo un confronto tra caratteri e l'accesso a valori già presenti nella tabella.

Quindi il tempo necessario per calcolare la lunghezza massima è:

$$
\Theta(n^2).
$$

La procedura di ricostruzione scorre al massimo $n$ posizioni, quindi richiede tempo $O(n)$, assorbito dal costo del riempimento della tabella.

Pertanto, la complessità temporale complessiva è:

$$
\Theta(n^2).
$$

Per quanto riguarda lo spazio, la tabella $L$ occupa $\Theta(n^2)$ celle.

Nell'opzione 1 si usa anche la tabella $P$, che occupa anch'essa $\Theta(n^2)$ spazio.

In entrambi i casi, la complessità spaziale complessiva rimane:

$$
O(n^2).
$$

Se si considera anche lo stack della ricostruzione ricorsiva, si aggiunge un costo $O(n)$, che viene comunque assorbito dallo spazio della tabella.
