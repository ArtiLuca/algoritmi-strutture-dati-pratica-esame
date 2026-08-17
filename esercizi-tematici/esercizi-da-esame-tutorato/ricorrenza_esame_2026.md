# Esercizio Ricorrenza da Esame

**Domanda A (6 punti)**
Data la ricorrenza $T(n) = \frac{3}{2}T(n-1) + 2$, mostrare che la soluzione è $\mathcal{O}(2^n)$.
Vale anche $T(n) = \Omega(2^n)$? Motivare la risposta.

---

### i. Dimostrazione limite superiore $\mathcal{O}(2^n)$

Per dimostrare che vale $T(n) = \mathcal{O}(2^n)$, dobbiamo mostrare che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \le c \cdot 2^n$.

Assumiamo come ipotesi induttiva che questo sia vero per valori di $m < n$, cioè che valga $T(m) \le c \cdot 2^m$.
Applicando l'ipotesi induttiva alla nostra ricorrenza (il che è lecito dato che $n-1 < n$) abbiamo:

$$
\begin{aligned}
T(n) &= \frac{3}{2}T(n-1) + 2 \\
&\le \frac{3}{2}(c2^{n-1}) + 2 \\
&= \frac{3}{2}\left(c\frac{2^n}{2}\right) + 2 \\
&= \frac{3}{4}c2^n + 2
\end{aligned}
$$

Vogliamo che $\frac{3}{4}c2^n + 2 \le c2^n$.
Sottraendo il termine con la $c$ da entrambe le parti otteniamo:

$$ 2 \le \frac{1}{4}c2^n $$

Poiché $2^n \ge 1$ per ogni $n \ge 0$, per far sì che la disuguaglianza valga sempre è sufficiente imporre che il limite sia coperto per il caso base $2^n = 1$, ovvero:

$$ 2 \le \frac{1}{4}c \implies c \ge 8 $$

Una scelta di $c = 8$ e $n_0$ sufficientemente grande ($n_0 \ge 0$) è sufficiente per dimostrare che vale $T(n) = \mathcal{O}(2^n)$ per ogni $n \ge n_0$.

---

### ii. Verifica limite inferiore $\Omega(2^n)$

Per quanto riguarda la seconda affermazione, ovvero $T(n) = \Omega(2^n)$, dimostreremo che questa è **falsa**.

Se provassimo a dimostrare per assurdo che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \ge d2^n$ operando in modo speculare a prima, arriveremmo alla seguente disuguaglianza:

$$ \frac{3}{4}d2^n + 2 \ge d2^n $$

Che possiamo riscrivere isolando il $2$:

$$ 2 \ge \frac{1}{4}d2^n \implies d \le \frac{8}{2^n} $$

Tuttavia, il limite del valore $\frac{8}{2^n}$ tende a $0$ per $n \to \infty$.
Di conseguenza, non può esistere alcuna costante fissa e strettamente positiva $d > 0$ (come richiesto matematicamente per la definizione della classe $\Omega$) che possa soddisfare la disuguaglianza $d \le \frac{8}{2^n}$ al crescere di $n$.

Pertanto, la seconda affermazione $T(n) = \Omega(2^n)$ è falsa. (Nota: Srotolando la ricorrenza in modo esatto, si può verificare che la base esponenziale reale è $\frac{3}{2}$, portando a una complessità esatta di $\Theta(1.5^n)$, che giustifica il limite superiore $2^n$ ma ne smentisce il limite inferiore).
