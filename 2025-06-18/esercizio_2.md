# Esercizio 2 — Scheduling greedy e somma dei tempi di completamento

[← Torna all'appello](README.md)

## Testo

**Esercizio 2 (10 punti)**

Abbiamo $n$ programmi da eseguire sul nostro computer. Ogni programma $j$, con:

```math
j \in \{1,2,\ldots,n\},
```

ha lunghezza $\ell_j$, che rappresenta la quantità di tempo richiesta per la sua
esecuzione.

Dato un ordine di esecuzione:

```math
\sigma = j_1,j_2,\ldots,j_n
```

dei programmi, cioè una permutazione di $\{1,2,\ldots,n\}$, il tempo di
completamento $C_{j_i}(\sigma)$ del programma $j_i$ è dato dalla somma delle
lunghezze dei programmi:

```math
j_1,j_2,\ldots,j_i.
```

L'obiettivo è trovare un ordine di esecuzione $\sigma$ che minimizza la somma dei
tempi di completamento di tutti i programmi, cioè:

```math
\sum_{j=1}^{n} C_j(\sigma).
```

### Punto (a)

Dare un semplice algoritmo greedy per questo problema, e valutarne la
complessità.

### Punto (b)

Dimostrare la proprietà di scelta greedy dell'algoritmo del punto (a), cioè che
esiste un ordine di esecuzione ottimo $\sigma^\star$ che contiene la scelta
greedy.

---

## Soluzione

## Punto (a)

La scelta greedy consiste nell'eseguire prima il programma di lunghezza minima.

Quindi l'algoritmo ordina i programmi per lunghezza crescente e poi li esegue in
quell'ordine.

Questa regola è nota anche come **Shortest Processing Time first**, cioè SPT.

Se l'ordine ottenuto è:

```math
\ell_{j_1} \le \ell_{j_2} \le \cdots \le \ell_{j_n},
```

allora eseguiamo i programmi nell'ordine:

```math
j_1,j_2,\ldots,j_n.
```

---

## Pseudocodice

```text
SPT-Schedule(l, n)
    allocate P[1..n]

    for i = 1 to n
        P[i] = i

    sort P by increasing value of l[P[i]]

    time = 0
    total = 0

    for i = 1 to n
        j = P[i]
        time = time + l[j]
        total = total + time

    return P, total
```

La complessità dell'algoritmo è dominata dall'ordinamento:

```math
\Theta(n \log n).
```

Dopo l'ordinamento, il calcolo della somma dei tempi di completamento richiede
solo una scansione lineare, quindi $\Theta(n)$.

La complessità totale è quindi:

```math
\Theta(n \log n).
```

Se i programmi fossero già ordinati per lunghezza crescente, allora la
complessità sarebbe:

```math
\Theta(n).
```

---

## Punto (b): proprietà di scelta greedy

Dobbiamo dimostrare che esiste un ordine ottimo che esegue per primo un
programma di lunghezza minima.

Sia $a$ un programma di lunghezza minima, cioè:

```math
\ell_a \le \ell_j
```

per ogni altro programma $j$.

Vogliamo dimostrare che esiste una soluzione ottima in cui $a$ è il primo
programma.

Sia $\sigma^\star$ un ordine ottimo.

Se $\sigma^\star$ ha già $a$ in prima posizione, allora abbiamo finito.

Supponiamo invece che $a$ non sia in prima posizione. Allora, nell'ordine
$\sigma^\star$, consideriamo il programma $b$ che si trova immediatamente prima
di $a$.

Poiché $a$ ha lunghezza minima, vale:

```math
\ell_a \le \ell_b.
```

Consideriamo solo questi due programmi consecutivi e supponiamo che prima di
loro sia già passato un tempo totale $T$.

### Ordine prima dello scambio: `b, a`

Il contributo di questi due programmi alla somma dei tempi di completamento è:

```math
(T+\ell_b)+(T+\ell_b+\ell_a)
=
2T+2\ell_b+\ell_a.
```

### Ordine dopo lo scambio: `a, b`

Il contributo diventa:

```math
(T+\ell_a)+(T+\ell_a+\ell_b)
=
2T+2\ell_a+\ell_b.
```

### Confronto

La differenza tra il costo prima dello scambio e il costo dopo lo scambio è:

```math
(2T+2\ell_b+\ell_a)-(2T+2\ell_a+\ell_b)
=
\ell_b-\ell_a.
```

Poiché $\ell_b \ge \ell_a$, questa differenza è non negativa.

Quindi scambiare `b, a` in `a, b` non aumenta il costo totale.

Ripetendo questo scambio, possiamo spostare $a$ una posizione alla volta verso
sinistra, fino a portarlo in prima posizione, senza aumentare il costo.

Poiché $\sigma^\star$ era ottimo, il nuovo ordine ottenuto è ancora ottimo.

Quindi esiste un ordine ottimo che contiene la scelta greedy, cioè che esegue
per primo un programma di lunghezza minima.
