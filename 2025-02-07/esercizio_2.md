# Esercizio 2 — Selezione di attività compatibili

[← Torna all'appello](README.md)

## Testo

**Esercizio 2 (10 punti)**

Si consideri il problema di selezione di attività compatibili, con $n$ attività
$a_1, \dots, a_n$ che ci vengono date attraverso due vettori $\mathbf{s}$ e $\mathbf{f}$ di
tempi di inizio e fine, e ordinate per tempo di *inizio*, cioè:

$$ 0 < s_1 \le s_2 \le \dots \le s_n $$

**(a)** Scrivere un algoritmo greedy iterativo che implementa la scelta greedy
di selezionare l'attività che inizia per ultima.

**(b)** Determinare l'insieme di attività restituito dall'algoritmo al punto
(a) quando eseguito sul seguente insieme di 6 attività, caratterizzate dai
seguenti vettori $\mathbf{s}$ e $\mathbf{f}$ di tempi di inizio e fine:

$$ \mathbf{s} = (1, 2, 3, 5, 7, 10) $$
$$ \mathbf{f} = (3, 9, 10, 7, 11, 12) $$

**(c)** Dimostrare la proprietà di scelta greedy, cioè che esiste soluzione
ottima che contiene l'attività che inizia per ultima.

---

## Soluzione

## Punto (a)

La scelta greedy richiesta consiste nel selezionare per prima l'attività che
inizia per ultima.

Poiché le attività sono ordinate per tempo di inizio crescente, cioè:

$$ s_1 \le s_2 \le \dots \le s_n $$

l'attività che inizia per ultima è $a_n$.

Dopo aver scelto $a_n$, scorriamo le attività all'indietro. Una nuova attività
$a_m$ è compatibile con l'ultima attività scelta se termina non oltre l'inizio
di quest'ultima, cioè se:

$$ f_m \le s_{\text{last}} $$

## Pseudocodice

```text
Greedy-Sel-Last(s, f, n)
    A = {a_n}
    last = n

    for m = n - 1 downto 1
        if f[m] <= s[last]
            A = A union {a_m}
            last = m

    return A
```

L'algoritmo restituisce le attività nell'ordine in cui vengono selezionate,
cioè dalla più tarda alla più precoce. Se si vuole l'ordine cronologico, basta
leggere il risultato al contrario.

---

## Punto (b)

I vettori sono:

$$ \mathbf{s} = (1, 2, 3, 5, 7, 10) $$
$$ \mathbf{f} = (3, 9, 10, 7, 11, 12) $$

Quindi le attività sono:

- $a_1 = [1, 3)$
- $a_2 = [2, 9)$
- $a_3 = [3, 10)$
- $a_4 = [5, 7)$
- $a_5 = [7, 11)$
- $a_6 = [10, 12)$

L'algoritmo procede da destra verso sinistra.

1. Sceglie inizialmente $a_6$, perché è l'attività che inizia per ultima.

   Quindi $A = \{a_6\}$ e `last` $= 6$.

2. Considera $a_5$.

   Poiché $f_5 = 11 > 10 = s_6$, l'attività $a_5$ non è compatibile con $a_6$
   e non viene scelta.

3. Considera $a_4$.

   Poiché $f_4 = 7 \le 10 = s_6$, l'attività $a_4$ viene scelta.

   Quindi $A = \{a_6, a_4\}$ e `last` $= 4$.

4. Considera $a_3$.

   Poiché $f_3 = 10 > 5 = s_4$, l'attività $a_3$ non viene scelta.

5. Considera $a_2$.

   Poiché $f_2 = 9 > 5 = s_4$, l'attività $a_2$ non viene scelta.

6. Considera $a_1$.

   Poiché $f_1 = 3 \le 5 = s_4$, l'attività $a_1$ viene scelta.

Il risultato, nell'ordine di selezione dell'algoritmo, è:

$$ A = \{a_6, a_4, a_1\} $$

In ordine cronologico, lo stesso insieme è:

$$ \{a_1, a_4, a_6\} $$

---

## Punto (c)

Dobbiamo dimostrare che esiste una soluzione ottima che contiene l'attività che
inizia per ultima.

Sia $a_m$ l'attività che inizia per ultima. Poiché le attività sono ordinate per
tempo di inizio crescente, possiamo prendere:

$$ a_m = a_n $$

Sia $OPT$ una soluzione ottima, cioè un insieme di cardinalità massima di
attività mutuamente compatibili.

Se $OPT$ contiene già $a_m$, allora la proprietà è dimostrata.

Supponiamo invece che $OPT$ non contenga $a_m$.

Sia $a_k$ l'attività di $OPT$ che inizia più tardi tra tutte le attività
contenute in $OPT$.

Poiché $a_m$ è l'attività che inizia più tardi tra tutte le attività dell'input,
vale:

$$ s_k \le s_m $$

Consideriamo ora una qualsiasi altra attività $a_i$ appartenente a $OPT$, con:

$$ a_i \ne a_k $$

Poiché $a_k$ è l'attività che inizia più tardi in $OPT$ e le attività di $OPT$
sono compatibili, l'attività $a_i$ deve terminare non oltre l'inizio di $a_k$,
cioè:

$$ f_i \le s_k $$

Dato che $s_k \le s_m$, otteniamo:

$$ f_i \le s_m $$

Quindi ogni attività di $OPT$ diversa da $a_k$ è compatibile anche con $a_m$.

Possiamo allora costruire il nuovo insieme:

$$ OPT' = OPT \setminus \{a_k\} \cup \{a_m\} $$

L'insieme $OPT'$ è ancora formato da attività mutuamente compatibili, ha la
stessa cardinalità di $OPT$ e contiene $a_m$.

Poiché $OPT$ era ottima e $|OPT'| = |OPT|$, anche $OPT'$ è ottima.

Dunque esiste una soluzione ottima che contiene l'attività che inizia per
ultima. Questo dimostra la proprietà di scelta greedy.
