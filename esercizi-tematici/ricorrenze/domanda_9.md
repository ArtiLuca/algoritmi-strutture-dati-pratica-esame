# Esercizio 9 - Dimostrazione O-grande e Omega con sostituzione

Sia data la seguente equazione di ricorrenza:

$$
T(n) = T(n/2) + T(\sqrt{n}/2) + 2n
$$

Si dimostri che $T(n) = \Theta(n)$.

---

### i. Dimostrazione del limite superiore $\mathcal{O}(n)$

Dimostriamo prima che vale $T(n) = \mathcal{O}(n)$, ovvero che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \le cn$.

Assumendo come ipotesi induttiva che la disuguaglianza valga per $m < n$, ovvero che valga $T(m) \le cm$, applichiamo questa ipotesi alla nostra ricorrenza (il che è lecito perché $\frac{n}{2} < n$ e $\frac{\sqrt{n}}{2} < n$ per $n > 0$):

$$
\begin{aligned}
T(n) &= T\left(\frac{n}{2}\right) + T\left(\frac{\sqrt{n}}{2}\right) + 2n \\
&\le c\left(\frac{n}{2}\right) + c\left(\frac{\sqrt{n}}{2}\right) + 2n \\
&= c\left(\frac{n + \sqrt{n}}{2}\right) + 2n
\end{aligned}
$$

Possiamo notare che $\sqrt{n} \le \frac{n}{2}$ per ogni $n \ge 4$. Possiamo quindi effettuare una maggiorazione:

$$
c\left(\frac{n + \sqrt{n}}{2}\right) + 2n \le c\left(\frac{n + \frac{n}{2}}{2}\right) + 2n = c\left(\frac{\frac{3n}{2}}{2}\right) + 2n = \frac{3}{4}cn + 2n
$$

Vogliamo che la nostra stima sia minore o uguale a $cn$:

$$
\frac{3}{4}cn + 2n \le cn
$$

Raccogliendo $n$ otteniamo $\left(\frac{3}{4}c + 2\right)n \le cn$.
Dividendo tutto per $n$ (lecito perché abbiamo assunto $n \ge 4$) otteniamo:

$$
\frac{3}{4}c + 2 \le c \implies 2 \le \frac{1}{4}c \implies c \ge 8
$$

Una scelta di $c \ge 8$ e $n_0 = 4$ soddisfa la condizione. Quindi vale che $T(n) = \mathcal{O}(n)$ per ogni $n \ge n_0$.

---

### ii. Dimostrazione del limite inferiore $\Omega(n)$

Dimostriamo ora che $T(n) = \Omega(n)$, ovvero che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \ge dn$.

Assumendo come ipotesi induttiva che questo valga per valori $m < n$, applichiamo alla nostra ricorrenza:

$$
\begin{aligned}
T(n) &= T\left(\frac{n}{2}\right) + T\left(\frac{\sqrt{n}}{2}\right) + 2n \\
&\ge d\left(\frac{n}{2}\right) + d\left(\frac{\sqrt{n}}{2}\right) + 2n \\
&= d\left(\frac{n + \sqrt{n}}{2}\right) + 2n
\end{aligned}
$$

Essendo che $\sqrt{n} \ge 0$ per ogni $n \ge 0$, possiamo effettuare questa volta una minorazione:

$$
d\left(\frac{n + \sqrt{n}}{2}\right) + 2n \ge d\left(\frac{n + 0}{2}\right) + 2n = \frac{1}{2}dn + 2n
$$

Vogliamo che il risultato sia maggiore o uguale a $dn$:

$$
\frac{1}{2}dn + 2n \ge dn
$$

Dalla disuguaglianza $\left(\frac{1}{2}d + 2\right)n \ge dn$, dividendo per $n$ (lecito per $n > 0$), otteniamo:

$$
\frac{1}{2}d + 2 \ge d \implies 2 \ge \frac{1}{2}d \implies d \le 4
$$

Una scelta di costante $d \le 4$ (con $d > 0$) e $n_0 = 1$ soddisfa la disuguaglianza. Quindi vale che $T(n) = \Omega(n)$ per ogni $n \ge n_0$.

---

### iii. Conclusione

Avendo dimostrato separatamente sia il limite superiore ($\mathcal{O}(n)$) che il limite inferiore ($\Omega(n)$), per il teorema della doppia implicazione asintotica possiamo concludere formalmente che la ricorrenza ammette come soluzione asintotica stretta:

$$
T(n) = \Theta(n)
$$
