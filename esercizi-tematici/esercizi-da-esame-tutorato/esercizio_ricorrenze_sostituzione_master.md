# Esercizi Ricorrenze - Tutorato

### (1) Dimostrare che la ricorrenza $T(n) = T(n/2) + T(n/4) + n$ ammette soluzione $\Theta(n)$

Per dimostrare che $T(n) = \mathcal{O}(n)$, dimostriamo che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \le cn$.

Assumiamo come ipotesi induttiva che questo valga per $m < n$, ovvero che $T(m) \le cm$.
Applichiamo l'ipotesi induttiva alla ricorrenza, il che è lecito essendo $n/2 < n$ e $n/4 < n$:

$$
\begin{aligned}
T(n) &= T\left(\frac{n}{2}\right) + T\left(\frac{n}{4}\right) + n \\
&\le c\frac{n}{2} + c\frac{n}{4} + n \\
&= \frac{3}{4}cn + n \\
&= \left(\frac{3}{4}c + 1\right)n
\end{aligned}
$$

Vogliamo che $\left(\frac{3}{4}c + 1\right)n \le cn$, quindi serve che $\frac{3}{4}c + 1 \le c$, da cui si ricava $1 \le \frac{1}{4}c$.
Una scelta di $c \ge 4$ soddisfa la disuguaglianza per dimostrare che $T(n) = \mathcal{O}(n)$ per ogni $n \ge n_0$.

In modo analogo, per dimostrare che $T(n) = \Omega(n)$, verifichiamo che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \ge dn$.
Assumiamo l'ipotesi induttiva per $m < n$, ovvero $T(m) \ge dm$:

$$
\begin{aligned}
T(n) &= T\left(\frac{n}{2}\right) + T\left(\frac{n}{4}\right) + n \\
&\ge d\frac{n}{2} + d\frac{n}{4} + n \\
&= \frac{3}{4}dn + n \\
&= \left(\frac{3}{4}d + 1\right)n
\end{aligned}
$$

Vogliamo che $\left(\frac{3}{4}d + 1\right)n \ge dn$, ovvero $\frac{3}{4}d + 1 \ge d$, da cui $1 \ge \frac{1}{4}d$.
Una scelta di $d \le 4$ è sufficiente per dimostrare che $T(n) = \Omega(n)$ per ogni $n \ge n_0$.

Avendo verificato entrambi i limiti, possiamo concludere che $T(n) = \Theta(n)$.

---

### (2) Trovare un'ipotesi per $T(n) = T(n-2) + 2n$ e dimostrare con sostituzione

Se "srotoliamo" la ricorrenza usando un albero, osserviamo una sequenza di costi del tipo:

$$ 2n, 2(n-2), 2(n-4), \dots, 2(n-i) $$

La discesa si ferma quando $n-i = 0$, implicando che l'altezza dell'albero di ricorsione è $h = \frac{n}{2}$.
Sommando i costi e applicando la somma di Gauss:

$$
T(n) = 2 \sum_{i=1}^{n/2} 2i = 4 \sum_{i=1}^{n/2} i = 4 \frac{\frac{n}{2}\left(\frac{n}{2}+1\right)}{2} = 4 \frac{\frac{n^2}{4} + \frac{n}{2}}{2} = \frac{n^2}{2} + n
$$

Ipotizziamo quindi come soluzione $T(n) = \Theta(n^2)$.

**Limite Superiore $\mathcal{O}(n^2)$:**
Vogliamo $\exists c > 0$ tale che $T(n) \le cn^2$. Assumiamo $T(n-2) \le c(n-2)^2$:

$$
\begin{aligned}
T(n) &= T(n-2) + 2n \\
&\le c(n-2)^2 + 2n \\
&= c(n^2 - 4n + 4) + 2n \\
&= cn^2 - 4cn + 4c + 2n \\
&= cn^2 + (2 - 4c)n + 4c
\end{aligned}
$$

Imponiamo che $(2 - 4c)n + 4c \le 0$.
Scegliendo $c = 1$, otteniamo $-2n + 4 \le 0 \implies n \ge 2$. La disuguaglianza regge, dimostrando che $T(n) = \mathcal{O}(n^2)$.

**Limite Inferiore $\Omega(n^2)$:**
Vogliamo $\exists d > 0$ tale che $T(n) \ge dn^2$. Assumiamo $T(n-2) \ge d(n-2)^2$:

$$
\begin{aligned}
T(n) &= T(n-2) + 2n \\
&\ge d(n-2)^2 + 2n \\
&= d(n^2 - 4n + 4) + 2n \\
&= dn^2 - 4dn + 4d + 2n \\
&= dn^2 + (2 - 4d)n + 4d
\end{aligned}
$$

Imponiamo che $(2 - 4d)n + 4d \ge 0$.
Per $d = \frac{1}{2}$, il termine lineare si annulla e otteniamo $+2 \ge 0$, che è sempre vero. Questo dimostra che $T(n) = \Omega(n^2)$.

Pertanto, $T(n) = \Theta(n^2)$.

---

### (3) Master Theorem per $T(n) = 4T(n/2) + n\log n$

Identifichiamo i parametri del Master Theorem: $a = 4$, $b = 2$, e $f(n) = n\log n$.
Calcoliamo lo spartiacque asintotico:

$$ n^{\log_b a} = n^{\log_2 4} = n^2 $$

Confrontiamo la watershed function con $f(n)$. Poiché $n^2 \gg n\log n$, ci troviamo in un possibile **Caso 1**.
Verifichiamo se $f(n) = \mathcal{O}(n^{\log_b a - \varepsilon})$ per un qualche $\varepsilon > 0$.

Scegliendo, ad esempio, $\varepsilon = 0.5$, si ha $f(n) = n\log n = \mathcal{O}(n^{1.5})$, che è verificato.
Possiamo concludere direttamente per il Caso 1 del Master Theorem che:

$$ T(n) = \Theta(n^{\log_b a}) = \Theta(n^2) $$

---

### (4) Master Theorem per $T(n) = 4T(n/2) + n^2\sqrt{n}$

Identifichiamo i parametri: $a = 4$, $b = 2$, e $f(n) = n^2\sqrt{n} = n^{2.5}$.
Calcoliamo lo spartiacque asintotico:

$$ n^{\log_b a} = n^{\log_2 4} = n^2 $$

Essendo $n^2 < n^{2.5}$, siamo in un possibile **Caso 3**.
Verifichiamo la condizione $f(n) = \Omega(n^{\log_b a + \varepsilon})$ per un $\varepsilon > 0$. Scegliendo $\varepsilon = 0.4$, la condizione $n^{2.5} = \Omega(n^{2.4})$ è banalmente soddisfatta.

Essendo nel Caso 3, dobbiamo verificare anche la **condizione di regolarità**: $\exists k < 1$ tale che $a \cdot f(n/b) \le k \cdot f(n)$.

$$
4 \cdot f\left(\frac{n}{2}\right) = 4 \cdot \left(\frac{n^2}{4}\sqrt{\frac{n}{2}}\right) = 4 \cdot \frac{n^2}{4} \cdot \frac{\sqrt{n}}{\sqrt{2}} = \frac{1}{\sqrt{2}}n^{2.5}
$$

Imponiamo la disuguaglianza:

$$ \frac{1}{\sqrt{2}}n^{2.5} \le k(n^{2.5}) $$

Questo vale per $\frac{1}{\sqrt{2}} \le k < 1$. La condizione di regolarità è quindi verificata.
Possiamo concludere per il Caso 3 del Master Theorem che:

$$ T(n) = \Theta(f(n)) = \Theta(n^2\sqrt{n}) $$
