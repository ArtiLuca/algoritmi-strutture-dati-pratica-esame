# Domanda B Esame — Hashing con doppio hash

Si consideri una tabella hash di dimensione $m=7$, e indirizzamento aperto con doppio hash basato sulle funzioni:
$h_1(k) = k \bmod m$ e $h_2(k) = 1 + k \bmod (m-2)$.
Si descriva sinteticamente come avviene l'inserimento degli elementi e si specifichi il risultato dell'inserzione della sequenza di chiavi: $10, 20, 34, 35, 48$.

Sarebbe appropriato lavorare con una tabella di dimensione $m=8$ e le stesse funzioni hash?

---

### i. Inserimento con doppio hash

La funzione di hash per l'indirizzamento aperto con doppio hash viene definita come segue:

$$
h(k, i) = (h_1(k) + i \cdot h_2(k)) \bmod m = (k \bmod m + i \cdot (1 + k \bmod (m - 2))) \bmod m
$$

Nel nostro caso, con $m = 7$, abbiamo:

$$
h(k, i) = (k \bmod 7 + i \cdot (1 + k \bmod 5)) \bmod 7
$$

Inseriamo la sequenza passo dopo passo:

- **Inserimento di 10:**
  $h(10, 0) = 10 \bmod 7 = 3$ (Inserito in 3)

- **Inserimento di 20:**
  $h(20, 0) = 20 \bmod 7 = 6$ (Inserito in 6)

- **Inserimento di 34:**
  $h(34, 0) = 34 \bmod 7 = 6$ (Collisione)

  $h(34, 1) = (6 + 1 \cdot (1 + 34 \bmod 5)) \bmod 7 = (6 + 1 + 4) \bmod 7 = 11 \bmod 7 = 4$ (Inserito in 4)

- **Inserimento di 35:**
  $h(35, 0) = 35 \bmod 7 = 0$ (Inserito in 0)

- **Inserimento di 48:**
  $h(48, 0) = 48 \bmod 7 = 6$ (Collisione)

  $h(48, 1) = (6 + 1 \cdot (1 + 48 \bmod 5)) \bmod 7 = (6 + 1 + 3) \bmod 7 = 10 \bmod 7 = 3$ (Collisione)

  $h(48, 2) = (6 + 2 \cdot 4) \bmod 7 = 14 \bmod 7 = 0$ (Collisione)

  $h(48, 3) = (6 + 3 \cdot 4) \bmod 7 = 18 \bmod 7 = 4$ (Collisione)

  $h(48, 4) = (6 + 4 \cdot 4) \bmod 7 = 22 \bmod 7 = 1$ (Inserito in 1)

La tabella finale quindi si presenta così:
- **0:** $35$
- **1:** $48$
- **2:**
- **3:** $10$
- **4:** $34$
- **5:**
- **6:** $20$

---

### ii. Analisi della dimensione $m = 8$

Se lavorassimo con le stesse funzioni hash $h_1(k), h_2(k)$ ma con $m = 8$, allora il doppio hashing non funzionerebbe bene e si limiterebbe a ispezionare solo un sottoinsieme delle celle della tabella.

Questo perché, per il buon funzionamento del doppio hashing, serve la condizione che il valore dello step $h_2(k)$ e la dimensione $m$ della tabella siano relativamente primi (coprimi). Ovvero, bisogna avere che $\text{MCD}(h_2(k), m) = 1$ per ogni chiave.
Con $m = 8$, avremmo $h_2(k) = 1 + k \bmod 6$, che può tranquillamente generare valori pari (es. 2, 4, 6) che condividono fattori comuni con 8.
Di conseguenza, con $m=8$ il doppio hashing non funzionerebbe come con la scelta di $m=7$, che essendo un numero primo garantisce sempre l'ispezione dell'intera tabella e risulta quindi una scelta nettamente migliore.
