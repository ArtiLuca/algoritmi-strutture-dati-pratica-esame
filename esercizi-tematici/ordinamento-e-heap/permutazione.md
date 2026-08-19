# Esercizio 9 - Permutazione di cifre

Scrivere una funzione `perm(m, n)` che dati due numeri interi $m$ e $n$, maggiori o uguali di 0, verifica se uno dei due numeri può essere ottenuto permutando le cifre dell'altro. Attenzione al ruolo degli zeri impliciti (es. 150 è permutazione di 51, dato che $51 = 051$). Valutarne la complessità.

---

### i. Idea e Ragionamento

Prendendo ispirazione dal Counting Sort, l'idea è utilizzare un array delle frequenze $C[0\dots 9]$ per tenere traccia delle cifre lette.
Si utilizza un unico ciclo `while` che continua finché almeno uno dei due numeri è maggiore di 0.

Ad ogni iterazione, si estraggono le cifre **meno significative** (le unità) dei due numeri usando l'operatore modulo 10, e le si "rimuove" dividendo i numeri per 10.
- Per il numero $m$, incrementiamo il contatore corrispondente alla sua cifra.
- Per il numero $n$, decrementiamo il contatore corrispondente alla sua cifra.

Il trucco elegante per gestire le lunghezze diverse (gli zeri impliciti iniziali) è questo: se uno dei due numeri si azzera prima dell'altro, il ciclo continua per svuotare il numero più lungo. Per il numero già azzerato, assumiamo implicitamente di aver letto la cifra $0$, andando ad aggiornare direttamente $C[0]$.
Alla fine, se i numeri sono permutazioni perfette, tutti gli incrementi e decrementi si annulleranno a vicenda, lasciando l'array $C$ riempito esclusivamente di zeri.

---

### ii. Pseudocodice

```algorithmic
// restituisce true se m e n sono uno la permutazione dell'altro
perm(m, n)
    // all'inizio C contiene tutti 0
    allocate C[0...9]
    for i = 0 to 9
        C[i] = 0

    // itero finché c'è almeno una cifra da analizzare in uno dei due
    while (m > 0) or (n > 0)

        // gestisco il numero m
        if m > 0
            d = m mod 10
            C[d] = C[d] + 1
            m = floor(m / 10)
        else
            // se m è finito, estraggo implicitamente uno 0
            C[0] = C[0] + 1

        // gestisco il numero n
        if n > 0
            d = n mod 10
            C[d] = C[d] - 1
            n = floor(n / 10)
        else
            // se n è finito, estraggo implicitamente uno 0
            C[0] = C[0] - 1						

    // verifico che l'array delle frequenze si sia completamente azzerato
    for i = 0 to 9
        if C[i] != 0
            return false

    return true										
```

---

### iii. Complessità

Sia $N = \max(\text{length}(m), \text{length}(n))$ il numero massimo di cifre tra i due numeri interi in input. (Nota: matematicamente, $N \approx \log_{10}(\max(m, n))$).

*   **Complessità Temporale:** Il ciclo `while` compie esattamente $N$ iterazioni. L'inizializzazione e il controllo finale dell'array $C$ richiedono sempre $10$ operazioni costanti. La complessità temporale è proporzionale al numero di cifre, quindi $\Theta(N)$. Rispetto al *valore* dei numeri, la complessità è $\Theta(\log(\max(m, n)))$.
*   **Complessità Spaziale:** Viene utilizzato un array $C$ di dimensione fissa $k = 10$, che non dipende dall'input. Pertanto, la complessità spaziale è $\Theta(1)$.
