# Algoritmi e Strutture Dati — Appello del 18 giugno 2025

Questa cartella contiene le mie soluzioni personali all'appello del  
**18 giugno 2025** del corso di Algoritmi e Strutture Dati.

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
| Domanda A | Classi asintotiche O e Ω | [Completata](domanda_a.md) |
| Domanda B | Codifica di Huffman | [Completata](domanda_b.md) |
| Esercizio 1 | Alberi binari di ricerca arricchiti | [Completata](esercizio_1.md) |
| Esercizio 2 | Scheduling greedy e tempi di completamento | [Completata](esercizio_2.md) |

---

## Domanda A — Classi O e Ω

**7 punti**

Dare la definizione formale delle classi $O(f(n))$ e $\Omega(f(n))$ per una
funzione $f(n)$.

Mostrare che se:

```math
f(n)=O(n)
```

e:

```math
g(n)=n^2-f(n),
```

allora:

```math
g(n)=\Omega(n^2).
```

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

## Esercizio 1 — Albero binario di ricerca arricchito

**9 punti**

Realizzare un arricchimento degli alberi binari di ricerca che permetta di
ottenere per ogni nodo $x$, in tempo costante, il numero delle foglie nel
sottoalbero radicato in $x$.

Indicare quali campi occorre aggiungere ai nodi.

Fornire il codice per la funzione `leaves(x)` che restituisce il numero delle
foglie nel sottoalbero radicato in $x$ e per la procedura di inserimento di un
nodo `insert(T, z)`.

Per entrambe valutare la complessità.

**[Vai alla soluzione](esercizio_1.md)**

---

## Esercizio 2 — Scheduling greedy

**10 punti**

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

**[Vai alla soluzione](esercizio_2.md)**
