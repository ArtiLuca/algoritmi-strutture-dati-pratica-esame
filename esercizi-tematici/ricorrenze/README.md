# Limiti Asintotici e Ricorrenze

[← Torna agli esercizi tematici](../README.md) · [Torna alla raccolta principale](../../README.md)

Questa cartella raccoglie esercizi su notazione asintotica, Master Theorem, metodo di sostituzione e dimostrazioni di limiti superiori, inferiori e stretti.

Gli esercizi sono pensati per allenarsi sulla parte teorica dell'esame: riconoscere la forma di una ricorrenza, scegliere il metodo più adatto, impostare correttamente ipotesi induttive e dimostrare relazioni tra classi asintotiche.

Ogni esercizio completato contiene una soluzione in stile esame, con passaggi algebrici espliciti e giustificazione delle costanti quando richiesto.

---

## Stato delle soluzioni

| Esercizio | Stato |
|---|---|
| Domanda 1 — `T(n) = 4T(n/2) + n log n` | Da completare |
| Domanda 2 — `T(n) = T(n/2) + T(n/4) + n` | Da completare |
| Domanda 3 — `T(n) = 4T(n/2) + n√n` | Da completare |
| Domanda 4 — `T(n) = T(n - 2) + 2n` | Da completare |
| Domanda 5 — Ricorrenza esatta con `T(n - 1) + 2` | Da completare |
| Domanda 6 — `3T(n/5) + T(n/6) + n` | [Completato](domanda_6.md) |
| Domanda 7 — `5T(⌊n/3⌋) + 2n²` | [Completato](domanda_7.md) |
| Domanda 8 — `T(n) = T(n - 1) + log n` | [Completato](esercizio_8.md) |
| Domanda 9 — `T(n/2) + T(√n/2) + 2n` | [Completato](domanda_9.md) |
| Domanda 10 — `T(4n/5) + n/2 + log n` | [Completato](domanda_10.md) |
| Domanda 11 — `1/2 T(n - 1) + n` | Da completare |
| Domanda 12 — Definizione di Ω e ricorrenza con sommatoria | [Completato](domanda_12.md) |
| Domanda 13 — Definizione di O e ricorrenza `2/3 T(n - 1) + 2n` | [Completato](esercizio_13.md) |
| Domanda 14 — `3T(n/2) + n(n + 1)` | Da completare |
| Domanda 15 — `T(n/2) + T(n/3) + √n + 2` | Da completare |
| Domanda 16 — `5T(n/3) + (n - 2)²` | Da completare |
| Domanda 17 — Transitività di Ω | [Completato](domanda_17.md) |
| Domanda 18 — Relazione tra Θ, O e Ω | Da completare |

---

## Testi degli Esercizi

### **Domanda 1**

Risolvere la ricorrenza $T(n) = 4 T(n/2) + n \log n$ utilizzando il master theorem.

---

### **Domanda 2**

Mostrare che la ricorrenza $T(n) = T(n/2) + T(n/4) + n$ ammette soluzione $T(n) = \Theta(n)$ utilizzando il metodo di sostituzione.

---

### **Domanda 3**

Risolvere la ricorrenza $T(n) = 4T(n/2) + n\sqrt{n}$ utilizzando il master theorem.

---

### **Domanda 4**

Risolvere la ricorrenza $T(n) = T(n - 2) + 2n$ utilizzando il metodo di sostituzione per dimostrare un limite asintotico stretto.

---

### **Domanda 5**

Risolvere la ricorrenza

$$
T(n) = \begin{cases} 3 & \text{se } n = 0 \\ T(n - 1) + 2 & \text{se } n > 0 \end{cases}
$$

utilizzando il metodo di sostituzione per determinare una soluzione esatta (non asintotica).

---

### **Domanda 6**

Sia data la seguente equazione di ricorrenza:

$$
T(n) = \begin{cases} 1 & \text{se } n = 1 \\ 3T(n/5) + T(n/6) + n & \text{se } n > 1 \end{cases}
$$

Si fornisca un limite asintotico stretto per la soluzione.

---

### **Domanda 7**

Sia data la seguente equazione di ricorrenza:

$$
T(n) = 5T(\lfloor n/3 \rfloor) + 2n^2
$$

Si fornisca un limite asintotico stretto per la soluzione.

---

### **Domanda 8**

Sia data la seguente equazione di ricorrenza:

$$
T(n) = T(n - 1) + \log n
$$

Si dimostri che $T(n) = \mathcal{O}(n \log n)$.

---

### **Domanda 9**

Sia data la seguente equazione di ricorrenza:

$$
T(n) = T(n/2) + T(\sqrt{n}/2) + 2n
$$

Si dimostri che $T(n) = \Theta(n)$.

---

### **Domanda 10**

Si consideri la ricorrenza

$$
T(n) = T\left(\frac{4n}{5}\right) + \frac{n}{2} + \log n
$$

Fornire limite asintotico stretto per la soluzione.

---

### **Domanda 11**

Si dimostri che la ricorrenza che segue ha soluzione $T(n) = \Theta(n)$

$$
T(n) = \frac{1}{2}T(n - 1) + n
$$

---

### **Domanda 12**

Dare la definizione di $\Omega(f(n))$. Dimostrare che la ricorrenza che segue ha soluzione $T(n) = \Omega(2^n)$

$$
T(n) = \sum_{k=1}^{n-1} T(k) T(n - k)
$$

---

### **Domanda 13**

Dare la definizione di $\mathcal{O}(f(n))$. Dimostrare che la ricorrenza che segue ha soluzione $T(n) = \mathcal{O}(n)$

$$
T(n) = \frac{2}{3}T(n - 1) + 2n
$$

---

### **Domanda 14**

Dare una soluzione asintotica per la ricorrenza $T(n) = 3T(n/2) + n(n + 1)$.

---

### **Domanda 15**

Data la ricorrenza $T(n) = T(n/2) + T(n/3) + \sqrt{n} + 2$ dimostrare che ha soluzione $T(n) = \mathcal{O}(n)$. Il limite è stretto, ovvero vale anche $T(n) = \Omega(n)$?

---

### **Domanda 16**

Data la ricorrenza $T(n) = 5T(n/3) + (n - 2)^2$, trovare la soluzione asintotica.

---

### **Domanda 17**

Dare la definizione di $\Omega(f(n))$. Mostrare che se $f(n) = \Omega(g(n))$ e $g(n) = \Omega(h(n))$ allora $f(n) = \Omega(h(n))$.

---

### **Domanda 18**

Dare la definizione di $\Theta(f(n))$. Mostrare che $\Theta(f(n)) = \mathcal{O}(f(n)) \cap \Omega(f(n))$.
