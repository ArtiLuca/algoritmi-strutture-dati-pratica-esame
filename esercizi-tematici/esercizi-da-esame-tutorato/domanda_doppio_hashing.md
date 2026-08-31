# Domanda B — Tabelle Hash

Si consideri una tabella hash di dimensione $m = 11$ che usa indirizzamento aperto con doppio hashing dove $h_1(k) = k \bmod 11$ e $h_2(k) = 1 + (k \bmod 9)$.
Inserire nell'ordine le seguenti chiavi: $22, 31, 4, 15, 28, 17$.

Mostrare la tabella finale.

Successivamente, rispondere alla seguente domanda: perché è utile che $h_2(k)$ non sia mai uguale a zero?

---

### i. Inserimento delle chiavi

Se si usa l'indirizzamento aperto con doppio hashing, la funzione hash generale è definita come:

$$
h(k, i) = (h_1(k) + i \cdot h_2(k)) \bmod m
$$

Sostituendo i valori del nostro caso otteniamo:

$$
h(k, i) = (k \bmod 11 + i \cdot (1 + (k \bmod 9))) \bmod 11
$$

Procediamo con l'inserimento delle chiavi nell'ordine dato:

1. **Inserimento di 22:**
   $h_1(22) = 22 \bmod 11 = 0 \implies h(22, 0) = 0$. Cella vuota, inserito.
2. **Inserimento di 31:**
   $h_1(31) = 31 \bmod 11 = 9 \implies h(31, 0) = 9$. Cella vuota, inserito.
3. **Inserimento di 4:**
   $h_1(4) = 4 \bmod 11 = 4 \implies h(4, 0) = 4$. Cella vuota, inserito.
4. **Inserimento di 15:**
   $h_1(15) = 15 \bmod 11 = 4 \implies h(15, 0) = 4$. **Collisione** (cella occupata dal $4$).
   Calcolo $h_2(15) = 1 + (15 \bmod 9) = 1 + 6 = 7$.
   - $i=1: h(15, 1) = (4 + 1 \cdot 7) \bmod 11 = 11 \bmod 11 = 0$. **Collisione** (cella occupata dal $22$).
   - $i=2: h(15, 2) = (4 + 2 \cdot 7) \bmod 11 = 18 \bmod 11 = 7$. Cella vuota, inserito.
5. **Inserimento di 28:**
   $h_1(28) = 28 \bmod 11 = 6 \implies h(28, 0) = 6$. Cella vuota, inserito.
6. **Inserimento di 17:**
   $h_1(17) = 17 \bmod 11 = 6 \implies h(17, 0) = 6$. **Collisione** (cella occupata dal $28$).
   Calcolo $h_2(17) = 1 + (17 \bmod 9) = 1 + 8 = 9$.
   - $i=1: h(17, 1) = (6 + 1 \cdot 9) \bmod 11 = 15 \bmod 11 = 4$. **Collisione** (cella occupata dal $4$).
   - $i=2: h(17, 2) = (6 + 2 \cdot 9) \bmod 11 = 24 \bmod 11 = 2$. Cella vuota, inserito.

---

### ii. Tabella Finale

| Indice | Chiave |
| :---: | :---: |
| **0** | $22$ |
| **1** | - |
| **2** | $17$ |
| **3** | - |
| **4** | $4$ |
| **5** | - |
| **6** | $28$ |
| **7** | $15$ |
| **8** | - |
| **9** | $31$ |
| **10** | - |

---

### iii. Analisi su $h_2(k) \neq 0$

È fondamentale che $h_2(k)$ non sia mai uguale a zero, altrimenti la funzione hash entrerebbe in un loop infinito durante la gestione di una collisione. Se il passo di scansione $h_2(k)$ valesse $0$, il termine $i \cdot h_2(k)$ si annullerebbe per qualsiasi valore di $i$, e l'algoritmo ispezionerebbe ripetutamente sempre e solo la cella iniziale $h_1(k)$ fallendo l'inserimento.

Inoltre, la condizione teorica affinché il doppio hashing esplori l'intera tabella senza saltare celle è che il passo $h_2(k)$ sia coprimo con la dimensione $m$ della tabella, ovvero $\text{MCD}(h_2(k), m) = 1$. Sebbene nel nostro caso $m=11$ sia un numero primo, se ammettessimo $h_2(k) = 0$, si avrebbe $\text{MCD}(0, 11) = 11 \neq 1$, violando così questa condizione fondamentale.
