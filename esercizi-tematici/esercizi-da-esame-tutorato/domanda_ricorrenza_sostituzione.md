# Domanda A — Ricorrenza con metodo di sostituzione

Si dimostri che la ricorrenza che segue ha soluzione $T(n) = \Theta(n)$:

$$
T(n) = \frac{2}{3}T(n-1) + 2n
$$

---

### i. Limite superiore $\mathcal{O}(n)$

Dimostriamo che vale $T(n) = \mathcal{O}(n)$, ovvero che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \le cn$, assumendo per induzione forte che questa valga per valori $m < n$, ovvero che valga $T(m) \le cm$:

$$
T(n) = \frac{2}{3}T(n-1) + 2n \le \frac{2}{3}c(n-1) + 2n = \frac{2}{3}cn - \frac{2}{3}c + 2n = \left(\frac{2}{3}c + 2\right)n - \frac{2}{3}c
$$

Faccio una maggiorazione:

$$
\left(\frac{2}{3}c + 2\right)n - \frac{2}{3}c  \le \left(\frac{2}{3}c + 2\right)n
$$

e quindi segue la catena di disuguaglianze:

$$
\left(\frac{2}{3}c + 2\right)n \le cn \implies \frac{2}{3}c + 2 \le c \implies 2 \le \frac{1}{3}c \implies c \ge 6
$$

Una scelta di $c = 9$ e $n_0 = 1$ vanno bene. Quindi vale $T(n) = \mathcal{O}(n)$ per ogni $n \ge n_0$.

---

### ii. Limite inferiore $\Omega(n)$

Dimostriamo che vale $T(n) = \Omega(n)$, ovvero che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \ge dn$, assumendo per induzione forte che questa valga per valori $m < n$, ovvero che valga $T(m) \ge dm$:

$$
T(n) = \frac{2}{3}T(n-1) + 2n \ge \frac{2}{3}d(n-1) + 2n = \frac{2}{3}dn - \frac{2}{3}d + 2n
$$

Vogliamo che $\frac{2}{3}dn - \frac{2}{3}d + 2n \ge dn$, quindi segue:

$$
-\frac{2}{3}d \ge \frac{1}{3}dn - 2n \implies -\frac{2}{3}d \ge n\left(\frac{1}{3}d - 2\right)
$$

(essendo che $-\frac{2}{3}d$ è costante, il termine a destra “domina” per $n \to \infty$)

$$
\frac{1}{3}d - 2 < 0 \implies \frac{1}{3}d < 2 \implies d < 6
$$

Una scelta di $d = 3$ e $n_0 = 1$ vanno bene. Quindi vale anche $T(n) = \Omega(n)$ per ogni $n \ge n_0$.

---

### iii. Conclusione

Avendo dimostrato entrambi i limiti superiore ed inferiore, possiamo concludere che:

$$
T(n) = \Theta(n)
$$
