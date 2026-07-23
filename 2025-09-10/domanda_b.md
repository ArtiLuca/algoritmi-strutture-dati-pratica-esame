# Domanda B — Algoritmo di Huffman

[← Torna all'appello](README.md)

## Testo

**Domanda B (6 punti)**

Indicare, in forma di albero binario, il codice prefisso ottenuto tramite
l'algoritmo di Huffman per l'alfabeto:

$$
\{a,b,c,d,e,f\},
$$

supponendo che ogni simbolo appaia con le seguenti frequenze:

| Simbolo | a | b | c | d | e | f |
|---|---:|---:|---:|---:|---:|---:|
| Frequenza | 12 | 7 | 14 | 30 | 10 | 27 |

Spiegare brevemente il processo di costruzione del codice.

---

## Soluzione

L'algoritmo di Huffman costruisce un codice prefisso ottimo tramite un approccio
greedy bottom-up.

Inizialmente, ogni simbolo dell'alfabeto viene rappresentato da un nodo foglia
avente come priorità la propria frequenza.

I nodi vengono inseriti in una coda con priorità minima $Q$, generalmente
implementata tramite un min-heap.

Finché nella coda rimane più di un nodo:

1. si estraggono i due nodi con frequenza minima;
2. si crea un nuovo nodo interno avente frequenza pari alla somma delle due
   frequenze;
3. i due nodi estratti diventano figli del nuovo nodo;
4. il nuovo nodo viene reinserito nella coda.

Quando rimane un solo nodo, esso rappresenta la radice dell'albero di Huffman.

---

## Costruzione dell'albero

Ordiniamo inizialmente i simboli per frequenza crescente:

$$
(b:7),\ (e:10),\ (a:12),\ (c:14),\ (f:27),\ (d:30).
$$

Le combinazioni effettuate sono:

$$
7+10=17,
$$

$$
12+14=26,
$$

$$
17+26=43,
$$

$$
27+30=57,
$$

$$
43+57=100.
$$

L'evoluzione della coda con priorità può essere rappresentata come segue:

```text
{b:7, e:10, a:12, c:14, f:27, d:30}

{a:12, c:14, 17, f:27, d:30}

{17, 26, f:27, d:30}

{f:27, d:30, 43}

{43, 57}

{100}
```

---

## Albero di Huffman

Assegnando il primo nodo estratto come figlio sinistro e il secondo come figlio
destro, si ottiene il seguente albero:

```text
                         (100)
                        /     \
                      (43)    (57)
                     /   \    /   \
                   (17) (26) f:27 d:30
                   / \   / \
                 b:7 e:10 a:12 c:14
```

Etichettiamo ogni arco verso sinistra con `0` e ogni arco verso destra con `1`.

Il codice di ciascun simbolo è dato dalla sequenza di bit incontrata lungo il
cammino dalla radice alla foglia corrispondente.

---

## Codici prefissi ottenuti

| Simbolo | Codice |
|---|---|
| a | `010` |
| b | `000` |
| c | `011` |
| d | `11` |
| e | `001` |
| f | `10` |

Nessun codice è prefisso di un altro, perché tutti i simboli corrispondono a
foglie dell'albero.

## Osservazione

Il codice di Huffman ottenuto non è necessariamente unico.

È possibile scambiare il figlio sinistro e il figlio destro di uno o più nodi,
ottenendo codici binari differenti ma con le stesse lunghezze e lo stesso costo
complessivo.

Ad esempio, è possibile adottare la convenzione opposta, assegnando `1` agli
archi sinistri e `0` agli archi destri, purché la scelta rimanga coerente in
tutto l'albero.
