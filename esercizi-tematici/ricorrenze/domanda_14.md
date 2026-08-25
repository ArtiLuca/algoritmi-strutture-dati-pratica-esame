# Domanda 14

Dare una soluzione asintotica per la ricorrenza $T(n) = 3T(n/2) + n(n + 1)$.

---

### i. Applicazione del Master Theorem

Riscriviamo la funzione costo sviluppando il prodotto: $f(n) = n(n+1) = n^2 + n$.
I parametri della ricorrenza sono:
- $a = 3$
- $b = 2$

Calcoliamo lo spartiacque asintotico:

$$
n^{\log_b a} = n^{\log_2 3} \approx n^{1.58}
$$

Essendo che $1.58 < 2$, il grado del polinomio $f(n)$ è strettamente maggiore, quindi siamo in un possibile **CASO 3**.
Per confermarlo, verifichiamo che $\exists \varepsilon > 0$ tale che $f(n) = \Omega(n^{\log_b a + \varepsilon})$. Applichiamo il metodo del limite:

$$
\lim_{n\to \infty} \frac{f(n)}{n^{\log_b a + \varepsilon}} = \lim_{n\to \infty} \frac{n^2 + n}{n^{\log_2 3 + \varepsilon}} = +\infty
$$

Si vede facilmente che una scelta di $\varepsilon$ tale che $0 < \varepsilon < 2 - \log_2 3$ (in modo che l'esponente al denominatore resti strettamente minore di 2) garantisce che il numeratore domini, soddisfacendo così la condizione.

---

### ii. Condizione di Regolarità

Essendo nel CASO 3, dobbiamo anche verificare la condizione di regolarità, ovvero che $\exists k < 1$ tale che $a f\left(\frac{n}{b}\right) \le k f(n)$ per $n$ sufficientemente grande:

$$
a f\left(\frac{n}{b}\right) = 3\left(\left(\frac{n}{2}\right)^2 + \frac{n}{2}\right) = 3\left(\frac{n^2}{4} + \frac{n}{2}\right) = \frac{3}{4}n^2 + \frac{3}{2}n
$$

$$
k f(n) = k(n^2 + n)
$$

Impostiamo quindi la disuguaglianza:

$$
\frac{3}{4}n^2 + \frac{3}{2}n \le k(n^2 + n)
$$

Possiamo trovare un limite inferiore per $k$ calcolando il limite del rapporto $\ell$:

$$
\ell = \lim_{n\to \infty} \frac{\frac{3}{4}n^2 + \frac{3}{2}n}{n^2 + n} = \lim_{n\to \infty} \frac{\frac{3}{4}n^2}{n^2} = \frac{3}{4}
$$

Quindi, affinché la disuguaglianza sia verificata, è sufficiente scegliere un valore $k$ tale che $\ell < k < 1$. Una scelta di $k = \frac{4}{5}$ (ovvero $0.8$, che è maggiore di $0.75$) soddisfa perfettamente la condizione di regolarità.

---

### iii. Conclusione

Avendo dimostrato entrambe le condizioni necessarie, possiamo concludere per il CASO 3 del Master Theorem che:

$$
T(n) = \Theta(f(n)) = \Theta(n^2)
$$
