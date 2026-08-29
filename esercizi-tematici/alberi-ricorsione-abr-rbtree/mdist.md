# Esercizio 1 — Distanza minima in un albero binario di ricerca

Realizzare una funzione `mdist(T, v)` che, dato un albero binario di ricerca $T$ e una chiave $v$, restituisca un nodo $x$ di $T$ la cui chiave abbia distanza minima da $v$, ovvero tale che il valore $|x.key - v|$ sia minimo.
Fornire lo pseudocodice, la complessità e una giustificazione della correttezza.

Ad esempio, dato il seguente albero:
```text
              10
             /  \
            5    20
           / \   / \
          2   6 15  30
               \    /
                9  25
```
la funzione `mdist(T, 8)` restituisce il nodo con chiave 9, mentre `mdist(T, 28)` restituisce il nodo con chiave 30.

---

### i. Idea e Logica

Per questo esercizio possiamo usare una sorta di "pruning" per cercare il nodo $x \in T$ tale che $|x.key - v|$ sia minimo. Nel caso $T$ sia vuoto si restituisce `nil`. Altrimenti, possiamo sfruttare le proprietà degli ABR per cercare il minimo, utilizzando due variabili locali `bestNode` e `bestDist` per tenere traccia del nodo migliore e della distanza minima trovata durante la discesa.
In particolare, all’inizio impostiamo `bestNode = T.root` e `bestDist = |T.root.key - v|`.

Possiamo distinguere tre casi di navigazione:
- **Caso 1:** $x.key == v$; in questo caso restituiamo subito $x$ essendo che non può esistere un minimo migliore.
- **Caso 2:** $v < x.key$; in questo caso ci spostiamo nel sottoalbero sinistro.
- **Caso 3:** $v > x.key$; analogamente, ci spostiamo nel sottoalbero destro.

Ad ogni spostamento del nodo corrente confrontiamo la distanza $|x.key - v|$ e aggiorniamo entrambe le variabili locali nel caso in cui abbiamo trovato un minimo migliore.

---

### ii. Pseudocodice

```algorithmic
// restituisce il nodo x tale che |x.key - v| sia minimo
// restituisce nil se T e' vuoto
mdist(T, v)

    // se T e' vuoto
    if T.root == nil
        return nil

    x = T.root
    // altrimenti, impostiamo minimi iniziali
    bestNode = x
    bestDist = |x.key - v|

    // applichiamo proprieta' ABR per trovare il minimo
    while x != nil

        // verifico se ho trovato un minimo migliore
        currentDist = |x.key - v|
        if currentDist < bestDist
            bestDist = currentDist
            bestNode = x

        // caso 1: non esiste minimo migliore
        if x.key == v
            return x

        // caso 2: scartiamo sottoalbero destro
        else if v < x.key
            x = x.left

        // caso 3: scartiamo sottoalbero sinistro
        else // v > x.key
            x = x.right				  

    // fine del ciclo
    return bestNode	  			
```

---

### iii. Correttezza

La correttezza dell’algoritmo `mdist(T, v)` si può dimostrare usando le proprietà degli ABR e analizzando i tre casi separatamente.

Se $T.root == \text{nil}$ allora $T$ è vuoto e quindi è corretto restituire `nil`. Altrimenti, si impostano `bestNode` e `bestDist` usando la radice per i loro valori iniziali e poi si entra nel ciclo `while`, dal quale si esce solamente quando abbiamo percorso un intero cammino radice-foglia, in base ai tre casi e alle proprietà degli ABR:

- **Caso 1:** se abbiamo $x.key == v$ allora non esiste un minimo migliore, essendo che $|x.key - v| = 0$, e quindi è corretto restituire immediatamente il nodo $x$.
- **Caso 2:** se $v < x.key$ allora possiamo scartare l’intero sottoalbero destro e spostarci a $x.left$. Questo è corretto perché se $v < x.key \implies v < y.key$ per ogni nodo $y$ nel sottoalbero $x.right$ (per definizione di ABR, ogni elemento $y$ a destra sarà tale che $y.key \ge x.key > v$). Di conseguenza, il minimo di sicuro non si può trovare in questo sottoalbero.
- **Caso 3:** se $v > x.key$, in modo speculare, vale che $v > y.key$ per ogni nodo $y$ nel sottoalbero $x.left$ (per definizione $y.key \le x.key < v$). Anche in questo caso, il minimo di sicuro non si può trovare nel sottoalbero sinistro.

Dopo aver correttamente verificato il minimo oppure scartato un sottoalbero per il quale siamo certi non si possa trovare di meglio, confrontiamo il nodo corrente con il minimo trovato finora, aggiornandolo se ne troviamo uno migliore. Quando si esce dal ciclo `while`, abbiamo percorso un intero cammino fino a una foglia, usando le proprietà degli ABR per spostarci sempre nel sottoalbero nel quale si può trovare un minimo possibilmente migliore di quello trovato in precedenza.
Quindi alla fine l’algoritmo restituisce correttamente il nodo tale che $|x.key - v|$ sia minimo.

---

### iv. Complessità

- **Complessità Temporale:** L’algoritmo `mdist(T, v)` scende lungo esattamente un cammino dalla radice verso una foglia e quindi avrà complessità $T(n) = \mathcal{O}(h)$ nel caso peggiore, oppure $\Omega(1)$ nel caso migliore fortunato in cui $T.root.key == v$. In generale, la complessità asintotica è $T(n) = \mathcal{O}(h)$.
- **Complessità Spaziale:** Essendo l'algoritmo puramente iterativo e utilizzando solo un numero costante di variabili ausiliarie, la complessità spaziale è $\mathcal{O}(1)$.
