# Domanda A — Classe $\Omega$

Assumendo che $f(n) = \Omega(n^2)$, si dimostri se la seguente affermazione è vera:
$$f(n) + g(n) = \Omega(n^2 + g(n))$$
Vale anche la seguente?
$$f(n) - g(n) = \Omega(n^2 - g(n))$$
Dimostrarlo oppure fornire un controesempio.

---

### i. Dimostrazione della prima affermazione

Siano $f(n)$ e $g(n)$ due funzioni arbitrarie asintoticamente positive, ricordiamo la definizione della classe $\Omega$:

$$
\Omega(f(n)) = \{h(n) \mid \exists d > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0 : 0 \le d \cdot f(n) \le h(n)\}
$$

Vogliamo dimostrare che:
$$f(n) = \Omega(n^2) \implies f(n) + g(n) = \Omega(n^2 + g(n))$$

Dall'ipotesi $f(n) = \Omega(n^2)$ segue, per definizione della classe $\Omega$, che $\exists d_1 > 0, \exists n_1 \in \mathbb{N}$ tale che:
$$f(n) \ge d_1n^2 \quad \text{per ogni } n \ge n_1$$

Essendo che $g(n) > 0$ (per l'assunzione di positività asintotica), possiamo sommare $g(n)$ a entrambi i lati della disuguaglianza:
$$f(n) + g(n) \ge d_1n^2 + g(n)$$

Vogliamo ricondurci alla forma richiesta dalla tesi. Se ora scegliamo una costante $d = \min(d_1, 1)$, poiché $d_1 > 0$, segue che anche $d > 0$.
Inoltre, per definizione di minimo, abbiamo che $d \le d_1$ e $d \le 1$. Di conseguenza possiamo minorare il lato destro:

$$
f(n) + g(n) \ge d_1n^2 + 1 \cdot g(n) \ge d n^2 + d g(n) = d(n^2 + g(n))
$$

Abbiamo trovato una costante $d > 0$ che soddisfa la disuguaglianza. Quindi segue, dalla definizione della classe $\Omega$, che $f(n) + g(n) = \Omega(n^2 + g(n))$, dimostrando la prima affermazione.

---

### ii. Controesempio per la seconda affermazione

Ci viene richiesto di mostrare se vale:
$$f(n) = \Omega(n^2) \implies f(n) - g(n) = \Omega(n^2 - g(n))$$

Questa affermazione **non è vera**.
Possiamo dimostrarlo fornendo un controesempio. Scegliamo:
- $f(n) = \frac{1}{2}n^2$
- $g(n) = \frac{1}{2}n^2 - n$

Entrambe le funzioni sono asintoticamente positive e l'ipotesi $f(n) = \Omega(n^2)$ è chiaramente rispettata.

Calcoliamo i due termini della disuguaglianza:
$$f(n) - g(n) = \frac{1}{2}n^2 - \left(\frac{1}{2}n^2 - n\right) = n$$
$$n^2 - g(n) = n^2 - \left(\frac{1}{2}n^2 - n\right) = \frac{1}{2}n^2 + n$$

Se l'affermazione fosse vera, dovrebbe valere che $n = \Omega\left(\frac{1}{2}n^2 + n\right)$.
Per definizione della classe $\Omega$, dovrebbe esistere una costante $d > 0$ e un $n_0 \in \mathbb{N}$ tali che per ogni $n \ge n_0$:
$$n \ge d\left(\frac{1}{2}n^2 + n\right)$$

Dividendo entrambi i lati per il blocco tra parentesi (lecito per $n > 0$), isoliamo $d$:
$$d \le \frac{n}{\frac{1}{2}n^2 + n}$$

Calcolando il limite per $n \to +\infty$, vediamo come si comporta questo vincolo asintoticamente:
$$
\lim_{n\to +\infty} \frac{n}{\frac{1}{2}n^2 + n} = 0
$$

Poiché il limite è $0$, significa che definitivamente (per $n$ sufficientemente grande) il valore $\frac{n}{\frac{1}{2}n^2 + n}$ diventa più piccolo di qualsiasi costante positiva prefissata. Quindi, la disuguaglianza imporrebbe $d \le 0$, il che entra in palese contraddizione con la definizione della classe $\Omega$ che esige rigorosamente $d > 0$.

Quindi, la seconda affermazione è falsa.
