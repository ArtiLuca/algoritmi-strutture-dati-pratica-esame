# Ordinamento e Heap

[← Torna agli esercizi tematici](../README.md) · [Torna alla raccolta principale](../../README.md)

Questa cartella raccoglie esercizi su algoritmi di ordinamento, varianti di counting sort, proprietà di array ordinati o parzialmente ordinati, e strutture heap.

Gli esercizi sono utili per ripassare sia algoritmi classici sia piccole varianti richieste spesso negli esami: modifiche a counting sort, ricerca di coppie in array ordinati, verifica della proprietà di heap ed estrazione da heap.

Ogni esercizio completato contiene una soluzione in stile esame, con pseudocodice, spiegazione dell'idea, correttezza e complessità.

---

## Stato delle soluzioni

| Esercizio | Stato |
|---|---|
| Esercizio 6 — Minimo tra due array permutati | Da completare |
| Domanda 20 — `RevCountingSort(A, B, n, k)` | [Completato](rev_counting_sort.md) |
| Esercizio 7 — Anagramma su alfabeto `{0, 1}` | [Completato](anagramma.md) |
| Domanda 21 — Coppia con `A[j] = 2 * A[i]` | [Completato](double.md) |
| Esercizio 8 — Massimo in array bi-ordinato | [Completato](top.md) |
| Esercizio 9 — Permutazione delle cifre | [Completato](permutazione.md) |
| Domanda 22 — Successore della radice in min-heap | [Completato](sndmin.md) |
| Domanda 23 — `IsMaxHeap(A)` | [Completato](is_max_heap.md) |
| Domanda 24 — `HeapExtractMin(A)` | [Completato](heap_extract_min.md) |
| Domanda 25 — `BuildMaxHeap` su array dato | [Completato](build_max_heap.md) |
| Minimo tra Min-Heap e Max-Heap — `min(A,B)` | [Completato](minimo_heap.md) |
| Esercizio SortJoin | [Completato](sort_join.md) |

---

## Testi degli Esercizi

### **Esercizio 6**

Fornire lo pseudocodice di una procedura `min(A, B)` che dati due array `A` e `B` che siano uno la permutazione dell'altro ne trova l'elemento minimo confrontando esclusivamente elementi di `A` ed elementi di `B` (non si possono confrontare due elementi di `A` o due elementi di `B` tra loro, e non si possono fare copie degli array, ovvero la funzione deve operare con spazio costante). Valutare la complessità della funzione.

---

### **Domanda 20**

Realizzare una funzione `RevCountingSort(A, B, n, k)` che, dato un array `A[1..n]` contenente interi nell'intervallo $[0..k]$, restituisce in `B[1..n]` una sua permutazione ordinata in modo decrescente utilizzando una variante del counting sort. Valutarne la complessità.

---

### **Esercizio 7**

Realizzare una funzione `Anagramma(x, y)` che date due stringhe $x$ e $y$ sull'alfabeto $\{0, 1\}$, verifica se $x$ è un anagramma di $y$ restituendo conseguentemente `true` o `false`. Una stringa è vista come un array di caratteri, con lunghezza data dall'attributo `len`. Ad esempio, la stringa $x$ è la sequenza di caratteri `x[1] x[2] ... x[x.len]`. Valutare la complessità.

---

### **Domanda 21**

Realizzare una funzione `Double(A, n)` che, dato un array `A[1..n]` ordinato in senso crescente, verifica se esiste una coppia di indici $i, j$ tali che $A[j] = 2 * A[i]$. Restituisce la coppia se esiste e `(0, 0)` altrimenti. Scrivere lo pseudocodice e valutare la complessità.

---

### **Esercizio 8**

Si dica che un array `A[1..n]` è *bi-ordinato* se esiste un indice $k$ tale che `A[1..k]` è ordinato in senso crescente e `A[k..n]` è ordinato in senso decrescente. Realizzare un algoritmo `top(A, n)` che dato in input un array `A` bi-ordinato con elementi distinti ne determina il valore massimo. Ad esempio su `A = (1, 2, 3, 14, 13, 4)` restituisce 14. Valutarne la complessità.

---

### **Esercizio 9**

Scrivere una funzione `perm(m, n)` che dati due numeri interi $m$ e $n$, maggiori o uguali di 0, verifica se uno dei due numeri può essere ottenuto permutando le cifre dell'altro. Ad esempio 915 e 159 sono uno la permutazione dell'altro mentre 911 e 19 no. Attenzione al ruolo degli zeri, ad es. 150 è la permutazione di 51, dato che $51 = 051$. Valutarne la complessità.

> **Suggerimento:** Il counting sort può fornire una ispirazione.
>

---

# Heap

### **Domanda 22**

Scrivere una funzione `sndmin(A)` che dato in input un array `A` organizzato a min-heap, restituisce il successore della radice, ovvero il minimo elemento dello heap maggiore della radice. Se un tale elemento non esiste genera un errore. Assumere che `A` sia non vuoto e gli elementi in `A` siano tutti distinti.

---

### **Domanda 23**

Scrivere una funzione `IsMaxHeap(A)` che dato in input un array di interi `A[1..n]` verifica se `A` è organizzato a max-heap e ritorna un corrispondente valore booleano. Valutarne la complessità.

---

### **Domanda 24**

Fornire lo pseudocodice della procedura `HeapExtractMin(A)` per estrarre il minimo elemento da un min-heap `A`, realizzato tramite un array come visto a lezione (la dimensione corrente dello heap è data dall'attributo `A.heapsize`). Discuterne la complessità.

---

### **Domanda 25**

Dare la definizione di max-heap. Dato un array `A[1..12]` con sequenza di elementi `[60, 6, 45, 95, 30, 24, 15, 80, 19, 38, 21, 70]` si indichi il risultato della procedura `BuildMaxHeap` applicata ad `A`. Si descriva sinteticamente come si procede per arrivare al risultato.

---

### **Domanda A (7 punti)**  

Dare la definizione di max-heap.  

Dato un insieme $S$ di elementi, memorizzato in parte in un min-heap $A$ e in parte in un max-heap $B$, entrambi non vuoti, dare un algoritmo $\min(A, B)$ per trovare il minimo di $S$ nelle due situazioni seguenti:  
  
(a) ogni elemento di $A$ è minore o uguale a ogni elemento di $B$;  

(b) ogni elemento di $B$ è minore o uguale a ogni elemento di $A$.  

In entrambi i casi scrivere lo pseudocodice e valutare la complessità.

---

## SortJoin

Siano dati due array $A[1 \dots 2n]$ e $B[1 \dots n]$ organizzati a max-heap, entrambi
contenenti $n$ elementi (`heapsize=n`).

Realizzare una procedura `SortJoin(A, B, n)` che dati in input array $A$ e $B$
con le proprietà sopra descritte, ritorna in $A$ un array ordinato contenente
tutti i $2n$ elementi originariamente presenti in $A$ e $B$.

L'array $B$ può essere modificato durante l'esecuzione della procedura, se
necessario, ma l'algoritmo dovrà operare in *spazio costante*.

Dare lo pseudocodice della procedura, motivarne la correttezza e valutarne la
complessità. Se si utilizzano operazioni sui max-heap andranno definite
esplicitamente.
