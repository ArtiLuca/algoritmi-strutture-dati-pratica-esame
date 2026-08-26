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
| Domanda A - Proprietà di $\mathcal{O}$ e $\Omega(n)$ | [Completato](notazione_asintotica_dimostrazione_domanda_A.md) |
| Esercizio Ricorrenze (Sostituzione & Master Theorem) | [Completato](esercizio_ricorrenze_sostituzione_master.md) |
| Esercizio 1 — `triplet(A)` | [Completato](triplet.md) |
| Domanda B — Albero Binario di Ricerca | Da completare |
| Domanda C — `diff(T)` | Da completare |
| Esercizio 1 — Albero `k-bounded` | Da completare |
| Esercizio 1 — `union(A1,A2,n)` con max-heap | Da completare |
| DP su stringhe con Memoization | [Completato](dp_stringhe_memoizzazione.md) |
| Domanda A - Ricorrenza con Master Theorem | [Completato](domanda_master_theorem.md) |
| Domanda B - Activity Selection Greedy Sel | [Completato](greedy_sel.md) |
| Esercizio 2 - Selezioni di Attività Compatibili | [Completato](activity_selection.md) |
| Domanda B - Algoritmo di Huffman | [Da Completare](domanda_huffman_1.md) |
| Domanda B - Hashing con doppio hashing | [Completato](double_hashing.md) |
| Esercizio 2 - Scheduling greedy e somma dei tempi di completamento | [Completato](schedule_opt.md) |
| Domanda A — Ricorrenze e classe Ω esponenziale | [Da Completare] |
| Domanda B — Longest Common Subsequence (LCS) | [Da Completare]|
| Esercizio 1 — Ordinamento in loco (TriSort) | [Da Completare] |
| Esercizio 2 — Algoritmo greedy per il resto delle monete | [Da Completare] |
| Domanda A — Ricorrenza con metodo di sostituzione | [Completato](domanda_ricorrenza_sostituzione.md) |
| Esercizio 2 - Programmazione dinamica bottom-up | [Completato](esercizio_dp_bottom_up_esame.md) |
| Esercizio 1 — Split con divide et impera | [Completato](split.md) | 
| Esercizio 2 — Programmazione dinamica (DP 2023) | [Completato](esercizio_dp_bottom_up_stringhe.md) |

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

### Domanda A — Classi $\mathcal{O}$ e $\Omega$

Dare la definizione formale delle classi $\mathcal{O}(f(n))$ e $\Omega(f(n))$ per una funzione $f(n)$.
Mostrare che se $f(n) = \mathcal{O}(n)$ e $g(n) = n^2 - f(n),$ allora $g(n) = \Omega(n^2)$.

---

### Esercizio Ricorrenze (Sostituzione & Master Theorem)

1. Dimostrare che la ricorrenza $T(n) = T(n/2) + T(n/4) + n$ ammette soluzione $\Theta(n)$
2. Trovare un'ipotesi per $T(n) = T(n-2) + 2n$ e dimostrare con sostituzione
3. Master Theorem per $T(n) = 4T(n/2) + n\log n$
4. Master Theorem per $T(n) = 4T(n/2) + n^2\sqrt{n}$

---

### Esercizio 1 — 9 punti

Realizzare una procedura `triplet(A)` che dato un array $A[1,n]$ di interi verifica se esistono tre indici, non necessariamente distinti, $i$, $j$ e $k$ tali che

$$
A[i]+A[j]=A[k].
$$

Fornire lo pseudocodice, motivare la correttezza della soluzione e valutarne la complessità.

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

---

### Domanda A — Ricorrenza con metodo di sostituzione

Si dimostri che la ricorrenza che segue ha soluzione $T(n)=\Theta(n)$:

```math
T(n)=\frac{2}{3}T(n-1)+2n.
```

---

### Esercizio 2 — Programmazione dinamica bottom-up

Date due stringhe $X = \langle x_1, x_2, \dots, x_m \rangle$ e $Y = \langle y_1, y_2, \dots, y_n \rangle$, si consideri la seguente quantità $\ell(i, j)$, definita per ogni coppia di valori $i, j$ con $0 \le i \le m$ e $0 \le j \le n$:

$$
\ell(i, j) =
\begin{cases}
1 & \text{se } i = 0 \text{ oppure } j = 0 \\
3 \cdot \ell(i, j - 1) & \text{se } i, j > 0 \text{ e } x_i = y_j \\
2 \cdot \ell(i - 1, j - 1) - \ell(i - 1, j) & \text{se } i, j > 0 \text{ e } x_i \ne y_j
\end{cases}
$$

Si vuole calcolare la quantità:

$$
q = \max \{ \ell(i, j) : 0 \le i \le m, 0 \le j \le n \}
$$

- **(a)** Scrivere un algoritmo bottom-up per il calcolo di $q$.
- **(b)** Determinare la complessità esatta dell'algoritmo, supponendo che le uniche operazioni di costo unitario e non nullo siano i confronti tra caratteri.

---

### Esercizio 1 — Split con divide et impera

Sia dato un array $V[1..n]$ i cui valori rappresentano la variazione giornaliera del valore di un titolo azionario.

È noto che il titolo è stato prima in perdita, con valori sempre negativi, poi ha iniziato a oscillare in giorni consecutivi tra valori positivi e negativi, e infine si è stabilizzato su valori positivi. Dunque nella sequenza **non possono esserci due giorni positivi seguiti da un negativo**.

Realizzare un algoritmo divide et impera `Split(V)` che individua il giorno in cui il titolo ha iniziato a essere stabile su valori positivi, ovvero il minimo indice

$$
i \in [1,n]
$$

tale che

$$
\forall j \ge i,\quad V[j] > 0.
$$

Se il titolo non si stabilizza su valori positivi, ritornare `0`.

Esempi:

- per $V=[-1,-2,2,-1,6,3]$ si deve ritornare $5$;
- per $V=[-1,-2,2,-1,6,-3]$ si deve ritornare `0`.

Fornire lo pseudocodice di `Split(V)`, motivarne la correttezza e individuarne la complessità. Si assuma che non ci siano valori nulli.

---

### Esercizio 2 — Programmazione dinamica (DP 2023)

Per $n > 0$, siano dati due vettori a componenti intere $a, b \in \mathbb{Z}^n$.
Si consideri la quantità $c(i, j)$ con $0 \le i \le j \le n-1$, definita come segue:

$$
c(i, j) =
\begin{cases}
a_i & \text{se } 0 < i \le n-1 \text{ e } j = n-1 \\
b_j & \text{se } i = 0 \text{ e } 0 \le j \le n-1 \\
c(i-1, j-1) \cdot c(i, j+1) & \text{se } 0 < i \le j < n-1
\end{cases}
$$

Si vuole calcolare la quantità:

$$
m = \max \{ c(i, j) : 0 \le i \le j \le n-1 \}
$$

- **(a)** Fornire un algoritmo iterativo bottom-up per il calcolo di $m$.
- **(b)** Valutare la complessità esatta dell’algoritmo, associando costo unitario alla moltiplicazione tra numeri interi e costo nullo a tutte le altre operazioni.
