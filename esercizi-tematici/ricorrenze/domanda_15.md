# Domanda 16

Data la ricorrenza $T(n) = 5T(n/3) + (n - 2)^2$, trovare la soluzione asintotica.

---

### i. Applicazione del Master Theorem

Provo ad usare il Master Theorem identificando i parametri:
- $f(n) = (n-2)^2$
- $a = 5 \ge 1$
- $b = 3 > 1$

Calcoliamo lo spartiacque asintotico:

$$
n^{\log_b a} = n^{\log_3 5} \approx n^{1.46}
$$

Essendo che $1.46 < 2$ siamo in un possibile **CASO 3**, quindi per prima cosa verifico che $\exists \varepsilon > 0$ che soddisfa la prima condizione, ovvero $f(n) = \Omega(n^{\log_b a + \varepsilon})$.

Per farlo, uso il metodo del limite:

$$
\lim_{n\to \infty} \frac{f(n)}{n^{\log_b a + \varepsilon}} = +\infty
$$

ovvero:

$$
\lim_{n\to \infty} \frac{(n-2)^2}{n^{\log_3 5 + \varepsilon}} = +\infty
$$

che si può approssimare ai termini dominanti:

$$
\lim_{n\to \infty} \frac{n^2}{n^{1.46 + \varepsilon}} = + \infty
$$

Si vede che una scelta di $\varepsilon$ tale che $0 < 2 - (\log_3 5 + \varepsilon)$ soddisfa la prima condizione richiesta (il grado del numeratore rimane strettamente maggiore di quello del denominatore) e quindi vale:

$$
f(n) = \Omega(n^{\log_b a + \varepsilon})
$$

---

### ii. Condizione di Regolarità

Essendo nel CASO 3, dobbiamo anche verificare che $\exists k < 1$ tale che $a f\left(\frac{n}{b}\right) \le k f(n)$, quindi:

$$
a f\left(\frac{n}{b}\right) = 5\left(\frac{n}{3}-2\right)^2 = 5\left(\frac{n^2}{9} - \frac{4}{3}n + 4\right) = \frac{5}{9}n^2 - \frac{20}{3}n + 20
$$

$$
k f(n) = k(n-2)^2 = k(n^2 - 4n + 4)
$$

Quindi abbiamo la disuguaglianza:

$$
\frac{5}{9}n^2 - \frac{20}{3}n + 20 \le k(n^2 - 4n + 4)
$$

Possiamo usare il limite del rapporto e se troviamo un valore $l < 1$ allora possiamo scegliere un qualunque $k > l$:

$$
\lim_{n\to \infty} \frac{\frac{5}{9}n^2 - \frac{20}{3}n + 20}{n^2 - 4n + 4} = \lim_{n\to \infty} \frac{\frac{5}{9}n^2}{n^2} = \frac{5}{9}
$$

per $n \to \infty$.
Quindi una scelta di $\frac{5}{9} < k < 1$ soddisfa in pieno la condizione di regolarità.

---

### iii. Conclusione

Avendo dimostrato entrambe le condizioni necessarie, possiamo concludere per il CASO 3 del Master Theorem che:

$$
T(n) = \Theta(f(n)) = \Theta(n^2)
$$
