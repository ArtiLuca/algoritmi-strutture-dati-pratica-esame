# Esercizio 1 — ABR arricchito con numero di foglie

Realizzare un arricchimento degli alberi binari di ricerca che permetta di ottenere per ogni nodo $x$, in tempo costante, il numero delle foglie nel sottoalbero radicato in $x$.
Indicare quali campi occorre aggiungere ai nodi.
Fornire il codice per la funzione `leaves(x)` che restituisce il numero delle foglie nel sottoalbero radicato in $x$ e per la procedura di inserimento di un nodo `insert(T, z)`.
Per entrambe valutare la complessità.

---

### i. Campi Aggiuntivi e Funzione `leaves(x)`

Per ottenere in tempo costante il numero di foglie nel sottoalbero radicato ad un dato nodo $x$, occorre aggiungere un ulteriore campo $x.leaf$, oltre ai campi usuali $x.left, x.right, x.p, x.key$.
Questo nuovo campo $x.leaf$ conterrà il numero di foglie del sottoalbero radicato in $x$. Se $x$ è esso stesso una foglia, $x.leaf$ varrà $1$.

La funzione `leaves(x)` si limita a leggere questo campo, gestendo in sicurezza il caso in cui il nodo passato sia `nil` (restituendo $0$).

```algorithmic
// Restituisce il numero di foglie del sottoalbero radicato in x
leaves(x)
    if x == nil
        return 0
    return x.leaf		
```

**Complessità:** La funzione esegue un semplice controllo e un accesso in memoria, quindi la complessità è $\mathcal{O}(1)$.

---

### ii. Procedura di Inserimento

Ogni nuovo nodo $z$ inserito in un ABR diventa inizialmente una foglia, quindi avrà $z.left = z.right = \text{nil}$ e $z.leaf = 1$.
L’inserimento vero e proprio procede in modo identico a quello standard. La modifica principale per mantenere aggiornato il nuovo campo avviene *dopo* l’inserimento: si risale lungo il cammino dal padre del nodo $z$ appena inserito fino alla radice, aggiornando il contatore delle foglie di ciascun antenato.

Poiché tutti gli antenati di $z$ sono garantiti essere nodi interni (hanno almeno un figlio), vale sempre la relazione:
$$x.leaf = \text{leaves}(x.left) + \text{leaves}(x.right)$$

Questa formula gestisce automaticamente anche il caso in cui $z$ venga agganciato a un nodo $x$ che precedentemente era una foglia: $x.leaf$ passerà dall'avere valore $1$ a valere $1 + 0 = 1$, mantenendo coerente il numero totale di foglie (poiché $z$ è diventato la nuova foglia al posto di $x$).

```algorithmic
Insert(T, z)

    // Setup iniziale del nuovo nodo (che diventa temporaneamente una foglia)
    z.left = nil
    z.right = nil
    z.leaf = 1

    // Fase 1: Ricerca della posizione di inserimento
    x = T.root
    y = nil
    while x != nil
        y = x
        if z.key < x.key
            x = x.left
        else
            x = x.right		

    // Fase 2: Inserimento standard
    z.p = y
    if y == nil
        T.root = z
    else if z.key < y.key
        y.left = z
    else
        y.right = z

    // Fase 3: Risalita per l'aggiornamento del campo "leaf"
    x = z.p
    while x != nil						 				
        x.leaf = leaves(x.left) + leaves(x.right)
        x = x.p		
```

**Complessità:**

- **Tempo:** La fase di discesa per trovare la posizione richiede tempo $\mathcal{O}(h)$, dove $h$ è l'altezza dell'albero. L'ulteriore fase di risalita ripercorre al massimo lo stesso cammino all'indietro, impiegando anch'essa $\mathcal{O}(h)$ operazioni a costo costante. La complessità temporale complessiva resta quindi $T(n) = \mathcal{O}(h)$.

- **Spazio:** L'algoritmo è puramente iterativo e utilizza solo puntatori ausiliari, garantendo una complessità spaziale $\mathcal{O}(1)$.
