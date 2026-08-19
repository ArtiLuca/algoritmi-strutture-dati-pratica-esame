# Esercizio 7 - Master Theorem

Sia data la seguente equazione di ricorrenza:
$$ T(n) = 5T(\lfloor n/3 \rfloor) + 2n^2 $$

Si fornisca un limite asintotico stretto per la soluzione.

---

### i. Applicazione del Master Theorem

Identifichiamo i parametri della ricorrenza: $a = 5$, $b = 3$, e $f(n) = 2n^2$.
Calcoliamo lo spartiacque asintotico:

$$ n^{\log_b a} = n^{\log_3 5} \approx n^{1.46} $$

Confrontando la funzione $f(n)$ con lo spartiacque, notiamo che l'esponente di $f(n)$ è 2, mentre $1.46 < 2$. Ci troviamo quindi in un possibile **Caso 3** del Master Theorem.

Verifichiamo la prima condizione, ovvero che $\exists \varepsilon > 0$ tale per cui valga:

$$ f(n) = \Omega(n^{\log_b a + \varepsilon}) $$

Calcoliamo il limite per verificare l'andamento asintotico:

$$ \lim_{n \to \infty} \frac{2n^2}{n^{\log_3 5 + \varepsilon}} = +\infty $$

Questo limite tende a infinito (confermando la classe $\Omega$) per qualsiasi valore di $\varepsilon$ scelto nell'intervallo $0 < \varepsilon < 2 - \log_3 5$. La prima condizione è quindi soddisfatta.

---

### ii. Condizione di Regolarità

Essendo nel Caso 3, dobbiamo verificare anche la condizione di regolarità, ovvero che $\exists k < 1$ tale che per $n$ sufficientemente grande valga:

$$ a f\left(\frac{n}{b}\right) \le k f(n) $$

Sostituendo i nostri valori otteniamo:

$$ 5 \left( 2\left(\frac{n}{3}\right)^2 \right) = 5 \left( \frac{2n^2}{9} \right) = \frac{10}{9}n^2 \le k(2n^2) $$

Usando il limite del rapporto per isolare $k$:

$$ \lim_{n \to \infty} \frac{\frac{10}{9}n^2}{2n^2} = \frac{10}{18} = \frac{5}{9} $$

Quindi, una scelta qualsiasi di $k$ tale che $\frac{5}{9} \le k < 1$ soddisfa pienamente la disuguaglianza. La condizione di regolarità è verificata.

---

### iii. Conclusione

Avendo dimostrato con successo entrambe le condizioni, possiamo concludere formalmente tramite il Caso 3 del Master Theorem che la complessità è dominata asintoticamente dal termine $f(n)$:

$$ T(n) = \Theta(f(n)) = \Theta(n^2) $$
