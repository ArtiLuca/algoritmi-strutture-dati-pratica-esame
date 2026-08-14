# Ricorrenza memoizzata $M(i,j)$

Sia $n>0$. Si consideri la seguente ricorrenza $M(i,j)$ definita su tutte le coppie $(i,j)$ con $1\leq i\leq j\leq n$:

$$
M(i,j)=
\begin{cases}
1 & \text{se } i=j,\\
2 & \text{se } j=i+1,\\
M(i+1,j-1)\cdot M(i+1,j)\cdot M(i,j-1) & \text{se } j>i+1.
\end{cases}
$$

1. Scrivere una coppia di algoritmi `INIT_M(n)` e `REC_M(i,j)` per il calcolo memoizzato di $M(1,n)$.
2. Calcolare il numero esatto $T(n)$ di moltiplicazioni tra interi eseguite per il calcolo di $M(1,n)$.

---

### (1) Algoritmi per il calcolo memoizzato

Essendo che il testo chiede memoizzazione, l’ordine di riempimento della tabella $M[1\dots n, 1\dots n]$ non è rilevante. In particolare, possiamo velocizzare il calcolo usando "early returns" nella procedura di inizializzazione `INIT_M(n)`. Dopodiché si riempie la tabella gestendo prima i casi base, poi il caso ricorsivo usando un valore di default per indicare "sottoproblema non ancora risolto" ed infine si chiama la routine ricorsiva `REC_M(M,1,n)` per il calcolo memoizzato di $M(1,n)$ dove ho aggiunto come parametro di input la tabella $M$ altrimenti non "funzionerebbe" in senso logico.

```text
// Procedura di inizializzazione
INIT_M(n)
    // per velocizzare i casi banali
    if n == 1
        return 1
    if n == 2
        return 2

    // allocazione tabella e riempimento casi base
    // vado fino a n-1 per gestire il caso base
    allocate M[1...n, 1...n]
    for i = 1 to n-1  
        M[i,i] = 1
        M[i,i+1] = 2
    M[n,n] = 1

    // riempimento con valore di default per sottoproblemi "non ancora risolti"
    // uso il valore di default '0' perché funziona bene in questo caso
    // si va fino a n-2 per j > i + 1
    for i = 1 to n-2        
        for j = i+2 to n
            M[i,j] = 0

    // invocazione routine ricorsiva
    return REC_M(M, 1, n)               
```

```text
// Routine ricorsiva
REC_M(M, i, j)
    // controllo se è il valore di default
    if M[i,j] == 0
        // applico la ricorrenza (2 moltiplicazioni per chiamata utile)
        M[i,j] = REC_M(M, i+1, j-1) * REC_M(M, i+1, j) * REC_M(M, i, j-1)

    return M[i,j]       
```

---

### (2) Calcolo esatto delle moltiplicazioni $T(n)$

Per il punto (2) possiamo notare che le operazioni di moltiplicazione per ogni $M(i,j)$ con $j > i+1$ sono esattamente 2.
Grazie alla memoizzazione, la ricorrenza viene calcolata esattamente una volta per ogni sottoproblema non base. Quindi basta contare quante sono le celle vuote, ovvero quante iterazioni si effettuano nei due cicli for annidati di inizializzazione, che vanno da $i=1\dots n-2$ e $j=i+2 \dots n$.

Quindi abbiamo:
$$ T(n) = \sum_{i=1}^{n-2} \sum_{j=i+2}^{n} 2 = 2 \cdot \sum_{i=1}^{n-2} (n - i - 1) $$

Avendo già fatto sommatorie simili in altri problemi, so che possiamo imporre un cambio di variabile $k = n - i - 1$.
Infatti:
- se $i=1 \implies k = n-2$
- se $i = n-2 \implies k = n - (n-2) - 1 = 1$

Quindi la sommatoria diventa:
$$ 2 \cdot \sum_{k=1}^{n-2} k $$

Usando la somma di Gauss otteniamo quindi:
$$ 2 \cdot \frac{(n-1)(n-2)}{2} = (n-1)(n-2) $$

Quindi il numero esatto di moltiplicazioni effettuate è $T(n) = (n-1)(n-2)$.
