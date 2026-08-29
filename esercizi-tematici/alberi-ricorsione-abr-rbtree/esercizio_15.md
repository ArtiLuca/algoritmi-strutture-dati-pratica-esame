# Esercizio 15 — ABR arricchito con parità della somma

Si consideri una estensione degli alberi binari di ricerca nei quali ogni nodo $x$ ha anche un campo booleano $x.even$ che vale `true` o `false` a seconda che la somma delle chiavi nel sottoalbero radicato in $x$ sia pari o dispari. Realizzare la procedura `Insert(T, z)` di modo che mantenga correttamente aggiornato anche il campo $even$. Valutarne la complessità.

---

### i. Idea e Logica

Il nuovo nodo $z$ da inserire viene posizionato inizialmente come una foglia. Il valore del suo campo `even` dipenderà unicamente dalla sua chiave: sarà `true` se $z.key \mod 2 == 0$, altrimenti `false`.

Per mantenere aggiornati i campi `even` del resto dell'albero, possiamo sfruttare l'aritmetica modulare direttamente durante la fase di discesa per la ricerca della posizione di inserimento.
Quando inseriamo $z$, la chiave $z.key$ andrà a sommarsi al totale di ogni sottoalbero radicato negli antenati di $z$.
- Se $z.key$ è **pari**, la parità della somma dei sottoalberi attraversati non cambia.
- Se $z.key$ è **dispari**, la parità della somma dei sottoalberi attraversati si inverte.

Quindi, per mantenere aggiornato l’ABR in modo efficiente, possiamo calcolare se $z$ è dispari all'inizio e, durante la fase di discesa, invertire il valore booleano di $x.even$ per ogni nodo visitato (eseguendo un semplice `!x.even`). Questo approccio *top-down* evita del tutto la necessità di scrivere codice aggiuntivo per risalire l'albero dopo l'inserimento.

---

### ii. Pseudocodice

```text
Insert(T, z)

    // Setup iniziale del nuovo nodo come foglia
    z.left = nil
    z.right = nil
    z.even = (z.key mod 2 == 0)

    // Flag per sapere se dobbiamo invertire la parita' degli antenati
    isOdd = (z.key mod 2 != 0)

    x = T.root
    y = nil

    // Fase di discesa e aggiornamento top-down
    while x != nil				
        y = x

        // se la chiave da inserire e' dispari, inverto la parita' del sottoalbero corrente
        if isOdd == true
            x.even = !x.even

        // proseguo con le normali regole di ricerca ABR
        if z.key < x.key
            x = x.left
        else
            x = x.right		 		  

    // Fase di aggancio del nuovo nodo
    z.p = y
    if y == nil
        T.root = z
    else if z.key < y.key
        y.left = z
    else
        y.right = z										
```

---

### iii. Complessità

- **Complessità Temporale:** L'inserimento visita esattamente un cammino dalla radice fino alla posizione di inserimento foglia. L'aggiornamento del campo `even` viene effettuato eseguendo una singola istruzione booleana $\Theta(1)$ per ogni nodo visitato lungo questo cammino, senza iterazioni aggiuntive. La complessità temporale rimane quindi invariata rispetto alla procedura standard, ovvero $T(n) = \mathcal{O}(h)$, dove $h$ è l'altezza dell'albero.
- **Complessità Spaziale:** L'algoritmo è iterativo e utilizza un numero costante di variabili di supporto, garantendo una complessità spaziale pari a $\mathcal{O}(1)$.
