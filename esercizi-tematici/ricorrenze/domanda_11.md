# Domanda 11

$$
T(n) = \frac{1}{2}T(n - 1) + n
$$

---

### i. Limite superiore $\mathcal{O}(n)$

Dimostriamo che vale $T(n) = \mathcal{O}(n)$, ovvero che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \le cn$, assumendo per induzione forte che questa valga per valori $m < n$, ovvero che valga $T(m) \le cm$:

$$
T(n) = \frac{1}{2}T(n-1) + n \le \frac{1}{2}c(n-1) + n = \frac{1}{2}cn - \frac{1}{2}c + n = \left(\frac{1}{2}c + 1\right)n - \frac{1}{2}c
$$

Possiamo effettuare una maggiorazione, ovvero:

$$
\left(\frac{1}{2}c + 1\right)n - \frac{1}{2}c \le \left(\frac{1}{2}c + 1\right)n
$$

Vogliamo che $\left(\frac{1}{2}c + 1\right)n \le cn$, quindi dividiamo entrambi i lati per $n$ (assumendo $n > 0$) e otteniamo:

$$
\frac{1}{2}c + 1 \le c \implies 1 \le \frac{1}{2}c \implies c \ge 2
$$

Con una scelta di $c=4$ la disuguaglianza $\left(\frac{1}{2}c + 1\right)n - \frac{1}{2}c \le cn$ diventa quindi $3n - 2 \le 4n$, che vale per ogni scelta $n_0 \ge 1$ e quindi abbiamo dimostrato che vale $T(n) = \mathcal{O}(n)$ per ogni $n \ge n_0$.

---

### ii. Limite inferiore $\Omega(n)$

Dimostriamo ora che vale $T(n) = \Omega(n)$, ovvero che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \ge dn$, assumendo per induzione forte che questa valga per valori $m < n$, ovvero che valga $T(m) \ge dm$:

$$
T(n) = \frac{1}{2}T(n-1) + n \ge \frac{1}{2}d(n-1) + n = \frac{1}{2}dn - \frac{1}{2}d + n
$$

Vogliamo che $\frac{1}{2}dn - \frac{1}{2}d + n \ge dn$, quindi impostiamo la disuguaglianza come segue:

$$
-\frac{1}{2}d \ge \frac{1}{2}dn - n \implies -\frac{1}{2}d \ge n\left(\frac{1}{2}d - 1\right)
$$

Possiamo notare che questo si verifica solo se la parte destra è strettamente minore di 0, essendo che per $n \to \infty$ questo termine “domina” sempre rispetto alla parte sinistra, che è una costante. Quindi, imponiamo:

$$
\frac{1}{2}d - 1 < 0 \implies \frac{1}{2}d < 1 \implies d < 2
$$

Infatti, una scelta di $d=1$ applicata alla disuguaglianza precedente ci porta a $\frac{3}{2}n - \frac{1}{2} \ge n$, che vale per qualunque $n_0 \ge 1$, e quindi abbiamo dimostrato che vale anche $T(n) = \Omega(n)$ per ogni $n \ge n_0$.

---

### iii. Conclusione

Avendo dimostrato che $T(n) = \mathcal{O}(n)$ e anche $T(n) = \Omega(n)$ possiamo quindi concludere che:

$$
T(n) = \Theta(n)
$$
