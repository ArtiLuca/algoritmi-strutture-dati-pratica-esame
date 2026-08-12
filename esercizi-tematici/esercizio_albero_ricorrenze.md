# Esercizi Albero delle Ricorrenze

Usare l'albero delle ricorrenze per dare un'ipotesi di soluzione e poi dimostrare con il metodo di sostituzione:

- $T(n) = T(n/2) + n^3$
- $T(n) = 4T(n/3) + n$
- $T(n) = 4T(n/2) + n$
- $T(n) = 3T(n-1) + 1$

---

### (1) $T(n) = T(n/2) + n^3$

Proviamo a fare un’ipotesi con l'albero delle ricorrenze, indicando i livelli dalla radice fino alle foglie utilizzando $i = 0 \dots h$. Assumiamo che all'ultimo livello $h$ ci siano solo le foglie.

- $i=0$: si ha un solo problema con costo locale $n^3$
- $i=1$: genera un sottoproblema con costo $(n/2)^3 = n^3/8$
- $i=2$: genera un sottoproblema con costo $(n/4)^3 = n^3/64$
- $i=3$: genera un sottoproblema con costo $(n/8)^3 = n^3/512$

Ad un livello generico $i$ abbiamo un costo pari a:

$$ \left(\frac{n}{2^i}\right)^3 = \frac{n^3}{8^i} $$

L'albero termina quando raggiungiamo il livello delle foglie, in cui si avrà un sottoproblema di dimensione 1, ovvero $\frac{n}{2^i} = 1$, che accade quando $i = h = \log_2 n$.

Sommando i costi sui vari livelli, otteniamo:

$$ T(n) = \sum_{i=0}^{h-1} \frac{n^3}{8^i} + \Theta(1) $$

dove $h = \log_2 n$ e $\Theta(1)$ indica il costo costante dell'unica foglia all'ultimo livello.

Portando fuori il termine $n^3$:

$$ T(n) = n^3 \sum_{i=0}^{h-1} \left(\frac{1}{8}\right)^i + \Theta(1) $$

Ricordando la serie geometrica $\sum_{i=0}^{\infty} q^i = \frac{1}{1 - q}$, possiamo maggiorare la somma:

$$ \sum_{i=0}^{h-1} \left(\frac{1}{8}\right)^i < \frac{1}{1 - \frac{1}{8}} = \frac{1}{\frac{7}{8}} = \frac{8}{7} $$

Ipotizziamo quindi come soluzione $T(n) = \Theta(n^3)$.

**Dimostrazione con il metodo di sostituzione:**

Prima dimostriamo che $T(n) = \mathcal{O}(n^3)$, ovvero che $\exists c > 0, \exists n_0$ tali che $T(n) \le c n^3$ per ogni $n \ge n_0$.

Assumiamo per ipotesi induttiva che $T(n/2) \le c(n/2)^3$.

$$ T(n) = T(n/2) + n^3 \le c\left(\frac{n}{2}\right)^3 + n^3 = c\frac{n^3}{8} + n^3 = \left(\frac{c}{8} + 1\right)n^3 $$

Vogliamo che $\left(\frac{c}{8} + 1\right)n^3 \le c n^3$, quindi serve che:

$$ \frac{c}{8} + 1 \le c \implies 1 \le c - \frac{c}{8} \implies 1 \le \frac{7}{8}c \implies c \ge \frac{8}{7} $$

Una scelta di $c = 2$ e $n_0 \ge 1$ soddisfa la condizione, dimostrando che $T(n) = \mathcal{O}(n^3)$.

In modo analogo, dimostriamo che $T(n) = \Omega(n^3)$, scegliendo un $d > 0$ opportuno tale che $T(n) \ge d n^3$.

Assumiamo per ipotesi induttiva che $T(n/2) \ge d(n/2)^3$.

$$ T(n) = T(n/2) + n^3 \ge d\left(\frac{n}{2}\right)^3 + n^3 = \left(\frac{d}{8} + 1\right)n^3 $$

Vogliamo che $\left(\frac{d}{8} + 1\right)n^3 \ge d n^3$, quindi serve che:

$$ \frac{d}{8} + 1 \ge d \implies 1 \ge \frac{7}{8}d \implies d \le \frac{8}{7} $$

Una scelta di $d = 1$ e $n_0 \ge 1$ soddisfa la condizione, dimostrando che $T(n) = \Omega(n^3)$.

Avendo dimostrato sia il limite superiore che inferiore, possiamo concludere che $T(n) = \Theta(n^3)$.

---

### (2) $T(n) = 4T(n/3) + n$
*(Da completare)*

---

### (3) $T(n) = 4T(n/2) + n$
*(Da completare)*

---

### (4) $T(n) = 3T(n-1) + 1$
*(Da completare)*
