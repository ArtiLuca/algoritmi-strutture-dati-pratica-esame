# Esercizi Tematici — Algoritmi e Strutture Dati

[← Torna alla raccolta principale](../README.md)

Questa cartella raccoglie esercizi di pratica su Algoritmi e Strutture Dati, scelti per approfondire gli argomenti del corso e allenarsi su problemi simili a quelli d'esame.

Gli esercizi non sono organizzati in base alla loro provenienza o difficoltà: l'obiettivo è avere una raccolta unica e semplice da espandere durante la preparazione.

Ogni esercizio completato contiene una soluzione completa in stile esame, con pseudocodice, motivazione della correttezza e analisi della complessità quando richieste.

---

## Stato delle soluzioni

| Esercizio | Stato |
|---|---|
| Insertion Sort ricorsivo | Da completare |
| Duplicati con Divide et Impera | Da completare |
| Somma di due elementi | Da completare |
| Proprietà della notazione asintotica | Da completare |
| Ricorrenza con metodo di sostituzione | Da completare |
| Ricorrenze asintotiche | Da completare |
| MergeSort con allocazione singola | Da completare |
| Ricerca binaria ricorsiva | Da completare |
| Moneta falsa | Da completare |
| Select con Heap | Da completare |
| Linked Heaps | Da completare |
| Fusione di Heap | Da completare |
| Conteggio delle inversioni | Da completare |
| QuickSort con Tripartition | Da completare |
| Hash invariato per anagrammi | Da completare |
| MSD RadixSort | Da completare |
| ABR e visita InOrder | Da completare |
| Ordinamento degli elementi di un Max-Heap | Da completare |
| Costruzione lineare di un ABR quasi completo | Da completare |
| Insert ricorsiva in un ABR | Da completare |
| Pairing delle carte | Da completare |
| Commutatività di ABR Delete | Da completare |
| ABR con puntatore al successore | Da completare |
| LCS — Proprietà di sottostruttura ottima | Da completare |
| LCS — Spanking e Amputation | Da completare |
| Sottostringa palindroma massima | Da completare |
| Shortest Common Supersequence | [Completato](../programmazione-dinamica-greedy/esercizio_20.md) |
| Ricorrenza memoizzata $M(i,j)$ | Da completare |
| Longest Increasing Subsequence | [Completato](../programmazione-dinamica-greedy/esercizio_28.md) |
| Shortest Palindrome Completion | Da completare |
| Selezione di attività compatibili | Da completare |
| Soste minime ai distributori | Da completare |
| Codifica di Huffman | Da completare |

---

## Testi degli Esercizi

### Insertion Sort ricorsivo

Realizzare una versione ricorsiva della funzione `InsertionSort`.

---

### Duplicati con Divide et Impera

Realizzare una funzione `Dup(A, p, r)` che verifica, in modo divide et impera, la presenza di duplicati nell'array $A$, restituendo un booleano.

Estenderla ad una funzione `DupCount(A, p, r)` che conti il numero di duplicati, ovvero il numero di coppie:

$$
\{(i,j) \mid i \neq j \land A[i]=A[j]\}
$$

Può essere interessante anche considerare varianti in cui si contano i valori ripetuti:

$$
\{A[i] \mid \exists j.\ j\neq i \land A[i]=A[j]\}
$$

oppure gli indici corrispondenti a ripetizioni:

$$
\{i \mid \exists j.\ j\neq i \land A[i]=A[j]\}
$$

---

### Somma di due elementi

Realizzare una funzione `Sum(A, key)` che, dato un array $A$ e un intero $key$, verifica se esistono indici $i$ e $j$ tali che:

$$
key=A[i]+A[j]
$$

---

### Proprietà della notazione asintotica

Dimostrare le seguenti uguaglianze:

- $f(n)=O(g(n))$ sse $g(n)=\Omega(f(n))$
- $\Theta(g(n))=O(g(n))\cap\Omega(g(n))$
- $f(n)=\Theta(f(n))$
- $f(n)=\Theta(g(n))$ sse $\Theta(f(n))=\Theta(g(n))$ sse $g(n)=\Theta(f(n))$
- $f(n)=O(g(n))$ e $g(n)=O(h(n))$ implica $f(n)=O(h(n))$

---

### Ricorrenza con metodo di sostituzione

Risolvere con il metodo di sostituzione:

$$
T(n)=T(n/3)+T(2n/3)+\Theta(n)
$$

mostrando che:

$$
T(n)=\Theta(n\log n)
$$

---

### Ricorrenze asintotiche

Risolvere:

$$
T(n)=2T(n/2)+\log n
$$

$$
T(n)=2T(n/2)+n^2
$$

$$
T(n)=2T(n/2)+n\log n
$$

---

### MergeSort con allocazione singola

Realizzare una versione del MergeSort nella quale l'array di supporto è allocato staticamente.

La procedura sarà del tipo `MergeSort(A, B, ...)`, dove $A$ è l'array di input e $B$ è un array della stessa dimensione utilizzato per la memorizzazione temporanea.

- **Versione 1:** utilizzare $B$ per memorizzare temporaneamente le parti già ordinate delle quali effettuare il merge.
- **Versione 2:** effettuare alternativamente il merge da $A$ verso $B$ e viceversa, evitando la fase di copia.
- **Possibile ottimizzazione:** ordinare i sottoarray più piccoli di una certa soglia $k$ con Insertion Sort.
- **Versione 3:** realizzare la procedura in modo iterativo anziché ricorsivo.

---

### Ricerca binaria ricorsiva

Realizzare una funzione ricorsiva `Search(A, k)` che, dato un array ordinato $A$ e un valore $k$, restituisce un indice $i$ tale che $A[i]=k$, se esiste, oppure $0$ altrimenti.

Analizzarne la complessità.

---

### Moneta falsa

Siano date $n$ monete, delle quali una è falsa e pesa meno delle altre.

Utilizzando una bilancia a due piatti e avendo a disposizione come operazione soltanto la pesata di due sottoinsiemi disgiunti di monete:

1. dare un algoritmo di complessità $O(\log n)$ che determina la moneta falsa;
2. mostrare che ogni algoritmo per il problema richiede $\Omega(\log n)$ operazioni.

---

### Select con Heap

Realizzare una funzione `Select(A, k)` che restituisce l'elemento che occuperebbe la $k$-esima posizione nell'array $A$ ordinato.

Trovare soluzioni con complessità:

- $O(n\log n)$
- $O(n+k\log n)$
- $O(n\log k)$

Per gli ultimi due casi utilizzare rispettivamente un MinHeap e un MaxHeap.

---

### Linked Heaps

Fornire una implementazione dei Max-Heap come alberi realizzati mediante strutture a puntatori.

Ogni nodo $x$ avrà almeno i campi:

- `x.key`
- `x.left`
- `x.right`

Realizzare le varie operazioni studiate sugli Heap e valutarne la complessità.

---

### Fusione di Heap

Realizzare una procedura `Fusion(T1, T2)` per fondere due alberi binari $T_1$ e $T_2$, il primo completo e il secondo quasi completo, della stessa altezza, che soddisfano la proprietà di Max-Heap.

La procedura deve mantenere la proprietà di Max-Heap e avere costo:

$$
O(\log n)
$$

dove $n$ è il numero totale di elementi.

---

### Conteggio delle inversioni

Realizzare con approccio Divide et Impera una funzione `Inv(A, p, r)` che ritorna il numero di inversioni in $A[p\dots r]$.

Una inversione è una coppia di indici $i,j$ tale che:

$$
i<j
\qquad\text{e}\qquad
A[i]>A[j]
$$

*Suggerimento: modificare MergeSort.*

---

### QuickSort con Tripartition

Realizzare una versione di `QuickSort(A, p, r)` basata su una tripartizione degli elementi.

La procedura `Partition(A, p, r)` deve dividere gli elementi in:

1. elementi minori della chiave;
2. elementi uguali alla chiave;
3. elementi maggiori della chiave.

Deve restituire due indici $q_1,q_2$ che individuano:

$$
A[p\dots q_1-1]
$$

$$
A[q_1\dots q_2]
$$

$$
A[q_2+1\dots r]
$$

---

### Hash invariato per anagrammi

Mostrare che la funzione:

$$
h(k)=k\bmod m
$$

quando:

$$
m=2^p-1
$$

e le chiavi $k$ consistono di $w$ parole di $p$ bit, è invariante rispetto a permutazioni delle parole che costituiscono la chiave.

---

### MSD RadixSort

Scrivere una versione del RadixSort che inizi l'ordinamento dalla cifra più significativa.

Una volta effettuato l'ordinamento rispetto alla cifra $j$-esima, occorre ordinare separatamente rispetto alla cifra $(j-1)$-esima i sottoarray che hanno identico valore per la cifra $j$-esima.

---

### ABR e visita InOrder

Dimostrare che un albero binario è un Albero Binario di Ricerca se e solo se una visita simmetrica elenca i nodi in ordine di chiave crescente.

---

### Ordinamento degli elementi di un Max-Heap

Dire se esiste un algoritmo di tempo lineare per elencare gli elementi di un Max-Heap in ordine crescente o decrescente.

Descrivere l'algoritmo oppure motivare l'impossibilità di realizzarlo.

---

### Costruzione lineare di un ABR quasi completo

Dire se esiste un algoritmo di tempo lineare per costruire un Albero Binario di Ricerca quasi completo a partire da un array $A$.

Descrivere l'algoritmo oppure motivare l'impossibilità di realizzarlo.

---

### Insert ricorsiva in un ABR

Realizzare una versione ricorsiva della procedura `Insert(T, x)` per gli Alberi Binari di Ricerca.

---

### Pairing delle carte

È dato un mazzo che contiene una coppia di carte per ogni valore $1,\dots,n$.

Le carte sono suddivise in due sequenze disordinate.

È possibile spostare una carta in una posizione diversa della stessa sequenza oppure nell'altra sequenza.

Determinare la carta di valore massimo che deve necessariamente essere spostata per riavvicinare tutte le coppie.

---

### Commutatività di ABR Delete

Dato un ABR $T$ e due suoi nodi $x$ e $y$, stabilire se eseguire le cancellazioni nei due ordini:

$$
Delete(Delete(T,x),y)
$$

e

$$
Delete(Delete(T,y),x)
$$

porta sempre allo stesso albero.

---

### ABR con puntatore al successore

Realizzare una implementazione degli Alberi Binari di Ricerca nella quale il campo padre `p` è sostituito dal campo `succ`, contenente il successore del nodo.

---

### LCS — Proprietà di sottostruttura ottima

Completare la dimostrazione della proprietà di sottostruttura ottima della Longest Common Subsequence.

---

### LCS — Spanking e Amputation

Calcolare la LCS tra:

- **spanking**
- **amputation**

calcolando soltanto la tabella $L[i,j]$ delle lunghezze.

---

### Sottostringa palindroma massima

Dare un algoritmo per individuare, all'interno di una stringa, una sottostringa di caratteri consecutivi palindroma di lunghezza massima.

Più precisamente:

1. dare una caratterizzazione ricorsiva;
2. ottenere un algoritmo bottom-up o top-down con memoization;
3. permettere anche la ricostruzione della sottostringa;
4. valutare la complessità.

---

### Shortest Common Supersequence

Realizzare un algoritmo che, date due sequenze $X$ e $Y$, determina una Shortest Common Supersequence $Z$ di lunghezza minima tale che:

$$
X\sqsubseteq Z
\qquad\text{e}\qquad
Y\sqsubseteq Z
$$

Determinare la caratterizzazione ricorsiva, l'algoritmo, la ricostruzione della soluzione e la complessità.

---

### Ricorrenza memoizzata $M(i,j)$

Sia $n>0$ e sia:

$$
M(i,j)=
\begin{cases}
1 & i=j\\
2 & j=i+1\\
M(i+1,j-1)M(i+1,j)M(i,j-1) & j>i+1
\end{cases}
$$

1. Scrivere `INIT_M(n)` e `REC_M(i,j)` per il calcolo memoizzato di $M(1,n)$.
2. Calcolare il numero esatto di moltiplicazioni eseguite.

---

### Longest Increasing Subsequence

Dimostrare la proprietà di sottostruttura ottima della Longest Increasing Subsequence.

---

### Shortest Palindrome Completion

Data una stringa $X$, determinare un completamento palindromo di lunghezza minima che contenga $X$ come sottosequenza.

- Dimostrare la proprietà di sottostruttura ottima.
- Calcolare l'informazione addizionale necessaria alla ricostruzione.
- Scrivere `PRINT-PC(i, j, B, X)` per stampare la soluzione.

---

### Selezione di attività compatibili

Si considerino $6$ attività con:

$$
s=(2,1,2,3,4,7)
$$

$$
f=(4,4,6,11,12,13)
$$

Determinare l'insieme di attività compatibili selezionato dall'algoritmo `GREEDY-SEL`.

---

### Soste minime ai distributori

Un'auto deve viaggiare da $A$ a $B$ con autonomia limitata.

Lungo il percorso sono presenti distributori a distanze note.

Determinare un algoritmo greedy che minimizzi il numero di soste necessarie, dimostrandone la correttezza e valutandone la complessità.

---

### Codifica di Huffman

Dato un alfabeto:

$$
\{A,B,C,D,E\}
$$

con frequenze:

$$
12\%,11\%,53\%,10\%,14\%
$$

determinare le cinque codeword prodotte dall'algoritmo di Huffman.
