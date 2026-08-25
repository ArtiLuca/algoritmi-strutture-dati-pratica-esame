# Domanda 28

Sia $T$ un albero binario i cui nodi $x$ hanno i campi $x.left, x.right, x.key$. L'albero si dice un **sum-heap** se per ogni nodo $x$, la chiave di $x$ è maggiore o uguale sia alla somma delle chiavi nel sottoalbero sinistro che alla somma delle chiavi nel sottoalbero destro.

Scrivere una funzione `IsSumHeap(T)` che dato in input un albero $T$ verifica se $T$ è un sum-heap e ritorna un corrispondente valore booleano. Valutarne la complessità.

---

### i. Idea e Logica

Per verificare se $x$ è la radice di un sum-heap valido, non basta controllare la proprietà sulla chiave, ma occorre conoscere due informazioni per ciascuno dei suoi sottoalberi:
1. Se il sottoalbero è a sua volta un sum-heap valido (booleano).
2. La somma totale delle chiavi contenute nel sottoalbero (intero).

Per evitare di ricalcolare la somma delle chiavi separatamente (il che degraderebbe le prestazioni), la strategia migliore consiste nell'utilizzare una procedura ricorsiva che restituisca una coppia $(b, s)$ composta da:
- Un valore booleano $b$ che indica se il sottoalbero radicato in $x$ è un sum-heap valido.
- Un valore intero $s$ che rappresenta la somma di tutte le chiavi nel sottoalbero radicato in $x$ (inclusa la chiave di $x$).

La funzione principale `IsSumHeap(T)` agirà da semplice wrapper che estrae la componente booleana dal risultato restituito dalla radice.

---

### ii. Pseudocodice

```text
// Wrapper principale
// restituisce true se T e' un sum-heap, false altrimenti
IsSumHeap(T)
    if T.root == nil
        return true

    (ok, sum) = sumHeapRec(T.root)
    return ok

// Procedura ricorsiva: verifica se x e' radice di un sum-heap
// Restituisce una coppia (bool, int): (sum-heap valido?, somma totale chiavi)
sumHeapRec(x)

    // Caso base: un sottoalbero vuoto e' un sum-heap triviale con somma 0
    if x == nil
        return (true, 0)

    else
        // Ricorro sul sottoalbero sinistro
        (leftValid, sumLeft) = sumHeapRec(x.left)
        // Ricorro sul sottoalbero destro
        (rightValid, sumRight) = sumHeapRec(x.right)

        // Condizione di validita' per il nodo corrente x:
        // - La chiave deve essere >= della somma delle chiavi del sottoalbero sinistro
        // - La chiave deve essere >= della somma delle chiavi del sottoalbero destro
        // - Entrambi i sottoalberi devono essere a loro volta sum-heap validi
        ok = (x.key >= sumLeft) and (x.key >= sumRight) and leftValid and rightValid

        // Somma aggiornata delle chiavi del sottoalbero corrente
        sum = x.key + sumLeft + sumRight

        return (ok, sum)
```

---

### iii. Complessità

- **Complessità Temporale:** L'algoritmo visita ciascun nodo dell'albero esattamente una volta in modalità post-order ed esegue un numero costante $\Theta(1)$ di operazioni per ciascun nodo (confronti e somme). Dunque la complessità temporale è:

$$
T(n) = \Theta(n)
$$

- **Complessità Spaziale:** Lo spazio di memoria ausiliario è occupato esclusivamente dallo stack delle chiamate ricorsive, ed è pari all'altezza dell'albero $\mathcal{O}(h)$ (ovvero $\mathcal{O}(n)$ nel caso pessimo di albero degenere e $\mathcal{O}(\log n)$ nel caso ottimo di albero bilanciato).
