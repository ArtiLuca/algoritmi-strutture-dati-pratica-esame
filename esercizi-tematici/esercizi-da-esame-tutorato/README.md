# Esercizi da Esame e Tutorato

[← Torna agli esercizi tematici](../README.md) · [Torna alla raccolta principale](../../README.md)

Questa cartella raccoglie esercizi provenienti da temi d'esame, simulazioni e attività di tutorato, organizzati come materiale di pratica aggiuntiva per Algoritmi e Strutture Dati.

Gli esercizi coprono più argomenti del corso: ricorrenze, notazione asintotica, divide et impera, heap, alberi binari, alberi binari di ricerca e varianti ricorsive su strutture dati.

L'obiettivo è allenarsi su tracce realistiche d'esame, dove spesso non basta scrivere l'algoritmo: è richiesto anche motivare la correttezza, valutare la complessità e, quando necessario, fornire una dimostrazione formale.

Ogni esercizio completato contiene una soluzione in stile esame, con idea dell'algoritmo, pseudocodice, correttezza e analisi della complessità.

---

## Stato delle soluzioni

| Esercizio | Stato |
|---|---|
| Domanda A — Ricorrenza `T(n)=4T(n/2)+n^3+1` | [Completato](ricorrenza_master_theorem_domanda_A.md) |
| Domanda A — Ricorrenza `T(n)=T(n-1)+2n-1` | Da completare |
| Domanda A — Proprietà di `Θ(g(n))` | Da completare |
| Esercizio Ricorrenze (Sostituzione & Master Theorem) | [Completato](esercizio_ricorrenze_sostituzione_master.md) |
| Esercizio 1 — Centro di array semi-ordinato | Da completare |
| Esercizio 1 — `triplet(A)` | [Completato](triplet.md) |
| Domanda B — `toTree(A)` | Da completare |
| Domanda B — Albero Binario di Ricerca | Da completare |
| Domanda C — `diff(T)` | Da completare |
| Esercizio 1 — Albero `k-bounded` | Da completare |
| Esercizio 1 — `union(A1,A2,n)` con max-heap | Da completare |
| DP su stringhe con Memoization | [Completato](dp_stringhe_memoizzazione.md) |
| Domanda A - Ricorrenza con Master Theorem | [Da Completare](domanda_master_theorem.md) |
| Domanda B - Activity Selection Greedy Sel | [Completato](greedy_sel.md) |
| Esercizio 2 - Selezioni di Attività Compatibili | [Da Completare](activity_selection.md) |
| Domanda B - Algoritmo di Huffman | [Da Completare](domanda_huffman_1.md) |
| Domanda B - Hashing con doppio hashing | [Da Completare](double_hashing.md) |
| Esercizio 2 - Scheduling greedy e somma dei tempi di completamento | [Da Completare] |
| Domanda A — Ricorrenze e classe Ω esponenziale | [Da Completare] |
| Domanda B — Longest Common Subsequence (LCS) | [Da Completare]|
| Esercizio 1 — Ordinamento in loco (TriSort) | [Da Completare] |
| Esercizio 2 — Algoritmo greedy per il resto delle monete | [Da Completare] |

---

## Testi degli Esercizi

### Domanda A — 6 punti

Dare una soluzione asintotica per la ricorrenza

$$
T(n)=4T(n/2)+n^3+1.
$$

---

### Domanda A — 7 punti

Risolvere la seguente ricorrenza

$$
T(n)=T(n-1)+2n-1
$$

fornendo un limite asintotico stretto per la soluzione.

Individuare una ipotesi di soluzione e quindi utilizzare il metodo di sostituzione per dimostrarne la correttezza.

---

### Domanda A — 8 punti

Definire formalmente la classe $\Theta(g(n))$.

Dimostrare le seguenti affermazioni o fornire un controesempio:

1. se $f(n),f'(n)\in\Theta(g(n))$ allora

$$
f(n)+f'(n)\in\Theta(g(n));
$$

2. $f(n),f'(n)\in\Theta(g(n))$ allora

$$
f(n)\cdot f'(n)\in\Theta(g(n)).
$$

---

### Esercizio Ricorrenze (Sostituzione & Master Theorem)

1. Dimostrare che la ricorrenza $T(n) = T(n/2) + T(n/4) + n$ ammette soluzione $\Theta(n)$
2. Trovare un'ipotesi per $T(n) = T(n-2) + 2n$ e dimostrare con sostituzione
3. Master Theorem per $T(n) = 4T(n/2) + n\log n$
4. Master Theorem per $T(n) = 4T(n/2) + n^2\sqrt{n}$

---

### Esercizio 1 — 10 punti

Diciamo che un array senza ripetizioni $A[1,n]$ è **semi-ordinato** se esiste un indice $k$, con

$$
1\leq k<n,
$$

tale che

$$
A[k+1..n]A[1..k]
$$

sia ordinato, ovvero i sottoarray $A[k+1..n]$ e $A[1..k]$ sono ordinati e

$$
A[n]<A[1].
$$

In questo caso l'indice $k$ viene detto il **centro** dell'array.

Ad esempio l'array che segue è semi-ordinato con centro $k=4$:

| Indice | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---:|---:|---:|---:|---:|---:|---:|
| A | 4 | 9 | 12 | 18 | -1 | 1 | 2 |

Scrivere una funzione `centre(A)` che dato un array $A$ semi-ordinato ne restituisce il centro.

Giustificare la correttezza dell'algoritmo e valutarne la complessità.

---

### Esercizio 1 — 9 punti

Realizzare una procedura `triplet(A)` che dato un array $A[1,n]$ di interi verifica se esistono tre indici, non necessariamente distinti, $i$, $j$ e $k$ tali che

$$
A[i]+A[j]=A[k].
$$

Fornire lo pseudocodice, motivare la correttezza della soluzione e valutarne la complessità.

---

### Domanda B — 7 punti — `toTree(A)`

Scrivere una funzione `toTree(A)` che, dato un array $A$ organizzato a max-heap (dimensione `A.heapSize`), lo trasforma in un albero binario realizzato con strutture linked, ancora organizzato a max-heap, e ritorna la radice di tale albero.

Il nuovo albero è costituito da nodi $x$ con i campi:

- `x.p` (parent);
- `x.k` (chiave);
- `x.l` (figlio sinistro);
- `x.r` (figlio destro).

Per allocare un nuovo nodo si assuma di avere a disposizione un costruttore `node()`.

Valutare la complessità.

---

### Domanda B — 5 punti — Albero Binario di Ricerca

Dare la definizione di albero binario di ricerca.

Specificare l'albero ottenuto inserendo, con la procedura vista a lezione, a partire da un albero vuoto, i nodi aventi le seguenti chiavi:

$$
5,\ 4,\ 8,\ 6,\ 12,\ 7.
$$

Si supponga che dall'albero così ottenuto si cancelli il nodo con chiave $5$ e si indichi l'albero ottenuto.

Sia per gli inserimenti che per la cancellazione, motivare sinteticamente il risultato ottenuto.

---

### Domanda C — 5 punti — `diff(T)`

Scrivere una funzione `diff(T)` che, dato in input un albero binario di ricerca $T$, determina la massima differenza di lunghezza tra due cammini che vanno dalla radice ad un sottoalbero vuoto.

Ad esempio:

- sull'albero ottenuto inserendo $1,2,3$ produce $2$;
- su quello ottenuto inserendo $2,1,3$ produce $0$.

Valutarne la complessità.

---

### Esercizio 1 — 7 punti — Albero k-bounded

Sia $T$ un albero binario i cui nodi $x$ hanno i campi:

- `x.left`
- `x.right`
- `x.key`

L'albero si dice **k-bounded**, per un certo valore $k$, se per ogni nodo $x$ la somma delle chiavi lungo ciascun cammino da $x$ ad una foglia è minore o uguale a $k$.

Scrivere una funzione `Bound(T,k)` che, dato in input un albero $T$ e un valore $k$, verifica se $T$ è k-bounded e ritorna un corrispondente valore booleano.

Valutarne la complessità.

---

### Esercizio 1 — 10 punti — `union(A1,A2,n)`

Realizzare una funzione `union(A1,A2,n)` che, dati due array di interi $A1$ e $A2$, organizzati a max-heap, con capacità $n$, restituisce un nuovo array $A$, ancora organizzato a max-heap con capacità $2n$, che contiene l'unione insiemistica dei valori contenuti in $A1$ e $A2$.

Si assuma che $A1$ e $A2$ non contengano duplicati e si faccia in modo anche che l'array ottenuto come unione non contenga duplicati.

Ad esempio, se $A1$ contiene i valori

$$
3,\ 1,\ 2
$$

e $A2$ contiene i valori

$$
5,\ 2,
$$

allora l'unione $A$ conterrà i valori

$$
5,\ 3,\ 1,\ 2,
$$

possibilmente non in questo ordine, ovvero l'elemento $2$ non è duplicato.

Valutare la complessità della funzione definita.

Qualora il risultato $A$ potesse contenere duplicati ci sarebbero soluzioni più efficienti?

---

### Esercizio 2 - DP su stringhe con Memoization

Data una stringa $X = x_1, x_2, \dots, x_n$, si consideri la seguente quantità $\ell(i, j)$, definita per $1 \le i \le j \le n$:

$$
\ell(i, j) =
\begin{cases}
1 & \text{se } i = j \\
2 & \text{se } i = j - 1 \\
2 + \ell(i + 1, j - 1) & \text{se } i < j - 1 \text{ e } x_i = x_j \\
\sum_{k=i}^{j-1}(\ell(i,k) + \ell(k+1,j)) & \text{se } i < j - 1 \text{ e } x_i \ne x_j
\end{cases}
$$

- **(1)** Scrivere una coppia di algoritmi `INIT_L(X)` e `REC_L(i, j)` per il calcolo memoizzato di $\ell(1, n)$.
- **(2)** Si determini la complessità al caso migliore $T_{\text{best}}(n)$ supponendo che le uniche operazioni di costo unitario e non nullo siano i confronti tra caratteri.

---

### Domanda A - Ricorrenza con Master Theorem

Si determini la soluzione asintotica della seguente equazione di ricorrenza:

```math
T(n)=3T(n/3)+n^2+1.
```

---

### Domanda B - Activity Selection Greedy Sel

Si consideri il problema di selezione di attività compatibili:

**(a)** Definire il problema.

**(b)** Descrivere brevemente l'algoritmo ottimo `GREEDY-SEL` visto in classe.

**(c)** Fornire un esempio di algoritmo greedy *non* ottimo, motivandone la non
ottimalità.

---

### Esercizio 2 - Selezioni di Attività Compatibili

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

### Domanda B - Algoritmo di Huffman

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

### Domanda B - Hashing con doppio hashing 

Si consideri una tabella hash di dimensione $m=7$, e indirizzamento aperto con
doppio hash basato sulle funzioni:

```math
h_1(k)=k \bmod m
```

e

```math
h_2(k)=1+k \bmod (m-2).
```

Si descriva sinteticamente come avviene l'inserimento degli elementi e si
specifichi il risultato dell'inserzione della sequenza di chiavi:

```math
10,20,34,35,48.
```

Sarebbe appropriato lavorare con una tabella di dimensione $m=8$ e le stesse
funzioni hash?

---

### Esercizio 2 - Scheduling greedy e somma dei tempi di completamento

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

### Domanda A — Ricorrenze e classe Ω esponenziale

Data la ricorrenza:

$$ 
T(n) = \frac{3}{2}T(n-1) + 2 
$$

mostrare che la soluzione è $O(2^n)$.

Vale anche $T(n) = \Omega(2^n)$? Motivare la risposta.

---

### Domanda B — Longest Common Subsequence (LCS)

Scrivere la ricorrenza sulle lunghezze $\ell(i,j)$ per il problema della longest
common subsequence (LCS).

---

### Esercizio 1 — Ordinamento in loco (TriSort)

Realizzare una procedura `TriSort(A)` che dato un array $A[1 \dots n]$ di $n$
elementi, con valori in $\{0, 1, 2\}$, lo ordina in modo crescente.

L'unica operazione ammessa per modificare l'array è:

$$ 
A[i] \leftrightarrow A[j] 
$$

il cui effetto è quello di scambiare gli elementi in posizione $i$ e $j$.

Dare lo pseudocodice e motivarne la correttezza. Valutare la complessità asintotica,
indicando anche il numero di confronti e di scambi nel caso peggiore.

---

### Esercizio 2 — Algoritmo greedy per il resto delle monete

Supponiamo di avere un numero illimitato di monete di ciascuno dei seguenti
valori: $\{50, 20, 1\}$. Dato un numero intero positivo $n$, l'obiettivo è selezionare il
più piccolo numero di monete tale che il loro valore totale sia $n$. Consideriamo
l'algoritmo greedy che consiste nel selezionare ripetutamente la moneta di
valore più grande possibile.

### Punto (a)

Fornire un valore di $n$ per cui l'algoritmo greedy non restituisce una
soluzione ottima.

### Punto (b)

Supponiamo ora che i valori delle monete siano $\{10, 5, 1\}$. In questo caso
l'algoritmo greedy restituisce sempre una soluzione ottima: dimostrare che ogni
insieme ottimo $M^\star$ di monete di valore totale $n$ contiene la scelta greedy.
