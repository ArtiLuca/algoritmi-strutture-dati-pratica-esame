# Esercizio 1 - Ricerca Tripla (Variante 3SUM)

Realizzare una procedura `triplet(A)` che dato un array $A[1\dots n]$ di interi verifica se esistono tre indici, non necessariamente distinti, $i$, $j$ e $k$ tali che $A[i] + A[j] = A[k]$.
Fornire lo pseudocodice, motivare la correttezza della soluzione e valutarne la complessità.

---

### i. Idea e Pseudocodice

Una possibile soluzione al problema richiede prima che l’array $A[1\dots n]$ venga ordinato in senso crescente, con un qualsiasi algoritmo di comparison-sort (ad esempio `MergeSort`). Questo viene indicato semplicemente con una chiamata generica `Sort(A)` che ordina $A$ con un costo $\Theta(n \log n)$.

Dopo l’ordinamento possiamo cercare la tripla $(i,j,k)$ tale che $A[i] + A[j] = A[k]$ usando la tecnica nota come "two pointers" (due puntatori). Si effettua una ricerca per ogni valore di $k \in 1\dots n$, usando gli indici $i, j$ per verificare se abbiamo trovato la tripla oppure quale delle due estremità possiamo essere sicuri di "scartare".

```algorithmic
// restituisce true se trova tripla (i,j,k) t.c. A[i] + A[j] = A[k]
// altrimenti, restituisce false se questa non esiste
triplet(A)
    // ordinamento usando comparison-sort (es: MergeSort)
    Sort(A)
		
    for k = 1 to n 
        i = 1
        j = n
				
        // uso '<=' anziché '<' per coprire il caso di "indici non necessariamente distinti"
        while i <= j
            sum = A[i] + A[j]
            
            // se ho trovato la tripla, ho finito
            if sum == A[k]
                return true
            // se somma corrente troppo piccola, incremento i		
            else if sum < A[k]
                i = i + 1
            // altrimenti, somma troppo grande, decremento j		
            else
                j = j - 1
				
    // se dopo aver provato ogni possibile combinazione la tripla non esiste		
    return false				
```

---

### ii. Correttezza

La correttezza si basa sull’ordinamento iniziale dell’array $A[1\dots n]$. Questo ci permette di esplorare in modo mirato e logico le combinazioni di indici $i$ e $j$ per ogni $k=1\dots n$.

Per ogni $k$ fissato, si entra in un ciclo `while` da cui si può uscire negativamente solamente quando $i > j$. Ovvero, quando abbiamo provato (o escluso con certezza) ogni possibile combinazione per quel $k$, includendo il caso $i=j$. 

Ad ogni iterazione si valuta la somma corrente $A[i] + A[j]$:

**Caso 1: Somma Esatta**
Se $A[i] + A[j] = A[k]$, abbiamo trovato la tripla $(i,j,k)$ e si restituisce correttamente `true`.

**Caso 2: Somma troppo piccola**
Se $A[i] + A[j] < A[k]$, la somma non è sufficiente. Poiché l'array è ordinato in senso crescente, sappiamo che $\forall j^{*} \le j$ varrà la seguente disuguaglianza:

$$ A[i] + A[j^{*}] \le A[i] + A[j] < A[k] $$

L’elemento $A[i]$ accoppiato a qualsiasi elemento disponibile produrrà sempre una somma troppo piccola e può essere definitivamente scartato. Perciò, si incrementa $i = i + 1$.

**Caso 3: Somma troppo grande**
In modo speculare, se $A[i] + A[j] > A[k]$, la somma supera il target. Sappiamo che $\forall i^{*} \ge i$ varrà:

$$ A[i^{*}] + A[j] \ge A[i] + A[j] > A[k] $$

L’elemento $A[j]$ è troppo grande per produrre la somma desiderata e può essere scartato. Perciò, si decrementa $j = j - 1$.

L’algoritmo prova quindi in modo esaustivo ma efficiente ogni possibile indice $k = 1\dots n$, scartando gli elementi che violano il limite grazie all'ordinamento. Se la tripla esiste, l’algoritmo la trova; altrimenti, restituisce `false` in totale sicurezza.

---

### iii. Complessità

La complessità temporale è data dalla fase iniziale di ordinamento, che costa $\Theta(n \log n)$, e dai due cicli annidati successivi.
Il ciclo esterno `for` viene eseguito $n$ volte. Al suo interno, il ciclo `while` fa convergere gli indici $i$ e $j$ (che distano inizialmente $n-1$ posizioni) in un massimo di $n$ passi. La fase di ricerca costa quindi $\mathcal{O}(n^2)$.

Complessivamente: $T(n) = \Theta(n \log n) + \mathcal{O}(n^2) = \Theta(n^2)$.
La complessità spaziale dipenderà unicamente dall'algoritmo di ordinamento scelto (es. $\mathcal{O}(n)$ per il MergeSort standard, o $\mathcal{O}(1)$ se si usasse un Heapsort).
