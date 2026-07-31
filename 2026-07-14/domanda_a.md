# Soluzione - Domanda A

Abbiamo la ricorrenza:

$$T(n)=\frac{3}{2}T(n-1)+2$$

## Dimostrazione del limite superiore: $T(n) = O(2^n)$

Vogliamo dimostrare che:

$$\exists c>0,\ \exists n_0\in\mathbb{N},\ \forall n\ge n_0: T(n)\le c\cdot 2^n$$

Assumiamo come ipotesi induttiva che la proprietà valga per $n-1$, cioè:

$$T(n-1)\le c\cdot 2^{n-1}$$

Applicando l'ipotesi induttiva alla ricorrenza otteniamo:

$$T(n) = \frac{3}{2}T(n-1)+2 \le \frac{3}{2}\left(c\cdot 2^{n-1}\right)+2$$

Quindi:

$$T(n) \le \frac{3}{4}c\cdot 2^n + 2$$

Per concludere la dimostrazione vogliamo che:

$$\frac{3}{4}c\cdot 2^n + 2 \le c\cdot 2^n$$

Spostando i termini:

$$2 \le \frac{1}{4}c\cdot 2^n$$

Questa disuguaglianza è vera, per esempio, scegliendo $c \ge 8$ e considerando $n \ge 0$.

Infatti, per $n \ge 0$ vale $2^n \ge 1$, quindi:

$$\frac{1}{4}c\cdot 2^n \ge \frac{1}{4}\cdot 8 \cdot 1 = 2$$

Con una scelta opportuna della costante $c$, che tenga conto anche del caso base, segue che:

$$T(n)=O(2^n)$$

---

## Dimostrazione del limite inferiore: $T(n) = \Omega(2^n)$

La seconda affermazione, invece, **non è vera**.

Per dimostrarlo in modo più preciso, espandiamo la ricorrenza.

Per semplicità, assumiamo un caso base costante $T(0)$. Allora:

$$T(n) = \left(\frac{3}{2}\right)^n T(0) + 2\sum_{k=0}^{n-1}\left(\frac{3}{2}\right)^k$$

La somma geometrica vale:

$$\sum_{k=0}^{n-1}\left(\frac{3}{2}\right)^k = \frac{\left(\frac{3}{2}\right)^n-1}{\frac{3}{2}-1} = 2\left(\left(\frac{3}{2}\right)^n-1\right)$$

Quindi:

$$T(n) = \left(\frac{3}{2}\right)^n T(0) + 4\left(\left(\frac{3}{2}\right)^n-1\right)$$

Ovvero:

$$T(n) = (T(0)+4)\left(\frac{3}{2}\right)^n-4$$

Quindi la ricorrenza cresce asintoticamente come:

$$T(n)=\Theta\left(\left(\frac{3}{2}\right)^n\right)$$

Ora confrontiamo $T(n)$ con $2^n$.

Consideriamo il rapporto:

$$\frac{T(n)}{2^n} = \frac{(T(0)+4)\left(\frac{3}{2}\right)^n-4}{2^n}$$

Separando i termini:

$$\frac{T(n)}{2^n} = (T(0)+4)\left(\frac{3}{4}\right)^n - \frac{4}{2^n}$$

Facendo tendere $n$ all'infinito:

$$\lim_{n\to\infty}\frac{T(n)}{2^n}=0$$

Questo significa che $T(n)$ cresce strettamente più lentamente di $2^n$.

Quindi non può esistere una costante $d > 0$ tale che, definitivamente:

$$T(n)\ge d\cdot 2^n$$

Perciò:

$$T(n)\ne \Omega(2^n)$$

In conclusione:

$$T(n)=O(2^n)$$

ma:

$$T(n)\ne \Omega(2^n)$$
