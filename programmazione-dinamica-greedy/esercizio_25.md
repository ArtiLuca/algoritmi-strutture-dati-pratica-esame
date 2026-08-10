# Esercizio 25 — Lunghezza esatta annodando pezzi di corda

## Traccia

Un marinaio ha $n$ pezzi di corda di lunghezze intere $l_1, \dots, l_n$, con $l_i \ge 2$, e deve annodarli per ottenere una corda di lunghezza esattamente $d$.

Tenendo conto che fare un nodo richiede una lunghezza pari ad `1`, ad esempio se annodo due pezzi lunghi `5` e `7` la corda che ottengo è lunga `11`, individuare, se esiste, un insieme minimo di pezzi che annodati producano una corda della lunghezza $d$ desiderata.

Più precisamente:

- **i.** dare una caratterizzazione ricorsiva del numero minimo $m(i,d')$ di pezzi di corda scelti in $l_1, \dots, l_i$ che possono essere annodati per produrre la lunghezza $d'$ ($+\infty$ se non è possibile ottenere $d'$ con nessuna combinazione);
- **ii.** usare la caratterizzazione al punto precedente per ottenere un algoritmo `Rope(l,n,d)` che dato l'array delle lunghezze `l[1..n]` determina il numero minimo di pezzi da annodare per ottenere $d$ (se esiste);
- **iii.** trasformare l'algoritmo in modo che restituisca oltre al numero anche l'indicazione di quali pezzi usare;
- **iv.** valutare la complessità dell'algoritmo.

## Idea

Per il punto **i** posso iniziare definendo $m(i,d')$ come il numero minimo di pezzi di corda tra $l_1, \dots, l_i$ che possono essere annodati per produrre una corda di lunghezza esattamente pari a $d'$.

Possiamo fare delle osservazioni per poi darne una caratterizzazione ricorsiva.

- Se $i=0$, allora non abbiamo pezzi di corda e dunque il problema non ammette soluzione. Quindi in questo caso si usa un valore sentinella $m(i,d') = +\infty$.
- Se consideriamo il pezzo di corda $i$ e abbiamo che $l_i = d'$, allora serve solamente un pezzo di corda per risolvere il problema e quindi $m(i,d') = 1$.
- Se consideriamo un pezzo di corda $i$ compatibile, ovvero tale che $l_i < d'$, allora dobbiamo valutare cosa ci conviene fare: usarlo oppure no.
- Se non usiamo il pezzo di corda $l_i$, allora rimangono $i-1$ pezzi per risolvere lo stesso problema di lunghezza $d'$, cioè otteniamo $m(i-1,d')$.
- Se invece usiamo il pezzo $l_i$, allora rimangono $i-1$ pezzi di corda per risolvere il problema ora di lunghezza $d' - l_i + 1$, dove si aggiunge `+1` per tenere conto del costo del nodo. Inoltre, avendo usato un pezzo di corda, dobbiamo anche aggiungere `+1` al numero di pezzi utilizzati.
- Se invece il pezzo di corda $i$ non è compatibile, ovvero abbiamo $l_i > d'$, allora non possiamo usarlo e quindi rimangono $i-1$ pezzi per risolvere lo stesso problema di lunghezza $d'$.

## Caratterizzazione ricorsiva

Riassumendo, possiamo definire una ricorrenza per $m(i,d')$ come segue:

$$
m(i,d') =
\begin{cases}
+\infty & \text{se } i=0, \\
1 & \text{se } l_i = d', \\
\min\{1 + m(i-1,d'-l_i+1),\ m(i-1,d')\} & \text{se } l_i \lt d', \\
m(i-1,d') & \text{se } l_i \gt d'.
\end{cases}
$$

Per motivi puramente estetici, utilizzo nelle parti relative allo pseudocodice $d^{*}$ anziché $d'$.

## Algoritmo bottom-up

Per il punto **ii** utilizzo un algoritmo bottom-up per implementare `Rope(l,n,d)` e uso una tabella $M[0..n, 1..d]$.

In particolare, $M[i,d^*]$ corrisponde al numero minimo di pezzi di corda utilizzati tra $l_1, \dots, l_i$ che si possono annodare in modo da ottenere una corda di lunghezza esattamente $d^{*}$.

Il valore di ritorno $M[n,d]$ si interpreta in due modi:

- Se $M[n,d] = +\infty$, allora il problema non ammette soluzione.
- Se $M[n,d]$ è un valore finito, allora questo valore corrisponde al numero minimo di pezzi di corda.

```text
// Algoritmo bottom-up per trovare numero minimo di pezzi di corda
Rope(l, n, d)

    // allocazione tabella
    allocate M[0..n, 1..d]

    // gestisco caso base in cui problema non ammette soluzione
    for d* = 1 to d
        M[0,d*] = +∞

    // riempimento tabella
    for i = 1 to n
        for d* = 1 to d

            // caso in cui mi serve esattamente 1 pezzo di corda
            if l[i] == d*
                M[i,d*] = 1

            // caso in cui ho un pezzo compatibile, prendo il minimo
            else if l[i] < d*
                M[i,d*] = min(
                              1 + M[i-1, d* - l[i] + 1],
                              M[i-1, d*]
                           )

            // altrimenti, pezzo non compatibile
            else
                M[i,d*] = M[i-1, d*]

    return M[n,d]
```

## Ricostruzione della soluzione

Per quanto richiesto dal punto **iii**, se volessimo anche ottenere i pezzi utilizzati nella soluzione ottima trovata, possiamo utilizzare un'ulteriore tabella $P[1..n, 1..d]$.

La tabella $P[i,d']$ indica tramite un valore booleano se il pezzo di corda $l_i$ è stato utilizzato oppure no per la soluzione ottima del sottoproblema relativo a una corda di lunghezza $d'$ usando i primi $i$ pezzi.

Inizialmente tutti i valori di $P[1..n, 1..d]$ sono impostati a `false`.

Possiamo usare questa nuova tabella per stampare i pezzi di corda utilizzati nella soluzione ottima trovata, solo se questa è effettivamente una soluzione ammissibile, ovvero se $M[n,d] \ne +\infty$.

La procedura di stampa `printRope(l,i,d,P)` opera in maniera ricorsiva, stampando i pezzi utilizzati nella soluzione finale trovata e applicando la ricorrenza ricorsivamente.

La stampa si ferma quando non ci sono più pezzi da considerare, oppure quando la lunghezza rimanente è stata completamente ottenuta.

Come prima, utilizzo nello pseudocodice $d^{*}$ anziché $d'$ solamente per motivi estetici.

```text
// commento solo le parti nuove rispetto a prima
Rope(l, n, d)

    allocate M[0..n, 1..d]

    // allocazione nuova tabella
    allocate P[1..n, 1..d]

    for d* = 1 to d
        M[0,d*] = +∞

    for i = 1 to n
        for d* = 1 to d

            // inizialmente tutti i valori di P sono false
            P[i,d*] = false

            // se serve esattamente un pezzo, si salva
            if l[i] == d*
                M[i,d*] = 1
                P[i,d*] = true

            // se il pezzo è compatibile, salvo solo se lo uso
            else if l[i] < d*
                used = 1 + M[i-1, d* - l[i] + 1]
                notUsed = M[i-1, d*]

                if used <= notUsed
                    M[i,d*] = used
                    P[i,d*] = true
                else
                    M[i,d*] = notUsed

            // se il pezzo non è compatibile, non si può usare
            else
                M[i,d*] = M[i-1, d*]

    // solo se ho trovato una soluzione possibile la stampo
    if M[n,d] != +∞
        printRope(l, n, d, P)

    // restituisco la soluzione
    return M[n,d]


// Procedura per stampa soluzione
printRope(l, i, d, P)

    // caso base: fine dei pezzi o lunghezza esaurita
    if i == 0 or d <= 0
        return

    // se ho usato il pezzo l_i
    if P[i,d] == true
        print l[i]

        // se era esattamente il pezzo finale, mi fermo
        if l[i] == d
            return

        // altrimenti continuo sottraendo la lunghezza effettiva, tenendo conto del nodo
        return printRope(l, i-1, d - l[i] + 1, P)

    // se non lo ho usato
    else
        return printRope(l, i-1, d, P)
```

## Complessità

Per il punto **iv**, la complessità temporale è data dai due cicli annidati, ovvero dalla dimensione della tabella $M[0..n, 1..d]$.

La procedura di stampa viene assorbita dal costo dei cicli annidati.

La complessità temporale complessiva è dunque:

$$
O(n \times d)
$$

Per lo spazio ulteriore usato, entrambe le tabelle $M[0..n, 1..d]$ e $P[1..n, 1..d]$ sono:

$$
O(n \times d)
$$

Oltre allo spazio ulteriore sullo stack dovuto alla funzione di stampa ricorsiva, abbiamo che la complessità spaziale complessiva è dovuta alle due tabelle, cioè:

$$
O(n \times d)
$$
