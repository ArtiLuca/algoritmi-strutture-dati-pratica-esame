# Algoritmi e Strutture Dati — Appello del 10 settembre 2025

Questa cartella contiene le mie soluzioni personali all'appello del  
**10 settembre 2025** del corso di Algoritmi e Strutture Dati.

## Fonte

Il testo dell'appello è disponibile nella pagina ufficiale del corso:

```text
https://www.math.unipd.it/~baldan/Algoritmi/Exams/
```

Le soluzioni presenti in questa cartella sono personali e non costituiscono
materiale ufficiale del corso.

## Stato delle soluzioni

| Problema | Argomento principale | Stato |
|---|---|---|
| Domanda A | Classe Ω e proprietà asintotiche | [Completata](domanda_a.md) |
| Domanda B | Codifica di Huffman | [Completata](domanda_b.md) |
| Esercizio 1 | Ricerca della chiave più vicina in un ABR | Da completare |
| Esercizio 2 | Memoizzazione e conteggio esatto delle operazioni | Da completare |

---

## Domanda A — Classe Ω

**7 punti**

Dare la definizione formale della classe $\Omega(f(n))$ per una funzione
$f(n)$.

Mostrare che, date due funzioni $f(n)$ e $g(n)$, che si possono assumere
sempre positive, se:

```math
f(n)=\Omega(n^2),
```

allora:

```math
f(n)+g(n)=\Omega(n^2+g(n)).
```

Vale anche:

```math
f(n)-g(n)=\Omega(n^2-g(n))?
```

Dimostrarlo oppure fornire un controesempio.

**[Vai alla soluzione](domanda_a.md)**

---

## Domanda B — Algoritmo di Huffman

**6 punti**

Indicare, in forma di albero binario, il codice prefisso ottenuto tramite
l'algoritmo di Huffman per l'alfabeto:

```math
\{a,b,c,d,e,f\},
```

supponendo che ogni simbolo appaia con le seguenti frequenze:

| Simbolo | a | b | c | d | e | f |
|---|---:|---:|---:|---:|---:|---:|
| Frequenza | 12 | 7 | 14 | 30 | 10 | 27 |

Spiegare brevemente il processo di costruzione del codice.

**[Vai alla soluzione](domanda_b.md)**

---

## Esercizio 1 — Distanza minima in un albero binario di ricerca

**10 punti**

Realizzare una funzione `mdist(T, v)` che, dato un albero binario di ricerca
$T$ e una chiave $v$, restituisca un nodo $x$ di $T$ la cui chiave abbia
distanza minima da $v$, ovvero tale che il valore:

```math
|x.k-v|
```

sia minimo.

Fornire:

- lo pseudocodice;
- l'analisi della complessità;
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

la funzione `mdist(T, 8)` deve restituire il nodo con chiave `9`, mentre
`mdist(T, 28)` deve restituire il nodo con chiave `30`.

**Soluzione da completare.**

---

## Esercizio 2 — Ricorrenza memoizzata

**9 punti**

Sia $n>0$ un intero.

Si consideri la seguente ricorrenza $M(i,j)$, definita per tutte le coppie
$(i,j)$ tali che:

```math
1\le i\le j\le n.
```

La ricorrenza è:

```math
M(i,j)=
\begin{cases}
1
& \text{se } i=j, \\[4pt]
2
& \text{se } j=i+1, \\[4pt]
M(i+1,j-1)\cdot M(i+1,j)\cdot M(i,j-1)
& \text{se } j>i+1.
\end{cases}
```

### Punto (a)

Scrivere una coppia di algoritmi `INIT_M(n)` e `REC_M(i, j)` per il calcolo
memoizzato di:

```math
M(1,n).
```

### Punto (b)

Calcolare il numero esatto $T(n)$ di moltiplicazioni tra interi eseguite
durante il calcolo di:

```math
M(1,n).
```

**Soluzione da completare.**
