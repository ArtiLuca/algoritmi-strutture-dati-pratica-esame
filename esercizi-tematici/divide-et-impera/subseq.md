# Esercizio 19 - Sottosequenza Ricorsiva

Scrivere una funzione ricorsiva `subseq(X, Y, m, n)` che date due sequenze `X[1..m]` e `Y[1..n]`, di lunghezza $m$ e $n$ rispettivamente, verifica se `X` è una sottosequenza di `Y` e restituisce un valore booleano conseguente. Valutarne la complessità.

---

### i. Idea e Ragionamento

Siano $X = \langle x_1x_2\dots x_m \rangle$ e $Y = \langle y_1y_2 \dots y_n \rangle$ due stringhe. Diciamo che $X$ è sottosequenza di $Y$ se esiste una successione di indici strettamente crescente $1 \le i_1 < i_2 < \dots < i_m \le n$ tale che $x_j = y_{i_j}$ per ogni $1 \le j \le m$.

Possiamo risolvere il problema operando in stile "divide-et-impera" analizzando i suffissi (o prefissi) delle stringhe e facendo le seguenti osservazioni:

- **Caso base 1:** Se $m = 0$, $X$ è la stringa vuota $\varepsilon$. La stringa vuota è sottosequenza di qualsiasi stringa per definizione, quindi restituiamo `true`.
- **Caso base 2:** Se $n = 0$ (e $m > 0$), $Y$ è la stringa vuota $\varepsilon$. Una stringa non vuota non può essere sottosequenza di una stringa vuota, quindi restituiamo `false`.
- **Passo Ricorsivo (Match):** Se troviamo che gli ultimi caratteri coincidono ($x_m = y_n$), allora il problema si riduce a verificare se il prefisso $X_{m-1}$ è sottosequenza del prefisso $Y_{n-1}$.
- **Passo Ricorsivo (Scarto):** Se invece $x_m \ne y_n$, l'ultimo carattere di $Y$ è inutile per completare $X$. Ci riduciamo quindi a cercare l'intera stringa $X_m$ nel prefisso $Y_{n-1}$.

---

### ii. Pseudocodice

```algorithmic
// restituisce true se X è sottosequenza di Y
subseq(X, Y, m, n)

    // se X è vuota, è sempre sottosequenza
    if m == 0
        return true

    // se Y è vuota (ma X non lo è), X non può essere sottosequenza		
    if n == 0		
        return false

    // se gli ultimi due caratteri coincidono, mi riconduco a (m-1, n-1)		
    if X[m] == Y[n]
        return subseq(X, Y, m - 1, n - 1)

    // se non coincidono, scarto l'ultimo carattere di Y e mi riconduco a (m, n-1)
    else 				
        return subseq(X, Y, m, n - 1)
```

---

### iii. Complessità

Nonostante il numero totale di possibili sottosequenze di $Y$ sia $\sum_{k=0}^{n} \binom{n}{k} = 2^n$, l'algoritmo non esplora l'intero spazio delle combinazioni.

Ad ogni chiamata ricorsiva, la dimensione del problema (in particolare la lunghezza $n$ della stringa $Y$) decresce rigorosamente di $1$, mentre $m$ decresce di $1$ oppure rimane invariato.
Il caso pessimo si verifica quando si esaurisce l'intera stringa $Y$ (ovvero si arriva al caso base $n = 0$), il che richiede esattamente $n$ chiamate ricorsive. Il caso migliore si verifica invece se $m=0$ fin dall'inizio, con tempo $\Theta(1)$.

- **Complessità Temporale:** Il tempo di esecuzione al caso pessimo è lineare, ovvero $\mathcal{O}(n)$.
- **Complessità Spaziale:** Lo spazio aggiuntivo è dovuto esclusivamente alla memoria allocata sullo stack per le chiamate ricorsive. Nel caso pessimo ci saranno $n$ record di attivazione impilati, risultando in una complessità spaziale di $\mathcal{O}(n)$.
