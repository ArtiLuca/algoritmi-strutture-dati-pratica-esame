# Alberi, Ricorsione, ABR e RB-Tree

[← Torna agli esercizi tematici](../README.md) · [Torna alla raccolta principale](../../README.md)

Questa cartella raccoglie esercizi su alberi binari, ricorsione su strutture ad albero e tabelle hash.

La prima parte è dedicata ad algoritmi ricorsivi su alberi binari: cammini, livelli, proprietà strutturali, somme nei sottoalberi e verifiche di bilanciamento.  
La seconda parte raccoglie esercizi sulle tabelle hash, in particolare inserimenti con indirizzamento aperto, doppio hashing e chaining.

L'obiettivo è allenarsi a scrivere soluzioni complete in stile esame, con pseudocodice chiaro, motivazione della correttezza e analisi della complessità.

---

## Stato delle soluzioni

| Esercizio | Stato |
|---|---|
| Domanda 26 — `MaxPath(T)` | [Completato](domanda_26.md) |
| Domanda 27 — `Level(T)` | [Completato](domanda_27.md) |
| Domanda 28 — `IsSumHeap(T)` | [Completato](domanda_28.md) |
| Esercizio 10 — `printFair(T)` | [Completato](esercizio_10.md) |
| Esercizio 11 — `sdegree(T)` | Da completare |
| Esercizio 12 — `bal1(T)` | Da completare |
| Esercizio 13 — `k-bound(T, k)` | Da completare |
| Domanda 29 — Albero binario completo | Da completare |
| Domanda 30 — Massima differenza tra cammini | Da completare |
| Domanda 36 — Predecessore in un ABR | [Completato](pred.md) |
| Domanda 37 — `IsABR(A)` su rappresentazione array | Da completare |
| Domanda 38 — Inserimento in ABR con campo `pred` | Da completare |
| Esercizio 14 — Costruzione di ABR di altezza minima | [Completato](bst.md) |
| Esercizio 15 — Inserimento in ABR con campo `even` | Da completare |
| Esercizio 16 — Stampa ordinata di un intervallo di chiavi | Da completare |
| Domanda 39 — Altezza nera | Da completare |
| Esercizio 17 — Verifica di Red-Black tree | Da completare |


## Testi degli Esercizi

### **Domanda 26**

Dato un albero nel quale i nodi contengono una chiave, si definisca costo di un cammino dalla radice ad una foglia, come la somma delle chiavi dei nodi che compaiono nel cammino. Scrivere una funzione `MaxPath(T)` che opera nel modo seguente. Prende in input un albero binario `T`, con radice `T.root`, e nodi $x$ che hanno come campi `x.k`, `x.l` e `x.r`, ovvero una chiave, il puntatore al figlio sinistro e destro, rispettivamente. Restituisce il costo del cammino di costo massimo dalla radice ad una foglia. Valutarne la complessità.

---

### **Domanda 27**

Realizzare una procedura `Level(T)` che dato un albero binario `T`, con radice `T.root`, e nodi $x$ con campi `x.left`, `x.right` e `x.key`, rispettivamente figlio destro, figlio sinistro e chiave intera, ritorna il numero di nodi per i quali la chiave `x.key` è minore o uguale al livello del nodo (la radice ha livello 0, i suoi figli livello 1 e così via). Valutare la complessità.

---

### **Domanda 28**

Sia `T` un albero binario i cui nodi $x$ hanno i campi `x.left`, `x.right`, `x.key`. L'albero si dice un *sum-heap* se per ogni nodo $x$, la chiave di $x$ è maggiore o uguale sia alla somma delle chiavi nel sottoalbero sinistro che alla somma delle chiavi nel sottoalbero destro.
Scrivere una funzione `IsSumHeap(T)` che dato in input un albero `T` verifica se `T` è un *sum-heap* e ritorna un corrispondente valore booleano. Valutarne la complessità.

---

### **Esercizio 10**

Un nodo $x$ di un albero binario `T` si dice *fair* se la somma delle chiavi nel cammino che conduce dalla radice dell'albero al nodo $x$ (escluso) coincide con la somma delle chiavi nel sottoalbero di radice $x$ (con $x$ incluso). Realizzare un algoritmo ricorsivo `printFair(T)` che dato un albero `T` stampa tutti i suoi nodi *fair*. Supporre che ogni nodo abbia i campi `x.left`, `x.right`, `x.p`, `x.key`. Valutare la complessità dell'algoritmo.

---

### **Esercizio 11**

Sia dato un albero i cui nodi contengono una chiave intera `x.key`, oltre ai campi `x.l`, `x.r` e `x.p` che rappresentano rispettivamente il figlio sinistro, il figlio destro e il padre. Si definisce grado di squilibrio di un nodo il valore assoluto della differenza tra la somma delle chiavi nei nodi foglia del sottoalbero sinistro e la somma delle chiavi dei nodi foglia del sottoalbero destro. Il grado di squilibrio di un albero è il massimo grado di squilibrio dei suoi nodi.
Fornire lo pseudocodice di una funzione `sdegree(T)` che calcola il grado di squilibrio dell'albero `T` (si possono utilizzare funzioni ricorsive di supporto). Valutare la complessità della funzione.

---

### **Esercizio 12**

Si consideri un albero binario `T`, i cui nodi $x$ hanno i campi `x.l`, `x.r`, `x.p` che rappresentano il figlio sinistro, il figlio destro e il padre, rispettivamente. Un cammino è una sequenza di nodi $x_0, x_1, \dots, x_n$ tale che per ogni $i = 1, \dots, n$ vale $x_{i+1}.p = x_i$. Il cammino è detto terminabile se $x_n.l = \text{nil}$ oppure $x_n.r = \text{nil}$. Diciamo che l'albero è 1-bilanciato se tutti i cammini terminabili dalla radice hanno lunghezze che differiscono al più di 1. Scrivere una funzione `bal1(T)` che dato in input l'albero `T` verifica se è 1-bilanciato e ritorna un corrispondente valore booleano. Valutarne la complessità.

---

### **Esercizio 13**

Sia `T` un albero binario i cui nodi $x$ hanno i campi `x.left`, `x.right`, `x.key`. L'albero si dice *k-bounded*, per un certo valore $k$, se per ogni nodo $x$ la somma delle chiavi lungo ciascun cammino da $x$ ad una foglia è minore o uguale a $k$.
Scrivere una funzione `k-bound(T, k)` che dato in input un albero `T` e un valore $k$ verifica se `T` è *k-bounded* e ritorna un corrispondente valore booleano. Valutarne la complessità.

---

### **Domanda 29**

Scrivere una funzione `complete(T)` che dato in input un albero binario verifica se è completo (ovvero ogni nodo interno ha due figli e tutte le foglie hanno la stessa distanza dalla radice).

---

### **Domanda 30**

Scrivere una funzione `diff(T)` che dato in input un albero binario `T` determina la massima differenza di lunghezza tra due cammini che vanno dalla radice ad un sottoalbero vuoto. Ad esempio sull'albero ottenuto inserendo 1, 2 e 3 produce 2, su quello ottenuto inserendo 2, 1, 3 produce 0. Valutarne la complessità.

---

### **Domanda 36**

Realizzare una funzione `pred(x)` che dato in input un nodo $x$, di un albero binario di ricerca `T`, restituisce il predecessore di $x$ (oppure `nil`, se il predecessore non esiste). Come a lezione, supporre che ogni nodo abbia i campi `x.left`, `x.right`, `x.p`, `x.key`.

---

### **Domanda 37**

Scrivere una funzione `IsABR(A)` che dato in input un array di interi `A[1..n]`, interpretato come albero binario (come nel caso degli heap, ogni `A[i]` è un nodo con figlio sinistro e destro `A[2i]` e `A[2i+1]`) verifica se `A` è un albero binario di ricerca. Valutarne la complessità.

---

### **Domanda 38**

Si consideri una variante degli alberi binari di ricerca nella quale i nodi $x$ hanno un campo `x.pred` (predecessore) invece che il campo `x.p` (parent). Realizzare la procedura di `Insert(T, z)` che inserisce un nodo $z$ nell'albero. Valutarne la complessità.

---

### **Esercizio 14**

Realizzare una procedura `BST(A)` che dato un array `A[1..n]` di interi, ordinato in modo crescente, costruisce un albero binario di ricerca di altezza minima che contiene gli elementi di `A` e ne restituisce la radice. Per allocare un nuovo nodo dell'albero si utilizzi una funzione `mknod(k)` che dato un intero $k$ ritorna un nuovo nodo con `x.key = k` e figlio destro e sinistro `x.left = x.right = nil`. Valutarne la complessità.

---

### **Eserizio 15**

Si consideri una estensione degli alberi binari di ricerca nei quali ogni nodo $x$ ha anche un campo booleano `x.even` che vale `true` o `false` a seconda che la somma delle chiavi nel sottoalbero radicato in $x$ sia pari o dispari. Realizzare la procedura `Insert(T, z)` di modo che mantenga correttamente aggiornato anche il campo `even`. Valutarne la complessità.

---

### **Esercizio 16**

Scrivere una funzione `range(T, k1, k2)` che dato un albero binario di ricerca `T` e due interi $k_1$ e $k_2$ tali che $k_1 \le k_2$, stampa, in ordine crescente, tutte le chiavi $k$ contenute nell'albero tali che $k_1 \le k \le k_2$. Valutarne la complessità.

---

### **Domanda 39**

Scrivere una funzione `blackHeight(T)` che dato in input un albero binario di ricerca `T`, i cui nodi $x$ hanno, oltre ai campi `x.key`, `x.left` e `x.right`, hanno un campo `x.col` che può essere B (per "black") oppure R (per "red"), verifica se per ogni nodo, il cammino da quel nodo a qualsiasi foglia contiene lo stesso numero di nodi neri (altezza nera). In caso negativo, restituisce -1, altrimenti restituisce l'altezza nera della radice.

---

### **Esercizio 17**

Scrivere una funzione `RBTree(T)` che dato in input un albero binario di ricerca `T`, i cui nodi $x$, oltre ai campi `x.key`, `x.left` e `x.right`, hanno un campo `x.col` che può essere B (per "black") oppure R (per "red"), verifica se questo è un Red-Black tree. In caso negativo, restituisce -1, altrimenti restituisce l'altezza nera della radice. Valutarne la complessità.
