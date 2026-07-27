# Esercizio 2 — Programmazione dinamica bottom-up

[← Torna all'appello](README.md)

## Testo

**Esercizio 2 (8 punti)**

Date due stringhe `X = <x_1, x_2, ..., x_m>` e
`Y = <y_1, y_2, ..., y_n>`, si consideri la seguente quantità `ell(i, j)`,
definita per ogni coppia di valori `i, j` con `0 <= i <= m` e `0 <= j <= n`:

```text
ell(i, j) =
    1                                      se i = 0 oppure j = 0
    3 * ell(i, j - 1)                      se i,j > 0 e x_i = y_j
    2 * ell(i - 1, j - 1) - ell(i - 1, j)  se i,j > 0 e x_i != y_j
```

Si vuole calcolare la quantità:

```text
q = max { ell(i, j) : 0 <= i <= m, 0 <= j <= n }.
```

**(a)** Scrivere un algoritmo bottom-up per il calcolo di `q`.

**(b)** Determinare la complessità esatta dell'algoritmo, supponendo che le
uniche operazioni di costo unitario e non nullo siano i confronti tra caratteri.

---

## Soluzione

## Punto (a)

Usiamo una tabella `L[0...m, 0...n]`, dove `L[i, j]` rappresenta il valore della
quantità `ell(i, j)`.

La ricorrenza dipende solo da valori già disponibili se riempiamo la tabella
riga per riga:

- `L[i, j - 1]` si trova nella stessa riga, ma in una colonna precedente;
- `L[i - 1, j - 1]` e `L[i - 1, j]` si trovano nella riga precedente.

Quindi possiamo riempire la tabella con `i` crescente e, per ogni `i`, con `j`
crescente.

Durante il riempimento manteniamo anche il valore massimo `q`.

---

## Pseudocodice

```text
compute_q(X, Y)
    m = length(X)
    n = length(Y)

    allocate L[0...m, 0...n]

    q = 1

    for i = 0 to m
        L[i, 0] = 1

    for j = 0 to n
        L[0, j] = 1

    for i = 1 to m
        for j = 1 to n
            if X[i] == Y[j]
                L[i, j] = 3 * L[i, j - 1]
            else
                L[i, j] = 2 * L[i - 1, j - 1] - L[i - 1, j]

            if L[i, j] > q
                q = L[i, j]

    return q
```

Nota: qui gli indici delle stringhe sono scritti in stile `1..m` e `1..n`,
coerentemente con la ricorrenza del testo.

---

## Punto (b): complessità esatta

Le uniche operazioni di costo unitario e non nullo sono i confronti tra
caratteri.

Un confronto tra caratteri viene eseguito esattamente una volta per ogni coppia
`(i, j)` con:

```text
1 <= i <= m
1 <= j <= n
```

Infatti, per ogni cella interna della tabella, l'algoritmo controlla se:

```text
X[i] == Y[j]
```

Il numero esatto di confronti è quindi:

```text
sum_{i=1}^{m} sum_{j=1}^{n} 1 = m * n
```

Quindi la complessità esatta, contando solo i confronti tra caratteri, è:

```text
m * n
```
