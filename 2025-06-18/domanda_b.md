# Domanda B — Codifica di Huffman

[← Torna all'appello](README.md)

## Testo

**Domanda B (6 punti)**

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

---

## Soluzione

L'algoritmo di Huffman utilizza un approccio greedy bottom-up per costruire un
codice prefisso ottimo.

Si usa una coda con priorità $Q$, solitamente implementata tramite un min-heap.

Inizialmente, ogni simbolo dell'alfabeto viene inserito in $Q$ come nodo foglia,
con priorità uguale alla sua frequenza.

Finché in $Q$ rimane più di un nodo, si estraggono i due nodi con frequenza
minima, si crea un nuovo nodo interno con frequenza uguale alla somma delle due
frequenze estratte, e si reinserisce questo nuovo nodo in $Q$.

Quando rimane un solo nodo, quello è la radice dell'albero di Huffman.

---

## Costruzione

Ordiniamo i simboli per frequenza crescente:

| Simbolo | Frequenza |
|---|---:|
| b | 7 |
| e | 10 |
| a | 12 |
| c | 14 |
| f | 27 |
| d | 30 |

Le fusioni effettuate dall'algoritmo sono:

```text
7 + 10 = 17
12 + 14 = 26
17 + 26 = 43
27 + 30 = 57
43 + 57 = 100
```

Quindi l'evoluzione della coda con priorità è:

```text
Q = {(b:7), (e:10), (a:12), (c:14), (f:27), (d:30)}
Q = {(a:12), (c:14), (17), (f:27), (d:30)}
Q = {(17), (26), (f:27), (d:30)}
Q = {(f:27), (d:30), (43)}
Q = {(43), (57)}
Q = {(100)}
```

---

## Albero ottenuto

Scegliendo la convenzione:

```text
sinistra = 0
destra   = 1
```

otteniamo, ad esempio, il seguente albero:

```text
                         (100)
                       /       \
                    (43)       (57)
                   /    \      /   \
                (17)   (26) (f:27) (d:30)
                / \    /  \
             (b:7)(e:10)(a:12)(c:14)
```

Da questo albero si ottengono i seguenti codici:

| Simbolo | Codice |
|---|---|
| a | 010 |
| b | 000 |
| c | 011 |
| d | 11 |
| e | 001 |
| f | 10 |

Il codice non è unico: scambiando sinistra e destra in uno o più nodi interni si
ottengono codici diversi ma equivalenti.
