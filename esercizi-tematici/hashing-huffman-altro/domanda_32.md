# Domanda 32

Si consideri una tabella hash di dimensione $m = 8$, e indirizzamento aperto con doppio hash basato sulle funzioni $h_1(k) = k \bmod m$ e $h_2(k) = 1 + 2 \cdot (k \bmod (m - 3))$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: 34, 12, 18, 9, 42.

---

### i. Funzione di Hash

Si usa il doppio hashing e quindi la funzione di hash $h(k, i)$ con $k$ chiave e $i$ come numero di tentativi sarà:

$$
h(k, i) = (h_1(k) + i \cdot h_2(k)) \bmod m
$$

Quindi nel nostro caso:

$$
h(k, i) = (k \bmod 8 + i \cdot (1 + 2 \cdot (k \bmod 5))) \bmod 8
$$

---

### ii. Inserimento della sequenza (34, 12, 18, 9, 42)

- **Inserimento di 34:**
  $h(34, 0) = 34 \bmod 8 = 2$ (Inserito in 2)

- **Inserimento di 12:**
  $h(12, 0) = 12 \bmod 8 = 4$ (Inserito in 4)

- **Inserimento di 18:**
  $h(18, 0) = 18 \bmod 8 = 2$ (Collisione con 34)
  $h(18, 1) = (2 + 1 \cdot (1 + 2 \cdot (18 \bmod 5))) \bmod 8 = (2 + 1 + 2 \cdot 3) \bmod 8 = 9 \bmod 8 = 1$ (Inserito in 1)

- **Inserimento di 9:**
  $h(9, 0) = 9 \bmod 8 = 1$ (Collisione con 18)
  $h(9, 1) = (1 + 1 \cdot (1 + 2 \cdot (9 \bmod 5))) \bmod 8 = (1 + 1 + 2 \cdot 4) \bmod 8 = 10 \bmod 8 = 2$ (Collisione con 34)
  $h(9, 2) = (1 + 2 \cdot 9) \bmod 8 = 19 \bmod 8 = 3$ (Inserito in 3)

- **Inserimento di 42:**
  $h(42, 0) = 42 \bmod 8 = 2$ (Collisione con 34)
  $h(42, 1) = (2 + 1 \cdot (1 + 2 \cdot (42 \bmod 5))) \bmod 8 = (2 + 1 + 2 \cdot 2) \bmod 8 = 7 \bmod 8 = 7$ (Inserito in 7)

---

### iii. Tabella Finale

La tabella risultante si presenta quindi alla fine come segue:

- **0:**
- **1:** $18$
- **2:** $34$
- **3:** $9$
- **4:** $12$
- **5:**
- **6:**
- **7:** $42$
