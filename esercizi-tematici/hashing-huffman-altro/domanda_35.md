# Domanda 35

Si consideri una tabella hash di dimensione $m = 9$, e indirizzamento aperto con doppio hash basato sulle funzioni $h_1(k) = k \bmod m$ e $h_2(k) = 1 + (k \bmod (m - 2))$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: 12, 3, 22, 14, 38.

---

### i. Funzione di Hash

Si usa il doppio hashing e quindi la funzione di hash $h(k, i)$ con $k$ chiave e $i$ come numero di tentativi sarà:

$$
h(k, i) = (h_1(k) + i \cdot h_2(k)) \bmod m
$$

Quindi nel nostro caso ($m=9$, $m-2=7$):

$$
h(k, i) = (k \bmod 9 + i \cdot (1 + k \bmod 7)) \bmod 9
$$

---

### ii. Inserimento della sequenza (12, 3, 22, 14, 38)

- **Inserimento di 12:**
  $h(12, 0) = 12 \bmod 9 = 3$ (Inserito in 3)

- **Inserimento di 3:**
  $h(3, 0) = 3 \bmod 9 = 3$ (Collisione con 12)
  $h(3, 1) = (3 + 1 \cdot (1 + 3 \bmod 7)) \bmod 9 = (3 + 1 + 3) \bmod 9 = 7 \bmod 9 = 7$ (Inserito in 7)

- **Inserimento di 22:**
  $h(22, 0) = 22 \bmod 9 = 4$ (Inserito in 4)

- **Inserimento di 14:**
  $h(14, 0) = 14 \bmod 9 = 5$ (Inserito in 5)

- **Inserimento di 38:**
  $h(38, 0) = 38 \bmod 9 = 2$ (Inserito in 2)

---

### iii. Tabella Finale

Quindi alla fine abbiamo una tabella finale come segue:

- **0:**
- **1:**
- **2:** $38$
- **3:** $12$
- **4:** $22$
- **5:** $14$
- **6:**
- **7:** $3$
- **8:**
