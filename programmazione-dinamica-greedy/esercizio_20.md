# Esercizio 20 — Shortest Common Supersequence (SCS)

## Traccia

Si ricordi che data una sequenza $X = x_1 \dots x_k$ si indica con $X_i$ il prefisso $x_1 \dots x_i$.

Una sottosequenza di $X$ è $x_{i_1} \dots x_{i_h}$ con $1 \le i_1 < i_2 < \dots < i_h \le k$, ovvero è una sequenza ottenuta da $X$ eliminando alcuni elementi.

Quando $Y$ è sottosequenza di $X$ si scrive $Y \sqsubseteq X$.

Realizzare un algoritmo che, date due sequenze $X = x_1 \dots x_k$ e $Y = y_1 \dots y_h$, determina una *shortest common supersequence* (SCS), ovvero una sequenza $Z$, di lunghezza minima, tale che sia $X \sqsubseteq Z$ che $Y \sqsubseteq Z$.

Ad esempio, per `X = "abf"` e `Y = "afgj"` una SCS è `"abfgj"`.

Più precisamente:

- **i.** dare una caratterizzazione ricorsiva della lunghezza $l_{i,j}$ di una SCS di $X_i$ e $Y_j$ e dedurne un algoritmo;
- **ii.** trasformare l'algoritmo in modo che fornisca una SCS di $X$ e $Y$;
- **iii.** valutare la complessità dell'algoritmo.

## Ripasso preliminare: Longest Common Subsequence

Prima di risolvere questo esercizio, ho pensato che sarebbe stato utile un ripasso sul problema della *Longest Common Subsequence* (LCS), in quanto è uscito come domanda d'esame a cui non sapevo rispondere bene:

| Domanda | Argomento | Link |
|---|---|---|
| Domanda B | Ricorrenza per Longest Common Subsequence (LCS) | [Domanda B Esame 2026-07-14](../2026-07-14/domanda_b.md) |

Inoltre, il problema della *Shortest Common Supersequence* (SCS) è molto collegato al problema della LCS.

Non è esattamente lo stesso problema con `min` al posto di `max`, ma la struttura della ricorrenza è simile: nella LCS si cerca di massimizzare una sottosequenza comune, mentre nella SCS si cerca di minimizzare una supersequenza che contenga entrambe le sequenze.

### Definizione di LCS

Date due stringhe:

$$
X = \langle x_1,\dots,x_m \rangle
\qquad
Y = \langle y_1,\dots,y_n \rangle
$$

la LCS di $X$ e $Y$ è una sottosequenza che soddisfa le seguenti due condizioni:

1. $Z$ è sottosequenza di $X$ e anche di $Y$;
2. $Z$ è la sottosequenza più lunga tra tutte le sottosequenze comuni.

Possiamo definire $\ell(i,j) = |LCS(X_i,Y_j)|$ come segue:

$$
\ell(i,j) =
\begin{cases}
0 & \text{se } i=0 \text{ oppure } j=0, \\
1 + \ell(i-1,j-1) & \text{se } i,j \gt 0 \text{ e } x_i = y_j, \\
\max\{\ell(i,j-1), \ell(i-1,j)\} & \text{se } i,j \gt 0 \text{ e } x_i \ne y_j.
\end{cases}
$$

Come visto a lezione, possiamo usare una tabella bidimensionale $L[i,j]$ per memorizzare i vari stati della ricorrenza $\ell(i,j)$ e anche una struttura dati ausiliaria $B[i,j]$ per ricostruire la sottosequenza massima trovata.

In particolare, la tabella `B` memorizza i seguenti casi:

$$
B[i,j] =
\begin{cases}
\text{↖} & \text{se } x_i = y_j, \\
\text{←} & \text{se } x_i \ne y_j \text{ e il massimo viene da } \ell(i,j-1), \\
\text{↑} & \text{se } x_i \ne y_j \text{ e il massimo viene da } \ell(i-1,j).
\end{cases}
$$

Dopodiché possiamo implementare il calcolo bottom-up e anche la ricostruzione della sottosequenza massima trovata usando i due algoritmi `computeLCS(X,Y)` e `printLCS(X,B,i,j)`:

```text
computeLCS(X, Y)
    m = length(X)
    n = length(Y)

    allocate L[0..m, 0..n]
    allocate B[1..m, 1..n]

    for i = 0 to m
        L[i,0] = 0

    for j = 1 to n
        L[0,j] = 0

    // scansione row-major
    for i = 1 to m
        for j = 1 to n

            if X[i] == Y[j]
                L[i,j] = 1 + L[i-1,j-1]
                B[i,j] = '↖'

            else if L[i-1,j] >= L[i,j-1]
                L[i,j] = L[i-1,j]
                B[i,j] = '↑'

            else
                L[i,j] = L[i,j-1]
                B[i,j] = '←'

    // stampa della LCS trovata
    printLCS(X, B, m, n)

    // restituisco lunghezza della LCS trovata
    return L[m,n]


printLCS(X, B, i, j)
    if i == 0 or j == 0
        // restituisco ε per indicare sottosequenza vuota
        return ε

    if B[i,j] == '↖'
        printLCS(X, B, i-1, j-1)
        print X[i]

    else if B[i,j] == '←'
        printLCS(X, B, i, j-1)

    else
        printLCS(X, B, i-1, j)
```

La complessità di `computeLCS` è:

$$
\Theta(m \times n)
$$

quindi al più quadratica rispetto alla lunghezza delle due sequenze.

La complessità di `printLCS` è:

$$
O(m+n)
$$

poiché ad ogni chiamata ricorsiva la somma dei due indici $i + j$ diminuisce di almeno 1.

### Versione memoizzata

Una soluzione equivalente è l'approccio top-down con memoization.

La procedura di inizializzazione e la routine ricorsiva vengono mostrate sotto:

```text
initLCS(X, Y)
    m = length(X)
    n = length(Y)

    if m == 0 or n == 0
        return 0

    allocate L[0..m, 0..n]

    for i = 0 to m
        L[i,0] = 0

    for j = 1 to n
        L[0,j] = 0

    for i = 1 to m
        for j = 1 to n
            // imposto con valore di default
            L[i,j] = -1

    return memoLCS(X, Y, m, n)


memoLCS(X, Y, i, j)
    if L[i,j] == -1

        if X[i] == Y[j]
            L[i,j] = memoLCS(X, Y, i-1, j-1) + 1

        else
            val_up = memoLCS(X, Y, i-1, j)
            val_left = memoLCS(X, Y, i, j-1)

            if val_up >= val_left
                L[i,j] = val_up
            else
                L[i,j] = val_left

    return L[i,j]
```

Con l'approccio memoizzato la complessità risulta ancora:

$$
O(m \times n)
$$

perché ogni sottoproblema $L[i,j]$ viene calcolato al massimo una volta.

### Esempio: `spanking` e `amputation`

Un esempio concreto preso dal corso è la seguente domanda:

> Calcola la LCS tra `spanking` e `amputation`, calcolando solo la tabella $L[i,j]$ delle lunghezze.

Seguendo gli algoritmi mostrati sopra, si ottiene la tabella che segue:

```text
    a m p u t a t i o n
  0 0 0 0 0 0 0 0 0 0 0
s 0 0 0 0 0 0 0 0 0 0 0
p 0 0 0 1 1 1 1 1 1 1 1
a 0 1 1 1 1 1 2 2 2 2 2
n 0 1 1 1 1 1 2 2 2 2 3
k 0 1 1 1 1 1 2 2 2 2 3
i 0 1 1 1 1 1 2 2 3 3 3
n 0 1 1 1 1 1 2 2 3 3 4
g 0 1 1 1 1 1 2 2 3 3 4
```

---

## Idea per la Shortest Common Supersequence

Ora torniamo al nostro esercizio 20 sulla *Shortest Common Supersequence* (SCS).

Il problema è analogo alla LCS nel senso che anche qui ragioniamo sui prefissi delle due sequenze e usiamo una tabella bidimensionale.

La differenza è che:

- Nel problema della LCS stiamo cercando una sottosequenza comune di lunghezza massima. Quindi vogliamo scartare caratteri che non compaiono in entrambe le stringhe e massimizzare la lunghezza valutando se conviene scartare da una stringa o dall'altra.
- Nel problema della SCS invece stiamo cercando una supersequenza di lunghezza minima che contenga tutti i caratteri di entrambe le sequenze. Quindi, se troviamo due caratteri uguali, li possiamo usare una sola volta nella SCS. Se invece i caratteri sono diversi, dobbiamo scegliere da quale sequenza prendere il prossimo carattere, aumentando la lunghezza di 1.

Quindi, riprendendo il testo dell'esercizio, date due stringhe:

$$
X = \langle x_1,\dots,x_k \rangle
\qquad
Y = \langle y_1,\dots,y_h \rangle
$$

possiamo definire $\ell(i,j)$ come la lunghezza di una SCS dei prefissi $X_i$ e $Y_j$, ovvero di:

$$
X_i = \langle x_1,\dots,x_i \rangle
\qquad
Y_j = \langle y_1,\dots,y_j \rangle
$$

con $0 \le i \le k$ e $0 \le j \le h$.

Possiamo dare una caratterizzazione ricorsiva in base alle seguenti osservazioni:

- Se $i = 0$, allora abbiamo esaurito i caratteri di $X$. Quindi l'unica cosa da fare è prendere tutti i `j` caratteri rimanenti di $Y$, e si ha $\ell(i,j) = j$.
- In modo analogo, se $j = 0$, allora abbiamo esaurito i caratteri di $Y$. Quindi l'unica cosa da fare è prendere tutti gli `i` caratteri rimanenti di $X$, e si ha $\ell(i,j) = i$.
- Se invece $i,j > 0$ e abbiamo che $X[i] == Y[j]$, allora possiamo usare quel carattere una sola volta nella SCS e consumare entrambi i caratteri. Quindi si ha $\ell(i,j) = 1 + \ell(i-1,j-1)$.
- Altrimenti, se $i,j > 0$ e $X[i] \ne Y[j]$, allora bisogna consumare un carattere da una delle due sequenze. In questo caso vogliamo minimizzare la scelta tra prendere il prossimo carattere da $X$ oppure da $Y$.

## Caratterizzazione ricorsiva

Riassumendo, possiamo definire $\ell(i,j)$ come segue:

$$
\ell(i,j) =
\begin{cases}
i & \text{se } j=0, \\
j & \text{se } i=0, \\
1 + \ell(i-1,j-1) & \text{se } i,j \gt 0 \text{ e } x_i = y_j, \\
1 + \min\{\ell(i,j-1), \ell(i-1,j)\} & \text{se } i,j \gt 0 \text{ e } x_i \ne y_j.
\end{cases}
$$

## Algoritmo bottom-up

Per il punto **i** e il punto **ii** possiamo usare un algoritmo bottom-up che usa la tabella $L[0\dots k, 0\dots h]$, dove $L[i,j]$ indica la lunghezza minima di una SCS per i prefissi $X_i$ e $Y_j$.

```text
computeSCS(X, Y)
    k = length(X)
    h = length(Y)

    // allocazione tabella
    allocate L[0..k, 0..h]

    // casi base
    for i = 0 to k
        L[i,0] = i

    for j = 1 to h
        L[0,j] = j

    // riempimento bottom-up
    for i = 1 to k
        for j = 1 to h

            if X[i] == Y[j]
                L[i,j] = 1 + L[i-1,j-1]

            else
                L[i,j] = 1 + min(L[i-1,j], L[i,j-1])

    return L[k,h]
```

## Ricostruzione di una SCS

Per quanto riguarda il punto **ii**, se volessimo anche ricostruire la supersequenza trovata, possiamo modificare lo pseudocodice precedente in modo che usi anche una tabella $B[1\dots k, 1\dots h]$ che memorizza le scelte effettuate durante la ricerca.

Ovvero:

- salviamo in $B[i,j]$ il valore $"xy"$ quando troviamo due caratteri uguali;
- salviamo in $B[i,j]$ il valore $"x"$ quando scegliamo di consumare un carattere del prefisso $X_i$;
- salviamo in $B[i,j]$ il valore $"y"$ quando scegliamo di consumare un carattere del prefisso $Y_j$.

Dopodiché, possiamo passare $B$ come parametro in una procedura di stampa `printSCS(X,Y,i,j,B)`, che stampa le nostre scelte seguendo la definizione della ricorrenza.

```text
computeSCS(X, Y)
    k = length(X)
    h = length(Y)

    // allocazione tabelle
    allocate L[0..k, 0..h]
    allocate B[1..k, 1..h]

    // casi base
    for i = 0 to k
        L[i,0] = i

    for j = 1 to h
        L[0,j] = j

    // riempimento bottom-up, con tracciamento della supersequenza
    for i = 1 to k
        for j = 1 to h

            // caso di due caratteri uguali
            if X[i] == Y[j]
                L[i,j] = 1 + L[i-1,j-1]
                B[i,j] = "xy"

            // caso in cui consumo un carattere da X
            else if L[i-1,j] <= L[i,j-1]
                L[i,j] = 1 + L[i-1,j]
                B[i,j] = "x"

            // caso in cui consumo un carattere da Y
            else
                L[i,j] = 1 + L[i,j-1]
                B[i,j] = "y"

    // stampo la supersequenza trovata
    printSCS(X, Y, k, h, B)

    return L[k,h]


printSCS(X, Y, i, j, B)

    // prima gestisco i casi base
    if i == 0
        for t = 1 to j
            print Y[t]
        return

    else if j == 0
        for t = 1 to i
            print X[t]
        return

    // altrimenti seguo la tabella B
    else

        // se ho trovato un carattere uguale per entrambi
        if B[i,j] == "xy"
            printSCS(X, Y, i-1, j-1, B)
            print X[i]

        // se ho esteso usando X
        else if B[i,j] == "x"
            printSCS(X, Y, i-1, j, B)
            print X[i]

        // altrimenti ho esteso usando Y
        else
            printSCS(X, Y, i, j-1, B)
            print Y[j]
```

## Complessità

Per il punto **iii**, la complessità temporale è data dal riempimento della tabella $L[0\dots k, 0\dots h]$.

Ogni cella viene calcolata una sola volta e ogni calcolo richiede tempo costante, quindi la complessità temporale è:

$$
\Theta(k \times h)
$$

La procedura di stampa della SCS richiede tempo lineare nella lunghezza della supersequenza stampata. Nel caso peggiore, questa lunghezza può essere:

$$
O(k+h)
$$

quindi viene assorbita dal costo del riempimento della tabella.

La complessità temporale complessiva rimane quindi:

$$
\Theta(k \times h)
$$

Per quanto riguarda la complessità spaziale, usiamo la tabella $L[0\dots k, 0\dots h]$.

Se vogliamo anche ricostruire una SCS, usiamo anche la tabella $B[1\dots k, 1\dots h]$.

Entrambe le tabelle hanno dimensione proporzionale a $k × h$, quindi la complessità spaziale complessiva è:

$$
\Theta(k \times h)
$$
