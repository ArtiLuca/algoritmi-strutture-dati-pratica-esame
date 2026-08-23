# Domanda A - Master Theorem

Si determini la soluzione asintotica della seguente equazione di ricorrenza:

$$
T(n) = 3T(n/3) + n^2 + 1
$$

---

### i. Applicazione del Master Theorem

Abbiamo un possibile **CASO 3** essendo che:

$$
n^{\log_b a} = n^{\log_3 3} = n^1 = n \ll f(n) = n^2 + 1
$$

Verifico che $\exists \varepsilon > 0$ tale che $f(n) = \Omega(n^{\log_b a + \varepsilon})$. Possiamo verificare usando il metodo del limite che questo vale per una qualsiasi scelta di $0 < \varepsilon < 1$, infatti vale:

$$
\lim_{n\to \infty} \frac{n^2+1}{n^{1+\varepsilon}} = + \infty
$$

per $0 < \varepsilon < 1$.

---

### ii. Condizione di Regolarità

Serve inoltre verificare la regolarità, ovvero che $a f\left(\frac{n}{b}\right) \le k f(n)$ per un $k < 1$.
Abbiamo quindi:

$$
3\left(\frac{n^2}{9} + 1\right) = \frac{1}{3}n^2 + 3  \le k(n^2+1)
$$

Usando il limite del rapporto troviamo:

$$
\lim_{n\to \infty} \frac{\frac{1}{3}n^2 + 3}{n^2 + 1} = \frac{1}{3}
$$

per $n \to \infty$, quindi basta scegliere un valore $k$ strettamente maggiore di questo, ovvero un valore $\frac{1}{3} < k < 1$ per soddisfare la regolarità.

---

### iii. Conclusione

Avendo verificato entrambe le condizioni del CASO 3, possiamo quindi concludere che:

$$
T(n) = \Theta(n^2)
$$
