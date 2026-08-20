# Esercizio 10 - Master Theorem con frazione

Si consideri la ricorrenza:

$$
T(n) = T\left(\frac{4n}{5}\right) + \frac{n}{2} + \log n
$$

Fornire un limite asintotico stretto per la soluzione.

---

### i. Applicazione del Master Theorem

Riscriviamo la ricorrenza nella forma standard $T(n) = a T(n/b) + f(n)$. Otteniamo:
- $a = 1 \ge 1$
- $b = \frac{5}{4} > 1$
- $f(n) = \frac{n}{2} + \log n$

Calcoliamo lo spartiacque asintotico:

$$
n^{\log_b a} = n^{\log_{5/4} 1} = n^0 = 1
$$

Essendo che $f(n) \gg 1$, ci troviamo in un possibile **Caso 3** del Master Theorem.

Per verificare la prima condizione richiesta dal Caso 3, dobbiamo assicurarci che $\exists \varepsilon > 0$ tale per cui:

$$
f(n) = \Omega(n^{\log_b a + \varepsilon})
$$

Usando il metodo del limite, valutiamo:

$$
\lim_{n\to \infty} \frac{f(n)}{n^{0+\varepsilon}} = \lim_{n\to \infty} \frac{\frac{n}{2} + \log n}{n^{\varepsilon}} = +\infty
$$

Questo limite è uguale a $+\infty$ per ogni scelta di $0 < \varepsilon < 1$ (poiché al numeratore domina il termine lineare $n^1$, che cresce più velocemente di $n^\varepsilon$). La prima condizione è dunque soddisfatta.

---

### ii. Condizione di Regolarità

Per il Caso 3, serve inoltre verificare la condizione di regolarità, ovvero che valga:

$$
a f\left(\frac{n}{b}\right) \le k f(n)
$$

per un qualche $k < 1$ e per $n$ sufficientemente grande.
Sostituendo i nostri valori:

$$
a f\left(\frac{n}{b}\right) = 1 \cdot f\left(\frac{4n}{5}\right) = \frac{\frac{4n}{5}}{2} + \log\left(\frac{4n}{5}\right) = \frac{2n}{5} + \log n - \log\left(\frac{5}{4}\right)
$$

Dobbiamo quindi verificare la disuguaglianza:

$$
\frac{2n}{5} + \log n - \log\left(\frac{5}{4}\right) \le k\left(\frac{n}{2} + \log n\right)
$$

Per trovare un $k$ idoneo, calcoliamo il limite del rapporto tra i due lati per $n \to \infty$:

$$
\lim_{n\to\infty} \frac{\frac{2n}{5} + \log n - \log\left(\frac{5}{4}\right)}{\frac{n}{2} + \log n} = \frac{\frac{2}{5}}{\frac{1}{2}} = \frac{4}{5}
$$

Quindi, per $n$ sufficientemente grande, il rapporto tende a $\frac{4}{5}$. Una qualsiasi costante $k$ scelta in modo che $\frac{4}{5} < k < 1$ (ad esempio $k = \frac{9}{10}$) soddisferà la disuguaglianza. La condizione di regolarità è quindi verificata.

---

### iii. Conclusione

Avendo dimostrato entrambe le condizioni, possiamo concludere tramite il Caso 3 del Master Theorem che la soluzione asintotica è dominata da $f(n)$:

$$
T(n) = \Theta(f(n)) = \Theta\left(\frac{n}{2} + \log n\right)
$$

Trascurando i termini di ordine inferiore ($\log n$) e la costante moltiplicativa ($\frac{1}{2}$), il limite asintotico stretto risulta infine:

$$
T(n) = \Theta(n)
$$
