# Esercizio 1 — Distanza minima in un albero binario di ricerca

[← Torna all'appello](README.md)

## Testo

**Esercizio 1 (10 punti)**

Realizzare una funzione `mdist(T, v)` che, dato un albero binario di ricerca
$T$ e una chiave $v$, restituisca un nodo $x$ di $T$ la cui chiave abbia
distanza minima da $v$, ovvero tale che il valore:

```math
|x.k-v|
```

sia minimo.

Fornire:

- lo pseudocodice;
- la complessità;
- una giustificazione della correttezza.

Ad esempio, dato il seguente albero:

```text
              10
             /  \
            5    20
           / \   / \
          2   6 15  30
               \    /
                9  25
```

la funzione `mdist(T, 8)` restituisce il nodo con chiave `9`, mentre
`mdist(T, 28)` restituisce il nodo con chiave `30`.

---

## Soluzione

L'idea è sfruttare la proprietà di ordinamento degli alberi binari di ricerca.

Durante una normale ricerca in un ABR, quando ci troviamo in un nodo $x$:

- se $v < x.k$, la ricerca prosegue nel sottoalbero sinistro;
- se $v > x.k$, la ricerca prosegue nel sottoalbero destro;
- se $v = x.k$, abbiamo trovato una distanza pari a `0`, quindi non è possibile
  fare meglio.

Per trovare il nodo con chiave più vicina a $v$, manteniamo un riferimento
`best` al miglior nodo incontrato finora. Ogni volta che visitiamo un nodo,
confrontiamo la sua distanza da $v$ con la distanza del nodo migliore corrente.

Non è necessario visitare tutto l'albero: si può seguire lo stesso cammino di
ricerca che si seguirebbe cercando la chiave $v$.

---

## Pseudocodice

```text
mdist(T, v)
    x = T.root

    if x == NIL
        return NIL

    best = x
    bestDist = |x.k - v|

    while x != NIL
        currentDist = |x.k - v|

        if currentDist < bestDist
            bestDist = currentDist
            best = x

        if x.k == v
            return x

        if v < x.k
            x = x.left
        else
            x = x.right

    return best
```

In caso di due nodi alla stessa distanza minima da $v$, l'algoritmo restituisce
uno dei nodi a distanza minima.

---

## Correttezza

Dimostriamo che l'algoritmo restituisce un nodo la cui chiave ha distanza minima
da $v$.

Durante l'esecuzione, la variabile `best` contiene sempre il miglior nodo tra
quelli già visitati, cioè il nodo visitato con valore minimo di $|x.k-v|$.

Consideriamo un generico nodo $x$ visitato dall'algoritmo.

### Caso 1: $v < x.k$

Per la proprietà degli ABR, tutte le chiavi nel sottoalbero destro di $x$ sono
maggiori o uguali a $x.k$.

Quindi, per ogni nodo $y$ nel sottoalbero destro di $x$:

```math
y.k \ge x.k > v.
```

Di conseguenza:

```math
|y.k-v| = y.k-v \ge x.k-v = |x.k-v|.
```

Poiché il nodo $x$ è già stato considerato, nessun nodo nel sottoalbero destro
può essere migliore del candidato già noto. È quindi corretto scartare il
sottoalbero destro e proseguire a sinistra.

### Caso 2: $v > x.k$

Analogamente, per la proprietà degli ABR, tutte le chiavi nel sottoalbero
sinistro di $x$ sono minori o uguali a $x.k$.

Quindi, per ogni nodo $y$ nel sottoalbero sinistro di $x$:

```math
y.k \le x.k < v.
```

Di conseguenza:

```math
|y.k-v| = v-y.k \ge v-x.k = |x.k-v|.
```

Poiché il nodo $x$ è già stato considerato, nessun nodo nel sottoalbero sinistro
può essere migliore del candidato già noto. È quindi corretto scartare il
sottoalbero sinistro e proseguire a destra.

### Caso 3: $v = x.k$

In questo caso:

```math
|x.k-v|=0.
```

La distanza `0` è la minima possibile, quindi l'algoritmo può restituire
immediatamente il nodo $x$.

---

In ogni passo, l'algoritmo scarta solo sottoalberi che non possono contenere un
nodo migliore del miglior candidato già visitato. Alla fine della visita,
`best` contiene quindi un nodo con distanza minima da $v$.

Se l'albero è vuoto, l'algoritmo restituisce correttamente `NIL`.

---

## Complessità

L'algoritmo segue un solo cammino dalla radice verso una foglia.

Se $h$ è l'altezza dell'albero, il costo temporale è:

```math
O(h).
```

Nel caso di un albero bilanciato:

```math
h = O(\log n),
```

quindi il costo è:

```math
O(\log n).
```

Nel caso peggiore, l'albero può essere degenere e avere altezza:

```math
h = O(n),
```

quindi il costo diventa:

```math
O(n).
```

La complessità spaziale è:

```math
O(1),
```

perché l'algoritmo è iterativo e mantiene solo un numero costante di variabili.
