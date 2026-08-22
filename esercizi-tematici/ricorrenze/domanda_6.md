### **Domanda 6**

Sia data la seguente equazione di ricorrenza:

$$ 
T(n) = \begin{cases} 
1 & \text{se } n = 1 \\ 
3T(n/5) + T(n/6) + n & \text{se } n > 1 
\end{cases} 
$$

Si fornisca un limite asintotico stretto per la soluzione.

---

### i. Idea e Ipotesi

Essendo che il caso $n > 1$ è una somma di termini lineari la cui "frazione" ricorsiva totale è $\frac{3}{5} + \frac{1}{6} = \frac{23}{30} < 1$, ipotizzo come soluzione asintotica stretta $T(n) = \Theta(n)$.
Provo quindi a dimostrare separatamente un limite superiore ($\mathcal{O}$) e un limite inferiore ($\Omega$) tramite il metodo di sostituzione.

---

### ii. Limite superiore: $\mathcal{O}(n)$

Vogliamo dimostrare che $T(n) = \mathcal{O}(n)$, ovvero che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \le cn$.

Assumendo come ipotesi induttiva che questo valga per valori $m < n$, ovvero che valga $T(m) \le cm$, possiamo applicare l'ipotesi induttiva alla nostra ricorrenza (il che è lecito perché $\frac{n}{5} < n$ e $\frac{n}{6} < n$ per $n > 1$):

$$
T(n) = 3T\left(\frac{n}{5}\right) + T\left(\frac{n}{6}\right) + n \le 3c\left(\frac{n}{5}\right) + c\left(\frac{n}{6}\right) + n = \frac{23}{30}cn + n = \left(\frac{23}{30}c + 1\right)n
$$

Affinché la dimostrazione sia valida, vogliamo che il risultato sia minore o uguale alla nostra ipotesi $cn$:

$$
\left(\frac{23}{30}c + 1\right)n \le cn
$$

Dividendo per $n$ (lecito perché $n \ge 1$) otteniamo la disuguaglianza:

$$
\frac{23}{30}c + 1 \le c \implies 1 \le \frac{7}{30}c \implies c \ge \frac{30}{7}
$$

Poiché $\frac{30}{7} \approx 4.28$, una scelta di $c = 5$ soddisfa il passo induttivo. Inoltre, tale scelta soddisfa anche il caso base $T(1)=1 \le 5$.
Possiamo quindi concludere che $T(n) = \mathcal{O}(n)$.

---

### iii. Limite inferiore: $\Omega(n)$

Vogliamo dimostrare che $T(n) = \Omega(n)$, ovvero che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \ge dn$.

Assumendo come ipotesi induttiva che questo valga per valori $m < n$, ovvero che valga $T(m) \ge dm$, possiamo applicare l'ipotesi induttiva alla nostra ricorrenza:

$$
T(n) = 3T\left(\frac{n}{5}\right) + T\left(\frac{n}{6}\right) + n \ge 3d\left(\frac{n}{5}\right) + d\left(\frac{n}{6}\right) + n = \frac{23}{30}dn + n = \left(\frac{23}{30}d + 1\right)n
$$

Affinché la dimostrazione sia valida, vogliamo che:

$$
\left(\frac{23}{30}d + 1\right)n \ge dn
$$

Dividendo per $n$ (lecito perché $n \ge 1$) abbiamo la disuguaglianza:

$$
\frac{23}{30}d + 1 \ge d \implies 1 \ge \frac{7}{30}d \implies d \le \frac{30}{7}
$$

Una scelta di $d = 1$ soddisfa il passo induttivo e anche il caso base $T(1)=1 \ge 1$.
Possiamo quindi concludere che $T(n) = \Omega(n)$.

---

### iv. Conclusione

Avendo dimostrato formalmente sia il limite superiore che il limite inferiore, posso dunque concludere per il teorema della doppia implicazione asintotica che l'ipotesi iniziale è corretta:

$$
T(n) = \Theta(n)
$$
