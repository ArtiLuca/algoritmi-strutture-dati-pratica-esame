# Domanda B — Selezione di attività compatibili

[← Torna all'appello](README.md)

## Testo

**Domanda B (7 punti)**

Si consideri il problema di selezione di attività compatibili:

**(a)** Definire il problema.

**(b)** Descrivere brevemente l'algoritmo ottimo `GREEDY-SEL` visto in classe.

**(c)** Fornire un esempio di algoritmo greedy *non* ottimo, motivandone la non
ottimalità.

---

## Soluzione

## Punto (a)

Il problema della selezione di attività compatibili consiste nel trovare un
sottoinsieme di attività mutuamente compatibili di cardinalità massima.

Sono date $n$ attività $a_1, \dots, a_n$. Ogni attività $a_i$ ha:

- un tempo di inizio $s_i$;
- un tempo di fine $f_i$;

con $s_i < f_i$.

Due attività $a_i$ e $a_j$ sono compatibili se non si sovrappongono, cioè se:

$$ f_i \le s_j $$

oppure:

$$ f_j \le s_i $$

L'obiettivo è selezionare il massimo numero possibile di attività mutuamente
compatibili.

Di solito, per l'algoritmo greedy visto a lezione, si assume che le attività
siano ordinate per tempo di fine crescente:

$$ f_1 \le f_2 \le \dots \le f_n $$

---

## Punto (b)

L'algoritmo `GREEDY-SEL` sceglie sempre l'attività compatibile che termina prima.

L'idea è che scegliere l'attività che finisce prima lascia più spazio possibile
alle attività successive.

Lo pseudocodice è:

```text
GREEDY-SEL(s, f, n)
    A = {a_1}
    last = 1

    for m = 2 to n
        if s[m] >= f[last]
            A = A union {a_m}
            last = m

    return A
```

La complessità è:

$$ \Theta(n) $$

L'algoritmo è corretto perché la scelta dell'attività che termina prima è una
scelta sicura.

Infatti, sia $a_1$ l'attività che termina per prima e sia $OPT$ una soluzione
ottima.

Se $OPT$ contiene già $a_1$, allora va bene.

Altrimenti, sia $a_k$ l'attività di $OPT$ che termina per prima tra quelle
selezionate in $OPT$.

Poiché $a_1$ termina per prima in assoluto, vale:

$$ f_1 \le f_k $$

Possiamo quindi sostituire $a_k$ con $a_1$. La nuova soluzione resta compatibile,
perché $a_1$ termina non più tardi di $a_k$, e ha la stessa cardinalità di
$OPT$.

Quindi esiste una soluzione ottima che contiene $a_1$. Dopo aver scelto $a_1$,
rimane lo stesso problema sulle attività compatibili successive.

---

## Punto (c)

Un esempio di algoritmo greedy non ottimo è:

> scegliere sempre l'attività che inizia prima.

Consideriamo le attività:

| Attività | Inizio | Fine |
|---:|---:|---:|
| $a_1$ | 2 | 4 |
| $a_2$ | 5 | 7 |
| $a_3$ | 8 | 10 |
| $a_4$ | 1 | 12 |
| $a_5$ | 11 | 13 |

L'algoritmo che sceglie sempre l'attività che inizia prima seleziona prima
$a_4$, perché inizia al tempo $1$.

Ma $a_4 = (1, 12)$ si sovrappone con $a_1$, $a_2$, $a_3$ e $a_5$. Quindi la
soluzione ottenuta è:

$$ \{a_4\} $$

di cardinalità $1$.

Invece, una soluzione ottima è:

$$ \{a_1, a_2, a_3, a_5\} $$

di cardinalità $4$.

Quindi la strategia greedy "scegliere sempre l'attività che inizia prima" non è
ottima.
