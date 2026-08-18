# Esercizio 13 - Definizione O-grande e Dimostrazione

**Domanda 13**
Dare la definizione di $\mathcal{O}(f(n))$. Dimostrare che la ricorrenza che segue ha soluzione $T(n) = \mathcal{O}(n)$
$$ T(n) = \frac{2}{3}T(n - 1) + 2n $$

---

### i. Definizione di $\mathcal{O}(f(n))$

Ricordando che, date due funzioni arbitrarie asintoticamente positive, cioè $f(n), g(n) > 0$, definiamo la classe $\mathcal{O}$ come l'insieme di funzioni:

$$ \mathcal{O}(f(n)) = \{g(n) \mid \exists c > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0 : 0 \le g(n) \le c \cdot f(n) \} $$

---

### ii. Dimostrazione $T(n) = \mathcal{O}(n)$

Seguendo la definizione sopra, per dimostrare che $T(n) = \mathcal{O}(n)$ verifichiamo che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tali che valga $T(n) \le cn$.

Uso come ipotesi induttiva il fatto che la disuguaglianza valga per scelte di $m < n$, ovvero che valga $T(m) \le cm$, e applico questa ipotesi induttiva alla ricorrenza (il che è lecito poiché $n-1 < n$):

$$
\begin{aligned}
T(n) &= \frac{2}{3}T(n-1) + 2n \\
&\le \frac{2}{3}c(n-1) + 2n \\
&= \frac{2}{3}cn - \frac{2}{3}c + 2n
\end{aligned}
$$

Vogliamo che la nostra espressione sia minore o uguale a $cn$:

$$ \frac{2}{3}cn - \frac{2}{3}c + 2n \le cn $$

Isoliamo il termine $2n$ da una parte e raccogliamo la $c$ dall'altra:

$$ 2n \le cn - \frac{2}{3}cn + \frac{2}{3}c \implies 2n \le \frac{1}{3}cn + \frac{2}{3}c \implies 2n \le c\left(\frac{1}{3}n + \frac{2}{3}\right) $$

Quindi serve che:

$$ c \ge \frac{2n}{\frac{1}{3}n + \frac{2}{3}} $$

Moltiplicando numeratore e denominatore per 3 otteniamo:

$$ c \ge \frac{6n}{n+2} $$

Essendo che:

$$ \lim_{n \to \infty} \frac{6n}{n+2} = 6 $$

ovvero è una funzione strettamente crescente che si avvicina a 6 dal basso senza mai superarlo, possiamo scegliere una costante asintotica $c \ge 6$.
(Ad esempio, se proviamo con $c = 6$, otteniamo $\frac{2}{3}(6)n - \frac{2}{3}(6) + 2n = 4n - 4 + 2n = 6n - 4 \le 6n$, che è sempre vero).

Dunque, una scelta di $c = 6$ e un $n_0$ sufficientemente grande (ad esempio $n_0 = 1$) sono sufficienti per dimostrare che vale $T(n) = \mathcal{O}(n)$ per ogni $n \ge n_0$.
