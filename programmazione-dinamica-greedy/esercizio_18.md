# Esercizio 18 — Sottostringa palindroma di lunghezza massima

## Traccia

Dare un algoritmo per individuare, all'interno di una stringa $a_1 \dots a_n$, una sottostringa, quindi una sequenza di caratteri consecutivi, palindroma di lunghezza massima.

Ad esempio, nella stringa `"colonna"` la sottostringa palindroma di lunghezza massima è `"olo"`.

Più precisamente:

- **i.** dare una caratterizzazione ricorsiva della lunghezza massima $l_{i,j}$ di una sottostringa palindroma di $a_i \dots a_j$;
- **ii.** tradurre tale definizione in un algoritmo bottom-up o top-down con memoization che determina la lunghezza massima;
- **iii.** trasformare l'algoritmo in modo che permetta anche di individuare la stringa, non solo la sua lunghezza;
- **iv.** valutare la complessità dell'algoritmo.

## Idea

Per il punto **i** definiamo $l_{i,j}$ come la lunghezza massima di una sottostringa palindroma contenuta in $a_i \dots a_j$.

Per la proprietà di sottostringa palindroma, ha senso operare su intervalli, dove per intervalli intendo sottostringhe delimitate dagli indici $i \dots j$, considerando le estremità di $a_i \dots a_j$.

In particolare, possiamo fare delle osservazioni sull'intervallo $a_i \dots a_j$ considerando la sua lunghezza, che chiamiamo `len`.

Per una qualsiasi sottostringa definita nell'intervallo $a_i \dots a_j$, avremo che la lunghezza dell'intervallo sarà:

$$
len = j - i + 1
$$

Possiamo fare le seguenti osservazioni:

- Se $i > j$, ovvero `len <= 0`, allora stiamo considerando la sottostringa vuota $\varepsilon$. Visto che la sottostringa vuota è per definizione palindroma, vale che $l_{i,j} = 0$.
- Se $i = j$, ovvero `len = 1`, allora stiamo considerando una sottostringa composta da un unico carattere. Visto che una sottostringa composta da un solo carattere è per definizione palindroma, vale che $l_{i,j} = 1$.
- Se invece $i < j$, allora stiamo considerando una sottostringa composta da almeno due caratteri. Possiamo notare che se vale $a_i = a_j$ e vale anche che la sottostringa interna $a_{i+1} \dots a_{j-1}$ è palindroma, allora possiamo dire che anche la sottostringa $a_i \dots a_j$ è palindroma.
- Ovvero, se troviamo due caratteri uguali $a_i = a_j$, allora possiamo estendere la lunghezza della sottostringa palindroma massima di $a_i \dots a_j$ di `2` solamente se anche la sottostringa interna $a_{i+1} \dots a_{j-1}$ è interamente palindroma.
- Questa seconda condizione di sottostringa interna interamente palindroma si può ridurre alla condizione $l_{i+1,j-1} = j - i - 1$, che segue dalla lunghezza dell'intervallo $a_{i+1} \dots a_{j-1}$.
- Se invece $i < j$ ma abbiamo che $a_i \ne a_j$, oppure se la sottostringa interna non è interamente palindroma, allora dobbiamo massimizzare la lunghezza della sottostringa palindroma scartando un carattere. Quindi consideriamo i due casi $l_{i+1,j}$ e $l_{i,j-1}$ e prendiamo il valore massimo.

## Caratterizzazione ricorsiva

Quindi, riassumendo, possiamo definire la ricorrenza per la lunghezza $l_{i,j}$ della sottostringa palindroma di lunghezza massima in $a_i \dots a_j$ come segue:

$$
l_{i,j} =
\begin{cases}
0 & \text{se } i \gt j, \\
1 & \text{se } i = j, \\
2 + l_{i+1,j-1} & \text{se } i \lt j \text{ e } a_i = a_j \text{ e } l_{i+1,j-1} = j - i - 1, \\
\max\{l_{i+1,j}, l_{i,j-1}\} & \text{altrimenti.}
\end{cases}
$$

## Algoritmo bottom-up

Per il punto **ii** possiamo usare un algoritmo bottom-up `palindrome(A)` che prova tutti gli intervalli di lunghezza da `2` a `n` per trovare la lunghezza della sottostringa palindroma massima.

Si utilizza una tabella $L[0..n, 0..n]$, dove $L[i,j]$ indica la lunghezza massima di una sottostringa palindroma contenuta in $a_i \dots a_j$.

In particolare, si gestiscono prima i casi base della sottostringa vuota, cioè `j = i - 1`, e della sottostringa composta da un solo carattere, cioè `j = i`.

```text
palindrome(A)
    n = length(A)

    // allocazione tabella
    allocate L[0..n, 0..n]

    // gestisco i casi base
    for i = 1 to n
        L[i,i-1] = 0
        L[i,i] = 1

    // riempimento considerando tutte le sottostringhe di lunghezza da 2 a n
    for len = 2 to n
        for i = 1 to n - len + 1
            j = i + len - 1

            // se trovo due caratteri uguali
            // e trovo anche che la sottostringa interna è interamente palindroma
            // allora posso estendere la lunghezza massima
            if A[i] == A[j] and L[i+1,j-1] == j - i - 1
                L[i,j] = 2 + L[i+1,j-1]

            // altrimenti, valuto il massimo scartando un estremo
            else
                L[i,j] = max(L[i+1,j], L[i,j-1])

    return L[1,n]
```

## Ricostruzione della sottostringa

Se volessimo anche ottenere, come richiesto dal punto **iii**, la sottostringa di lunghezza massima trovata, allora bisogna ricordare dove troviamo il massimo e da dove parte la sottostringa palindroma massima trovata come soluzione.

Possiamo utilizzare una seconda tabella $P[1..n, 1..n]$, dove $P[i,j]$ indica l'indice dal quale parte la sottostringa palindroma massima trovata per $a_i \dots a_j$.

Questo perché poi basta aggiungere la lunghezza massima trovata e sottrarre `1` per ottenere gli indici che compongono la soluzione trovata.

Possiamo poi passare questi indici ad una procedura `printPalindrome(A,start,end)` per stampare la soluzione trovata facendo una semplice scansione lineare di `A`.

```text
palindrome(A)
    n = length(A)

    // allocazione tabelle
    allocate L[0..n, 0..n]
    allocate P[1..n, 1..n]

    // gestisco i casi base, in particolare sottostringhe di un solo carattere
    for i = 1 to n
        L[i,i-1] = 0
        L[i,i] = 1
        P[i,i] = i

    // riempimento come prima, però tenendo traccia dell'indice di partenza
    for len = 2 to n
        for i = 1 to n - len + 1
            j = i + len - 1

            // se possiamo estendere il massimo
            if A[i] == A[j] and L[i+1,j-1] == j - i - 1
                L[i,j] = 2 + L[i+1,j-1]
                P[i,j] = i

            // altrimenti, scegliamo il sottoproblema migliore
            else
                if L[i+1,j] >= L[i,j-1]
                    L[i,j] = L[i+1,j]
                    P[i,j] = P[i+1,j]
                else
                    L[i,j] = L[i,j-1]
                    P[i,j] = P[i,j-1]

    start = P[1,n]
    end = P[1,n] + L[1,n] - 1

    printPalindrome(A, start, end)

    return L[1,n]


// Procedura di stampa
printPalindrome(A, start, end)
    for i = start to end
        print A[i]
```

## Complessità

Per quanto riguarda il punto **iv**, la complessità temporale è complessivamente:

$$
\Theta(n^2)
$$

Questo perché l'algoritmo considera tutti gli intervalli possibili della stringa usando due cicli annidati.

La procedura di stampa finale è lineare, cioè:

$$
\Theta(n)
$$

e quindi viene assorbita dal costo quadratico.

Anche lo spazio utilizzato è complessivamente:

$$
O(n^2)
$$

perché usiamo le due tabelle $L[0..n, 0..n]$ e $P[1..n, 1..n]$, che sono entrambe di dimensione quadratica.
