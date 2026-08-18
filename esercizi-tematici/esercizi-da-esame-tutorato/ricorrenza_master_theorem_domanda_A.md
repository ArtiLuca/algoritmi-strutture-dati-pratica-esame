# Esercizio Ricorrenza da Esame

**Domanda A (6 punti)**
Dare una soluzione asintotica per la ricorrenza

$$ 
T(n) = 4T(n/2) + n^3 + 1 
$$

---

### i. Applicazione del Master Theorem

Identifichiamo i parametri della ricorrenza: $a = 4$, $b = 2$, e $f(n) = n^3 + 1$.
Calcoliamo la funzione soglia del Master Theorem:

$$ n^{\log_b a} = n^{\log_2 4} = n^2 $$

Confrontiamo $f(n)$ con $n^2$. Poiché $f(n)$ è un polinomio di grado 3, cresce asintoticamente più in fretta di $n^2$, indicando che ci troviamo in un possibile **Caso 3** del Master Theorem.

Verifichiamo la prima condizione del Caso 3, ovvero che $\exists \varepsilon > 0$ tale per cui $f(n) = \Omega(n^{\log_b a + \varepsilon})$.
Calcoliamo il limite per la verifica asintotica:

$$ \lim_{n \to \infty} \frac{n^3 + 1}{n^{2+\varepsilon}} = \lim_{n \to \infty} \frac{n^3}{n^{2+\varepsilon}} + \frac{1}{n^{2+\varepsilon}} $$

Scegliendo, ad esempio, $\varepsilon = 0.5$, otteniamo al denominatore $n^{2.5}$. Poiché il numeratore ha grado 3 e il denominatore grado 2.5, il limite tende a $+\infty$, soddisfacendo la condizione.

---

### ii. Condizione di Regolarità

Essendo nel Caso 3, dobbiamo verificare anche la **condizione di regolarità**: $\exists k < 1$ e un $n_0$ tale che, per ogni $n \ge n_0$, valga $a \cdot f(n/b) \le k \cdot f(n)$.

Sostituendo i nostri valori:

$$
4 \cdot f\left(\frac{n}{2}\right) = 4 \left( \left(\frac{n}{2}\right)^3 + 1 \right) = 4 \left( \frac{n^3}{8} + 1 \right) = \frac{1}{2}n^3 + 4
$$

Vogliamo che:

$$ \frac{1}{2}n^3 + 4 \le k(n^3 + 1) $$

Affinché questa disuguaglianza sia vera per un $n$ sufficientemente grande, ci basta scegliere un qualsiasi $k$ strettamente compreso tra $\frac{1}{2}$ e $1$.
Ad esempio, scegliendo $k = \frac{3}{4}$ otteniamo:

$$ \frac{1}{2}n^3 + 4 \le \frac{3}{4}n^3 + \frac{3}{4} \implies \frac{1}{4}n^3 \ge 3.25 \implies n^3 \ge 13 $$

Questa disuguaglianza è sempre verificata per ogni $n \ge 3$. La condizione di regolarità è quindi soddisfatta.

---

### iii. Conclusione

Avendo verificato sia la condizione di crescita polinomiale maggiore che la condizione di regolarità, possiamo concludere tramite il Caso 3 del Master Theorem che la complessità asintotica è dominata dal termine $f(n)$:

$$ T(n) = \Theta(f(n)) = \Theta(n^3) $$
