# Soluzione - Domanda A

Abbiamo la ricorrenza:
$$T(n) = \frac{3}{2}T(n-1) + 2$$

## Dimostrazione del limite superiore: $T(n) = O(2^n)$

Dimostriamo che $\exists c > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0$ valga $T(n) \le c \cdot 2^n$.

Assumo come ipotesi induttiva che valga per $n-1$, ovvero:
$$T(n-1) \le c \cdot 2^{n-1}$$

Applicando l'ipotesi induttiva alla ricorrenza abbiamo:
$$T(n) = \frac{3}{2}T(n-1) + 2 \le \frac{3}{2}(c \cdot 2^{n-1}) + 2$$

Sviluppando otteniamo:
$$= \frac{3}{2}c \cdot \frac{2^n}{2} + 2 = \frac{3}{4}c \cdot 2^n + 2$$

Quindi vogliamo dimostrare ora che:
$$\frac{3}{4}c \cdot 2^n + 2 \le c \cdot 2^n$$

Spostando i termini otteniamo:
$$2 \le \frac{1}{4}c \cdot 2^n \implies c \ge \frac{8}{2^n}$$

Quindi, considerando $n \ge 0$, con una scelta opportuna di $c \ge 8$ e $n_0 = 0$ si dimostra che $T(n) = O(2^n)$.

---

## Dimostrazione del limite inferiore: $T(n) = \Omega(2^n)$

Si può dimostrare che **non vale** che $T(n) = \Omega(2^n)$. Infatti, se provassimo a dimostrare che:
$$\exists d > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0 \implies T(n) \ge d \cdot 2^n$$
si vedrebbe che la disuguaglianza non regge.

Infatti, procedendo in modo analogo al limite superiore, assumendo come ipotesi induttiva che questo sia vero per $n-1$, ovvero che valga:
$$T(n-1) \ge d \cdot 2^{n-1}$$

Applicando alla ricorrenza otterremmo:
$$T(n) = \frac{3}{2}T(n-1) + 2 \ge \frac{3}{2}(d \cdot 2^{n-1}) + 2 = \frac{3}{4}d \cdot 2^n + 2$$

Vogliamo che:
$$\frac{3}{4}d \cdot 2^n + 2 \ge d \cdot 2^n$$

Ovvero che:
$$2 \ge \frac{1}{4}d \cdot 2^n$$

Si vede subito che questo **non vale** $\forall n \ge n_0$ perché la parte a sinistra è una costante, mentre il valore a destra cresce in base al valore di $n$. Infatti, per $n$ che tende all'infinito, si ha che:
$$\lim_{n \to \infty} \frac{2}{\frac{1}{4}d \cdot 2^n} = 0$$
Ovvero, $\nexists d > 0$ che soddisfi la disuguaglianza $\forall n \ge n_0$.

Quindi la seconda affermazione $T(n) = \Omega(2^n)$ **non è vera**.
