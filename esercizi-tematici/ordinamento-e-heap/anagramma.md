# Esercizio 7 - Anagramma Binario

Realizzare una funzione `Anagramma(x, y)` che date due stringhe $x$ e $y$ sull'alfabeto $\{0, 1\}$, verifica se $x$ è un anagramma di $y$ restituendo conseguentemente `true` o `false`. Una stringa è vista come un array di caratteri, con lunghezza data dall'attributo `len`. Ad esempio, la stringa $x$ è la sequenza di caratteri $x[1] x[2] \dots x[x.len]$. Valutare la complessità.

---

### i. Idea e Ragionamento

Per definizione, due stringhe sono un anagramma l'una dell'altra se contengono gli stessi caratteri con la stessa frequenza, possibilmente disposti in un ordine diverso (es. "race" e "care").

Siano $x, y$ due stringhe sull’alfabeto $\{0,1\}$. La stringa $x$ è un anagramma di $y$ se contiene lo stesso numero di caratteri $0$ e $1$.
Di conseguenza, se le lunghezze differiscono ($x.len \ne y.len$), non può essere vero che $x$ sia anagramma di $y$.

Se invece $x.len = y.len$, bisogna verificare se hanno le stesse frequenze. Sfruttando il fatto che l'alfabeto è binario, possiamo limitarci a contare il numero di caratteri $1$ di ciascuna stringa usando due variabili locali.
Indicando con $c1_x, c1_y$ il numero di caratteri $1$ e con $c0_x, c0_y$ il numero di caratteri $0$ di ciascuna stringa, se vale $c1_x = c1_y$ (ovvero le due stringhe hanno lo stesso numero di $1$), avranno necessariamente anche lo stesso numero di $0$.

Matematicamente:
$$ c1_x = c1_y \implies c0_x = x.len - c1_x = y.len - c1_y = c0_y $$

---

### ii. Pseudocodice

```text
// restituisce true se x è anagramma di y, false altrimenti
Anagramma(x, y)
    // se le lunghezze sono diverse, non possono essere anagrammi
    if x.len != y.len
        return false

    // contatori per il carattere '1'
    c1_x = 0
    c1_y = 0

    // conteggio in una singola passata
    for i = 1 to x.len
        if x[i] == '1'
            c1_x = c1_x + 1
        if y[i] == '1'
            c1_y = c1_y + 1				 

    // se hanno lo stesso numero di 1, avendo la stessa lunghezza,
    // avranno anche lo stesso numero di 0
    return c1_x == c1_y
```

---

### iii. Complessità

La complessità temporale è direttamente proporzionale alla lunghezza delle stringhe. Assumendo che abbiano la stessa lunghezza $n$ ($n = x.len = y.len$), il ciclo `for` eseguirà esattamente $n$ iterazioni. Ogni iterazione svolge un numero costante di controlli e incrementi $\Theta(1)$.

- **Complessità Temporale:** $T(n) = \Theta(n)$, ovvero lineare.
- **Complessità Spaziale:** $\mathcal{O}(1)$, poiché vengono utilizzate solo due variabili contatore, indipendentemente dalla lunghezza dell'input.
