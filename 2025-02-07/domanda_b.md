# Domanda B — Hashing con doppio hash

[← Torna all'appello](README.md)

## Testo

**Domanda B (7 punti)**

Si consideri una tabella hash di dimensione $m=7$, e indirizzamento aperto con
doppio hash basato sulle funzioni:

```math
h_1(k)=k \bmod m
```

e

```math
h_2(k)=1+k \bmod (m-2).
```

Si descriva sinteticamente come avviene l'inserimento degli elementi e si
specifichi il risultato dell'inserzione della sequenza di chiavi:

```math
10,20,34,35,48.
```

Sarebbe appropriato lavorare con una tabella di dimensione $m=8$ e le stesse
funzioni hash?

---

## Soluzione

Con indirizzamento aperto e doppio hashing, al tentativo $i$ la posizione
visitata è:

```math
h(k,i)=\bigl(h_1(k)+i\cdot h_2(k)\bigr)\bmod m.
```

Nel nostro caso $m=7$, quindi:

```math
h_1(k)=k\bmod 7,
```

e:

```math
h_2(k)=1+k\bmod 5.
```

L'inserimento prova le posizioni:

```math
h(k,0), h(k,1), h(k,2), \ldots
```

fino a trovare una cella libera.

---

## Inserimento delle chiavi

### Chiave 10

```math
h(10,0)=10\bmod 7=3.
```

La posizione `3` è libera, quindi inseriamo `10` in posizione `3`.

### Chiave 20

```math
h(20,0)=20\bmod 7=6.
```

La posizione `6` è libera, quindi inseriamo `20` in posizione `6`.

### Chiave 34

```math
h(34,0)=34\bmod 7=6.
```

La posizione `6` è occupata.

Calcoliamo il secondo hash:

```math
h_2(34)=1+(34\bmod 5)=1+4=5.
```

Proviamo quindi:

```math
h(34,1)=(6+1\cdot 5)\bmod 7=11\bmod 7=4.
```

La posizione `4` è libera, quindi inseriamo `34` in posizione `4`.

### Chiave 35

```math
h(35,0)=35\bmod 7=0.
```

La posizione `0` è libera, quindi inseriamo `35` in posizione `0`.

### Chiave 48

```math
h(48,0)=48\bmod 7=6.
```

La posizione `6` è occupata.

Calcoliamo il secondo hash:

```math
h_2(48)=1+(48\bmod 5)=1+3=4.
```

Proviamo quindi:

```math
h(48,1)=(6+1\cdot 4)\bmod 7=10\bmod 7=3.
```

La posizione `3` è occupata.

```math
h(48,2)=(6+2\cdot 4)\bmod 7=14\bmod 7=0.
```

La posizione `0` è occupata.

```math
h(48,3)=(6+3\cdot 4)\bmod 7=18\bmod 7=4.
```

La posizione `4` è occupata.

```math
h(48,4)=(6+4\cdot 4)\bmod 7=22\bmod 7=1.
```

La posizione `1` è libera, quindi inseriamo `48` in posizione `1`.

---

## Tabella finale

| Indice | Contenuto |
|---:|---:|
| 0 | 35 |
| 1 | 48 |
| 2 | |
| 3 | 10 |
| 4 | 34 |
| 5 | |
| 6 | 20 |

---

## Caso $m=8$

Non sarebbe appropriato usare $m=8$ con le stesse funzioni hash.

Nel doppio hashing, per poter visitare tutta la tabella, è importante che il
passo $h_2(k)$ sia coprimo con la dimensione della tabella $m$:

```math
\gcd(m,h_2(k))=1.
```

Se questo non accade, la sequenza di tentativi può visitare solo una parte della
tabella.

Con $m=8$, la funzione diventerebbe:

```math
h_2(k)=1+k\bmod 6.
```

Questa funzione può produrre valori non coprimi con `8`, ad esempio `2`, `4` o
`6`.

Per esempio, se il passo fosse `2`, la sequenza visiterebbe solo metà delle
celle della tabella.

Quindi $m=8$ non è una scelta appropriata per questo schema di doppio hashing.
