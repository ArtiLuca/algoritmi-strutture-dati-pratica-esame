# Esercizio 21 — Resto con numero minimo di banconote

## Traccia

Si supponga di dover pagare una certa somma $s$.

Per farlo si hanno a disposizione le banconote $b_1, \dots, b_n$, ciascuna di valore $v_1, \dots, v_n$, dove i valori sono numeri naturali.

Si vuole determinare, se esiste, un insieme di banconote:

$$
b_{i_1}, \dots, b_{i_k}
$$

che totalizzi esattamente la somma richiesta e che minimizzi il numero $k$ di banconote utilizzate.

Più precisamente:

- **i.** mostrare che vale la proprietà della sottostruttura ottima e fornire una caratterizzazione ricorsiva del costo $c(s',j)$ della soluzione ottima per il sottoproblema di dare una somma pari a $s'$ con le banconote in $b_1, \dots, b_j$, con $j \le n$;
- **ii.** tradurre tale definizione in un algoritmo bottom-up o top-down con memoization che determina il costo della soluzione ottima;
- **iii.** trasformare l'algoritmo in modo che permetta anche di individuare la soluzione, non solo il suo costo;
- **iv.** valutare la complessità dell'algoritmo.

## Idea

Per il punto **i** possiamo mostrare che il problema gode della proprietà della sottostruttura ottima.

Una soluzione ottima per una somma $s'$ usando le prime $j$ banconote contiene infatti soluzioni ottime per sottoproblemi più piccoli, ottenuti riducendo la somma da totalizzare oppure riducendo il numero di banconote disponibili.

Possiamo osservare che, se dobbiamo totalizzare una somma $s'$ usando le banconote $b_1, \dots, b_j$ di valore $v_1, \dots, v_j$, la scelta ottimale consiste nel valutare se conviene includere oppure no l'ultima banconota $b_j$ di valore $v_j$.

Se non usiamo la banconota $b_j$, allora il costo è identico a quello ottenuto con le prime $j-1$ banconote per la stessa somma $s'$.

Se invece usiamo la banconota $b_j$, assumendo che $v_j \le s'$, allora il costo è uno in più rispetto al costo ottimo per formare la somma $s' - v_j$ usando le prime $j-1$ banconote.

Quindi il problema gode della proprietà di sottostruttura ottima, in quanto una soluzione ottima è composta da soluzioni ottime a sottoproblemi di taglia più piccola.

## Caratterizzazione ricorsiva

Per dare una caratterizzazione ricorsiva al problema, possiamo definire $c(s',j)$ come il numero minimo di banconote necessario per totalizzare esattamente la somma $s'$ usando solo le banconote:

$$
b_1, \dots, b_j
$$

Assumendo di avere le banconote $b_1, \dots, b_j$ di valore $v_1, \dots, v_j$, con $j \le n$, possiamo fare le seguenti osservazioni:

- Se $s' = 0$, allora il costo per totalizzare una somma pari a `0` è `0`, perché non dobbiamo usare nessuna banconota.
- Se $j = 0$ e $s' > 0$, allora abbiamo esaurito le banconote a disposizione e il problema non può essere risolto. Quindi si usa il valore sentinella $+\infty$.
- Se consideriamo la banconota $b_j$ con $j > 0$ e abbiamo che $v_j \le s'$, allora bisogna valutare se conviene utilizzare la banconota oppure scartarla. Se la scartiamo, il costo è $c(s',j-1)$. Se invece la usiamo, il costo è $1 + c(s'-v_j,j-1)$.
- Se consideriamo la banconota $b_j$ con $j > 0$ e abbiamo che $v_j > s'$, allora la banconota non può essere utilizzata nella somma, essendo troppo grande, e quindi la scartiamo.

Riassumendo, possiamo definire una ricorrenza per il calcolo di $c(s',j)$ come segue:

$$
c(s',j) =
\begin{cases}
0 & \text{se } s'=0, \\
+\infty & \text{se } j=0 \text{ e } s' \gt 0, \\
\min(\{1+c(s'-v_j,j-1),\ c(s',j-1)\}) & \text{se } j,s' \gt 0 \text{ e } v_j \le s', \\
c(s',j-1) & \text{se } j,s' \gt 0 \text{ e } v_j \gt s'.
\end{cases}
$$

## Algoritmo con memoization

Per il punto **ii** possiamo usare una tabella $C[0..s, 0..n]$, dove $C[sPrime,j]$ indica il numero minimo di banconote necessario per totalizzare esattamente la somma `sPrime` usando solo le prime `j` banconote.

Uso un approccio memoizzato costituito da un algoritmo di inizializzazione `initBanconote(s,v,n)`, che si occupa del riempimento iniziale della tabella usando come valore di default `-1` per indicare sottoproblemi ancora non risolti.

Si assume che venga passato come parametro un array $v[1..n]$ contenente il valore delle banconote a disposizione.

Infine, l'algoritmo chiama la procedura ricorsiva `banconoteRec(sPrime,v,j,C)` per risolvere il problema.

In particolare, il valore di ritorno $C[s,n]$ si interpreta così:

- se vale $+\infty$, allora non esiste una soluzione;
- altrimenti, indica il numero minimo di banconote necessarie.

```text
// procedura di inizializzazione
initBanconote(s, v, n)

    // allocazione tabella
    allocate C[0..s, 0..n]

    // riempimento iniziale con valore di default
    for sPrime = 0 to s
        for j = 0 to n
            C[sPrime,j] = -1

    // invocazione routine ricorsiva
    return banconoteRec(s, v, n, C)


// routine ricorsiva
banconoteRec(sPrime, v, j, C)

    // controllo per valore di default
    if C[sPrime,j] == -1

        // se somma pari a 0
        if sPrime == 0
            C[sPrime,j] = 0

        // se ho finito le banconote a disposizione
        else if j == 0
            C[sPrime,j] = +∞

        // se la banconota può essere usata, valuto se conviene usarla o scartarla
        else if v[j] <= sPrime
            used = 1 + banconoteRec(sPrime - v[j], v, j-1, C)
            notUsed = banconoteRec(sPrime, v, j-1, C)
            C[sPrime,j] = min(used, notUsed)

        // altrimenti la banconota non può essere utilizzata
        else
            C[sPrime,j] = banconoteRec(sPrime, v, j-1, C)

    return C[sPrime,j]
```

## Ricostruzione della soluzione

Per quanto riguarda il punto **iii**, se volessimo anche tenere traccia di quali banconote vengono utilizzate nella soluzione ottima trovata, inizialmente volevo usare un solo array $B[0..n]$ per indicare tramite un valore booleano se una data banconota viene utilizzata oppure no.

Però poi mi sono reso conto che questo non funzionerebbe, perché se usiamo una banconota per la risoluzione di un sottoproblema, questo non significa necessariamente che quella banconota sarà anche utilizzata nella soluzione ottima finale.

Dopo aver perso un po' di tempo, anche perché la soluzione ufficiale usa un array del tipo $B[0..n]$, ho scelto di optare per una scelta più sicura secondo me.

Ovvero, uso una tabella $B[0..s, 0..n]$, dove $B[sPrime,j]$ indica tramite un valore booleano se la banconota `b_j` viene usata nella soluzione ottima del sottoproblema di somma `sPrime` con le prime `j` banconote.

Dopodiché, possiamo passare questa tabella a una procedura ricorsiva per la stampa della soluzione ottima trovata.

La procedura `printBanconote(sPrime,j,v,B)` stampa la soluzione ottima trovata solo nel caso in cui questa sia effettivamente possibile, ovvero solo nel caso in cui la soluzione ottima finale trovata sia tale che $C[s,n] \ne +\infty$.

La stampa della soluzione si ferma al caso base in cui la somma è pari a `0`, oppure procede in modo ricorsivo seguendo le scelte salvate nella tabella `B`.

```text
initBanconote(s, v, n)

    // allocazione tabelle
    allocate C[0..s, 0..n]
    allocate B[0..s, 0..n]

    // riempimento iniziale
    for sPrime = 0 to s
        for j = 0 to n
            C[sPrime,j] = -1
            B[sPrime,j] = false

    // calcolo soluzione ottima
    C[s,n] = banconoteRec(s, v, n, C, B)

    // guard: stampa soluzione solo se non impossibile
    if C[s,n] != +∞
        printBanconote(s, n, v, B)

    // restituisco anche il costo della soluzione
    return C[s,n]


// procedura ricorsiva
banconoteRec(sPrime, v, j, C, B)

    if C[sPrime,j] == -1

        if sPrime == 0
            C[sPrime,j] = 0

        else if j == 0
            C[sPrime,j] = +∞

        // separo i casi per facilitare il tracciamento in B
        else if v[j] <= sPrime
            used = 1 + banconoteRec(sPrime - v[j], v, j-1, C, B)
            notUsed = banconoteRec(sPrime, v, j-1, C, B)

            if used < notUsed
                C[sPrime,j] = used
                B[sPrime,j] = true
            else
                C[sPrime,j] = notUsed

        else
            C[sPrime,j] = banconoteRec(sPrime, v, j-1, C, B)

    return C[sPrime,j]


// procedura per la stampa
printBanconote(sPrime, j, v, B)

    // se somma pari a 0
    if sPrime == 0
        return

    // se non abbiamo più banconote
    // per il guard C[s,n] != +∞ questo caso non dovrebbe accadere
    else if j == 0
        return

    // se abbiamo usato la banconota b_j
    else if B[sPrime,j] == true
        print v[j]
        return printBanconote(sPrime - v[j], j-1, v, B)

    // altrimenti, se non l'abbiamo usata
    else
        return printBanconote(sPrime, j-1, v, B)
```

## Complessità

Per quanto riguarda il punto **iv**, la complessità temporale è data dal numero di stati della tabella $C[0..s, 0..n]$.

Ogni stato viene calcolato al massimo una volta e ogni calcolo richiede tempo costante, quindi la complessità temporale complessiva è:

$$
O(s \times n)
$$

La procedura di stampa richiede tempo al più lineare nel numero di banconote considerate, quindi viene assorbita dal costo della tabella.

Per quanto riguarda lo spazio usato, anche questo è:

$$
O(s \times n)
$$

per l'uso delle tabelle $C[0..s, 0..n]$ e $B[0..s, 0..n]$.

Inoltre, viene allocata memoria ulteriore sullo stack per la chiamata di stampa ricorsiva, ma questa si può assorbire nel costo dato dalle due tabelle.

Quindi anche la complessità spaziale complessiva risulta essere:

$$
O(s \times n)
$$
