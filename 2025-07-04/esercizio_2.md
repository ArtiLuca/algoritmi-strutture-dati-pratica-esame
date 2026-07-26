# Esercizio 2 — Memoizzazione e complessità al caso migliore

[← Torna all'appello](README.md)

## Testo

**Esercizio 2 (9 punti)**

Data una stringa `X = x_1, x_2, ..., x_n`, si consideri la seguente quantità
`l(i, j)`, definita per `1 <= i <= j <= n`:

```text
l(i, j) =
    1                                    se i = j
    2                                    se i = j - 1
    2 + l(i + 1, j - 1)                  se i < j - 1 e x_i = x_j
    sum_{k=i}^{j-1}(l(i,k) + l(k+1,j))   se i < j - 1 e x_i != x_j
```

**(1)** Scrivere una coppia di algoritmi `INIT_L(X)` e `REC_L(i, j)` per il
calcolo memoizzato di `l(1, n)`.

**(2)** Si determini la complessità al caso migliore `T_best(n)` supponendo che
le uniche operazioni di costo unitario e non nullo siano i confronti tra
caratteri.

---

## Soluzione

## Punto (1)

Usiamo una tabella `L[1...n, 1...n]`, dove `L[i, j]` rappresenta il valore della
ricorrenza `l(i, j)`.

La procedura `INIT_L(X)`:

1. calcola la lunghezza `n` della stringa;
2. gestisce direttamente i casi base `n = 1` e `n = 2`;
3. alloca la tabella `L`;
4. inizializza i casi base;
5. inizializza a `0` gli stati non ancora calcolati;
6. invoca la procedura ricorsiva `REC_L(X, 1, n)`.

Uso il valore `0` come sentinella per indicare che un valore non è ancora stato
calcolato. Questo è sicuro perché tutti i valori della ricorrenza sono positivi.

Ho scelto di scrivere la procedura ricorsiva come `REC_L(X, i, j)`, passando
anche la stringa `X`, perché la procedura deve confrontare i caratteri `X[i]` e
`X[j]`.

---

## Pseudocodice

```text
INIT_L(X)
    n = length(X)

    if n == 1
        return 1

    if n == 2
        return 2

    allocate L[1...n, 1...n]

    // casi base
    for i = 1 to n - 1
        L[i, i] = 1
        L[i, i + 1] = 2

    L[n, n] = 1

    // stati non ancora calcolati
    for i = 1 to n - 2
        for j = i + 2 to n
            L[i, j] = 0

    return REC_L(X, 1, n)


REC_L(X, i, j)
    if L[i, j] == 0
        if X[i] == X[j]
            L[i, j] = 2 + REC_L(X, i + 1, j - 1)

        else
            L[i, j] = 0

            for k = i to j - 1
                L[i, j] =
                    L[i, j] +
                    REC_L(X, i, k) +
                    REC_L(X, k + 1, j)

    return L[i, j]
```

Poiché si usa memoizzazione, ogni sottoproblema viene calcolato al massimo una
volta. L'ordine di riempimento della tabella non deve essere stabilito
esplicitamente come in una soluzione bottom-up.

---

## Punto (2)

Ora calcoliamo la complessità al caso migliore, contando solo i confronti tra
caratteri come operazioni di costo unitario e non nullo.

Il caso migliore si verifica quando, in ogni chiamata ricorsiva su un intervallo
di lunghezza almeno `3`, il confronto tra i due caratteri estremi risulta vero:

```text
X[i] == X[j]
```

In questo caso non viene eseguita la sommatoria. La ricorsione procede solo sul
sottoproblema interno:

```text
REC_L(X, i + 1, j - 1)
```

Quindi, se `n = j - i + 1` è la lunghezza dell'intervallo considerato, il costo
nel caso migliore soddisfa:

```text
T_best(n) = T_best(n - 2) + 1
```

dove `+1` rappresenta il confronto tra `X[i]` e `X[j]`.

I casi base sono gli intervalli di lunghezza `1` e `2`, dove non viene eseguito
alcun confronto tra caratteri.

Srotolando la ricorrenza:

```text
T_best(n) = T_best(n - 2) + 1
          = T_best(n - 4) + 2
          = T_best(n - 6) + 3
          ...
          = T_best(n - 2k) + k
```

La ricorsione termina quando la lunghezza residua diventa `1` oppure `2`.

Il numero di confronti eseguiti è quindi:

```text
floor((n - 1) / 2)
```

Quindi:

```text
T_best(n) = floor((n - 1) / 2)
```

e in notazione asintotica:

```text
T_best(n) = Theta(n)
```
