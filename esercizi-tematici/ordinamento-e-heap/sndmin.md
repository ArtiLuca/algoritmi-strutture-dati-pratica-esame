# Esercizio 22 - Secondo Minimo in un Min-Heap

Scrivere una funzione `sndmin(A)` che, dato in input un array $A$ organizzato a $\text{min-heap}$, restituisce il successore della radice, ovvero il minimo elemento dello heap maggiore della radice. Se un tale elemento non esiste genera un errore. Assumere che $A$ sia non vuoto e gli elementi in $A$ siano tutti distinti.

---

### i. Idea e Ragionamento

In un $\text{min-heap}$, la proprietà fondamentale garantisce che il genitore sia sempre minore o uguale ai suoi figli. Di conseguenza, la radice $A[1]$ contiene sempre il valore minimo assoluto dello heap.

Per la medesima proprietà, qualsiasi elemento situato a profondità $\ge 2$ (ovvero dai nipoti della radice in giù) sarà strettamente maggiore del proprio genitore situato al livello 1. Pertanto, il secondo elemento più piccolo dell'intero heap deve necessariamente trovarsi tra i figli diretti della radice, ovvero in posizione $A[2]$ (figlio sinistro) oppure $A[3]$ (figlio destro).

Consideriamo le possibili dimensioni dell'array ($A.size$):
- Se $A.size \le 1$: lo heap contiene solo la radice (o è vuoto), quindi il successore non esiste e si genera un errore.
- Se $A.size = 2$: lo heap possiede solo il figlio sinistro, che sarà obbligatoriamente il secondo minimo.
- Se $A.size \ge 3$: lo heap possiede sia il figlio sinistro che quello destro. Il secondo minimo sarà il minimo tra $A[2]$ e $A[3]$.

---

### ii. Pseudocodice

```text
// restituisce il secondo minimo di un min-heap A, oppure genera un errore
sndmin(A)
    // caso base: non esiste un successore della radice
    if A.size <= 1
        return ERROR

    // esiste solo il figlio sinistro
    else if A.size == 2
        return A[2]

    // esistono entrambi i figli (A.size >= 3)
    else
        return min(A[2], A[3])
```

---

### iii. Complessità

L'algoritmo effettua solamente un numero costante di controlli sulle dimensioni dell'array ed eventualmente un confronto tra due elementi a posizioni fisse ($A[2]$ e $A[3]$).

Non viene effettuata alcuna visita dell'albero o ciclo.

- **Complessità Temporale:** $T(n) = \Theta(1)$ (tempo costante).
- **Complessità Spaziale:** $\mathcal{O}(1)$ (spazio costante, nessuna struttura ausiliaria richiesta).
