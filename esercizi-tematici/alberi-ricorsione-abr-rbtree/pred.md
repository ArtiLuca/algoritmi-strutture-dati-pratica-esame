# Domanda 36

Realizzare una funzione `pred(x)` che dato in input un nodo $x$ di un albero binario di ricerca $T$, restituisce il predecessore di $x$ (oppure `nil`, se il predecessore non esiste). Come a lezione, supporre che ogni nodo abbia i campi $x.left$, $x.right$, $x.p$, $x.key$.

---

### i. Idea e Logica

Dato un albero binario di ricerca (ABR) $T$ e un suo nodo $x$, il predecessore equivale all’elemento con chiave massima tra quelli con chiave strettamente più piccola di $x$ (assumendo che siano chiavi tutte distinte). In altre parole, il predecessore di $x$ è il nodo che lo precede esattamente in una visita *in-order*.

La ricerca si divide in due casi mutuamente esclusivi:
1. **Se $x$ ha un sottoalbero sinistro:** il predecessore si trova scendendo nel figlio sinistro e poi cercando il valore massimo di quel sottoalbero (ovvero andando sempre a destra finché possibile).
2. **Se $x$ non ha un sottoalbero sinistro:** il predecessore si trova risalendo l'albero attraverso i puntatori al padre ($x.p$). Nello specifico, è il primo antenato per il quale il nodo $x$ (o uno dei suoi antenati) si trova nel sottoalbero destro. Si risale finché non si incontra un nodo che è figlio destro del proprio padre.

Serve quindi una procedura d'appoggio `Max(x)` che restituisce il nodo con chiave massima per il sottoalbero radicato in $x$.

---

### ii. Pseudocodice

```text
// restituisce il nodo con chiave massima del sottoalbero radicato in x
// (se x e' nil, non entra nel ciclo o va protetta con un controllo)
Max(x)
    while x.right != nil
        x = x.right
    return x

// restituisce il predecessore di x
pred(x)
    // Caso 1: il predecessore e' nel sottoalbero sinistro
    if x.left != nil
        return Max(x.left)

    // Caso 2: il predecessore e' un antenato
    else
        y = x.p

        // Risalgo l'albero finche' sono un figlio sinistro.
        // Mi fermo quando divento un figlio destro o arrivo alla radice (y == nil)
        while y != nil and x == y.left
            x = y
            y = y.p

        return y
```

---

### iii. Complessità

- **Complessità Temporale:** Entrambe le procedure `Max(x)` e `pred(x)` eseguono percorsi che scendono o risalgono l'albero seguendo dei semplici puntatori. Nel caso pessimo, il percorso tracciato può attraversare tutti i livelli dell'albero dalla radice alla foglia più profonda. Quindi la complessità temporale è proporzionale all’altezza dell’albero:

$$
\mathcal{O}(h)
$$

Nel caso di un ABR ben bilanciato avremo $h = \Theta(\log n)$, mentre nel caso pessimo di un ABR degenere (simile a una lista concatenata) avremo $h = \Theta(n)$.

- **Complessità Spaziale:** Le procedure sono puramente iterative e usano solo un paio di puntatori d'appoggio, non richiedendo alcuno spazio aggiuntivo sullo stack per la ricorsione. La complessità spaziale è pertanto $\mathcal{O}(1)$.
