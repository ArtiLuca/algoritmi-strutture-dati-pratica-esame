# Domanda A — Ricorrenze e classi $\mathcal{O}$ e $\Omega$

Data la ricorrenza:

$$
T(n) = \frac{3}{2}T(n-1) + 2
$$

mostrare che la soluzione è $\mathcal{O}(2^n)$.
Vale anche $T(n) = \Omega(2^n)$? Motivare la risposta.

---

### i. Dimostrazione limite superiore $\mathcal{O}(2^n)$

Per dimostrare che $T(n) = \mathcal{O}(2^n)$, dobbiamo provare che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tali che:

$$
T(n) \le c 2^n \quad \forall n \ge n_0
$$

Procediamo per induzione matematica (metodo della sostituzione). Assumiamo che l'ipotesi valga per valori $m < n$ (in particolare per $n-1$, ovvero $T(n-1) \le c2^{n-1}$) e sostituiamo nella ricorrenza:

$$
T(n) = \frac{3}{2}T(n-1) + 2 \le \frac{3}{2} c (2^{n-1}) + 2
$$

Riscriviamo $2^{n-1}$ come $\frac{2^n}{2}$:

$$
T(n) \le \frac{3}{2} c \frac{2^n}{2} + 2 = \frac{3}{4} c 2^n + 2
$$

Vogliamo che questo risultato sia $\le c 2^n$. Imponiamo quindi la disuguaglianza:

$$
\frac{3}{4} c 2^n + 2 \le c 2^n
$$

Sottraendo $\frac{3}{4} c 2^n$ da entrambi i lati otteniamo:

$$
2 \le \frac{1}{4} c 2^n \implies c \ge \frac{8}{2^n}
$$

Essendo che la quantità $\frac{8}{2^n}$ decresce al crescere di $n$, ci basta scegliere un valore per $n_0$ e prendere il $c$ corrispondente. Scegliendo $n_0 = 1$, otteniamo $c \ge 4$. Una scelta di $c = 8$ (che copre anche il caso $n=0$) e $n_0 = 1$ soddisfa pienamente la condizione. Abbiamo così dimostrato che $T(n) = \mathcal{O}(2^n)$.

---

### ii. Analisi per il limite inferiore $\Omega(2^n)$

Una dimostrazione per sostituzione dell'ipotesi $T(n) = \Omega(2^n)$ fallisce. Infatti, cercando $d > 0$ tale che $T(n) \ge d 2^n$, otterremmo $d \le \frac{8}{2^n}$. Poiché $\lim_{n \to \infty} \frac{8}{2^n} = 0$, non esiste alcuna costante $d > 0$ che possa soddisfare la disuguaglianza definitivamente. Tuttavia, il fallimento del metodo della sostituzione non è una prova sufficiente per smentire la classe $\Omega$.

Per dimostrare rigorosamente che l'affermazione è falsa, procediamo espandendo la ricorrenza (metodo iterativo o *unfolding*):

$$
T(n) = \frac{3}{2}T(n-1) + 2
$$

$$
T(n) = \frac{3}{2}\left[\frac{3}{2}T(n-2)+2\right] + 2 = \left(\frac{3}{2}\right)^2 T(n-2) + 2\left(\frac{3}{2}\right) + 2
$$

$$
T(n) = \left(\frac{3}{2}\right)^2\left[\frac{3}{2}T(n-3)+2\right] + 2\left(\frac{3}{2}\right) + 2 = \left(\frac{3}{2}\right)^3 T(n-3) + 2\left(\frac{3}{2}\right)^2 + 2\left(\frac{3}{2}\right) + 2
$$

Ad un generico passo $k$, l'equazione diventa:

$$
T(n) = \left(\frac{3}{2}\right)^k T(n-k) + 2 \sum_{i=0}^{k-1} \left(\frac{3}{2}\right)^i
$$

Assumendo come caso base $T(0) = 0$ (o una qualsiasi costante) ed espandendo fino a $k = n$:

$$
T(n) = \left(\frac{3}{2}\right)^n T(0) + 2 \sum_{i=0}^{n-1} \left(\frac{3}{2}\right)^i
$$

Possiamo calcolare il valore esatto usando la formula della serie geometrica finita per la sommatoria:

$$
\sum_{i=0}^{n-1} \left(\frac{3}{2}\right)^i = \frac{\left(\frac{3}{2}\right)^n - 1}{\frac{3}{2} - 1} = \frac{\left(\frac{3}{2}\right)^n - 1}{\frac{1}{2}} = 2 \cdot \left[ \left(\frac{3}{2}\right)^n - 1 \right]
$$

Sostituendo il risultato, otteniamo la forma chiusa asintotica:

$$
T(n) \approx 2 \cdot 2 \cdot \left(\frac{3}{2}\right)^n = 4 \cdot \left(\frac{3}{2}\right)^n - 4 = \Theta\left(1.5^n\right)
$$

Avendo dimostrato che la ricorrenza cresce esattamente come $\Theta(1.5^n)$, possiamo concludere con certezza matematica che non può valere $T(n) = \Omega(2^n)$, poiché $1.5 < 2$ e quindi la funzione asintoticamente è strettamente più lenta. L'affermazione è pertanto **falsa**.
