# Esercizio 1 — Split con divide et impera

[← Torna all'appello](README.md)

## Testo

**Esercizio 1 (10 punti)**

Sia dato un array `V[1..n]` i cui valori rappresentano la variazione giornaliera
del valore di un titolo azionario.

È noto che il titolo è stato prima in perdita, con valori sempre negativi, poi
ha iniziato a oscillare in giorni consecutivi tra valori positivi e negativi, e
infine si è stabilizzato su valori positivi. Dunque nella sequenza non ci
possono essere due giorni positivi seguiti da un negativo.

Realizzare un algoritmo *divide et impera* `Split(V)` che individua il giorno in
cui il titolo ha iniziato a essere stabile su valori positivi, ovvero il minimo
indice `i` in `[1,n]` tale che per ogni `j >= i` vale `V[j] > 0`.

Se il titolo non si stabilizza su valori positivi, ritornare `0`.

Ad esempio, se l'array è:

```text
V = [-1, -2, 2, -1, 6, 3]
```

l'indice da ritornare sarà `5`, mentre per:

```text
V = [-1, -2, 2, -1, 6, -3]
```

si ritornerà `0`.

Fornire lo pseudocodice di `Split(V)`, motivarne la correttezza e individuarne
la complessità. Si assuma che non ci siano valori nulli.

---

## Soluzione

Dal testo sappiamo che la sequenza ha una struttura particolare:

1. una prima parte con valori negativi;
2. una parte centrale oscillante tra valori positivi e negativi;
3. eventualmente, una parte finale con soli valori positivi.

Inoltre, non possono esserci due valori positivi consecutivi seguiti poi da un
valore negativo.

Quindi, se troviamo due valori positivi consecutivi, allora da quel punto in poi
la sequenza è stabile su valori positivi.

L'obiettivo è trovare il minimo indice `i` tale che:

```text
per ogni j >= i, V[j] > 0
```

Se tale indice non esiste, restituiamo `0`.

La soluzione usa una ricerca divide et impera simile a una ricerca binaria.

---

## Pseudocodice

```text
Split(V)
    n = V.length

    m = SplitRec(V, 1, n, n)

    if m > n
        return 0
    else
        return m


SplitRec(V, p, r, n)
    if p > r
        return p

    q = floor((p + r) / 2)

    if V[q] < 0
        return SplitRec(V, q + 1, r, n)

    else
        if q < n and V[q + 1] < 0
            return SplitRec(V, q + 1, r, n)

        else
            return SplitRec(V, p, q - 1, n)
```

---

## Correttezza

Definiamo la proprietà `P(i)` come:

```text
P(i) = "da i in poi tutti i valori sono positivi"
```

Vogliamo trovare il minimo indice `i` tale che `P(i)` è vera.

Per l'ipotesi del testo, la proprietà `P(i)` è falsa prima dell'inizio della
stabilità ed è vera da quel punto in poi.

A ogni passo l'algoritmo considera l'indice centrale `q`.

### Caso 1: `V[q] < 0`

Se `V[q] < 0`, allora nessun indice `i <= q` può essere stabile, perché scegliendo
un tale `i` avremmo comunque il valore negativo `V[q]` nella parte da `i` in poi.

Quindi è corretto cercare solo nella metà destra.

### Caso 2: `V[q] > 0` e `q < n` e `V[q + 1] < 0`

In questo caso, anche se `V[q]` è positivo, il giorno successivo è negativo.

Quindi nessun indice `i <= q` può essere stabile, perché da `i` in poi sarebbe
presente il valore negativo `V[q + 1]`.

Anche in questo caso è corretto cercare solo nella metà destra.

### Caso 3: `V[q] > 0` e (`q = n` oppure `V[q + 1] > 0`)

In questo caso abbiamo trovato un valore positivo seguito da un altro valore
positivo, oppure siamo arrivati all'ultimo elemento.

Per l'ipotesi del testo, non possono esserci due positivi consecutivi seguiti
da un negativo. Quindi `P(q)` è vera: da `q` in poi tutti i valori sono positivi.

Tuttavia, `q` potrebbe non essere il primo indice stabile. Perciò è corretto
continuare a cercare nella metà sinistra.

Quando l'intervallo di ricerca diventa vuoto, l'indice `p` è il primo indice
stabile trovato dalla ricerca. Se `p = n + 1`, significa che non esiste una parte
finale stabile positiva e `Split(V)` restituisce `0`.

Quindi l'algoritmo è corretto.

---

## Complessità

A ogni passo l'algoritmo esamina un numero costante di elementi e continua su
una sola metà dell'intervallo.

La ricorrenza è:

```math
T(n)=T(n/2)+\Theta(1).
```

Quindi:

```math
T(n)=\Theta(\log n).
```

La complessità temporale è:

```math
\Theta(\log n).
```

La complessità spaziale è:

```math
O(\log n),
```

a causa dello stack di chiamate ricorsive.

Una versione iterativa avrebbe spazio:

```math
O(1).
```
