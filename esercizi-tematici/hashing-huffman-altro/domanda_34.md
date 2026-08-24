### **Domanda 34**

Si consideri una tabella hash di dimensione $m = 8$, gestita mediante chaining (liste di trabocco) con funzione di hash $h(k) = k \bmod m$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: $14, 10, 22, 18, 19$.

---

Se usiamo il **chaining**, la funzione di hash $h(k) = k \bmod m$ inserisce gli elementi in un array di liste $T[0\dots m-1]$ in modo che $T[i]$ contenga tutti gli elementi aventi lo stesso valore di hash della chiave.

Nel corso abbiamo usato la convenzione di inserire gli elementi con stesso hashing di chiave in testa alla lista.

Calcoliamo i valori di hash per la sequenza fornita:
- $14 \bmod 8 = 6$
- $10 \bmod 8 = 2$
- $22 \bmod 8 = 6$
- $18 \bmod 8 = 2$
- $19 \bmod 8 = 3$

Quindi alla fine la tabella hash $T[0\dots 7]$ si presenta in questo modo:

- **0:**
- **1:**
- **2:** $18 \to 10$
- **3:** $19$
- **4:**
- **5:**
- **6:** $22 \to 14$
- **7:**
