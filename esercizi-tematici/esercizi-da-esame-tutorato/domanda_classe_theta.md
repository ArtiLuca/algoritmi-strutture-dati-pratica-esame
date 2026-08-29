## Domanda A (8 punti)

Definire formalmente la classe $\Theta(g(n))$. Dimostrare le seguenti affermazioni o fornire un controesempio:

- (i) se $f(n), f'(n) \in \Theta(g(n))$ allora $f(n) + f'(n) \in \Theta(g(n))$
- (ii) se $f(n), f'(n) \in \Theta(g(n))$ allora $f(n) \cdot f'(n) \in \Theta(g(n))$

---

### i. Definizione di $\Theta(g(n))$

Siano $h(n)$ e $g(n)$ due funzioni arbitrarie asintoticamente positive; possiamo definire la classe:

$$
\Theta(g(n)) = \{h(n) \mid \exists c, d > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0 : 0 \le d \cdot g(n) \le h(n) \le c \cdot g(n)\}
$$

---

### ii. Dimostrazione punto (i)

**Tesi:** $f(n) \in \Theta(g(n))$ e $f'(n) \in \Theta(g(n)) \implies f(n) + f'(n) \in \Theta(g(n))$

Dalla prima ipotesi segue, per definizione della classe $\Theta$, che $\exists c_1, d_1 > 0, \exists n_1 \in \mathbb{N}$ tali che:

$$
d_1 \cdot g(n) \le f(n) \le c_1 \cdot g(n) \quad \text{per ogni } n \ge n_1
$$

In modo analogo, per la seconda ipotesi, $\exists c_2, d_2 > 0, \exists n_2 \in \mathbb{N}$ tali che:

$$
d_2 \cdot g(n) \le f'(n) \le c_2 \cdot g(n) \quad \text{per ogni } n \ge n_2
$$

Per dimostrare che $f(n) + f'(n) \in \Theta(g(n))$, occorre dimostrare che $\exists c, d > 0, \exists n_0 \in \mathbb{N}$ tali che:

$$
d \cdot g(n) \le f(n) + f'(n) \le c \cdot g(n) \quad \text{per ogni } n \ge n_0
$$

Scegliendo $n_0 = \max(n_1, n_2)$ possiamo sommare le due catene di disuguaglianze:

$$
(d_1 + d_2) \cdot g(n) \le f(n) + f'(n) \le (c_1 + c_2) \cdot g(n)
$$

Impostando le nuove costanti $d = d_1 + d_2$ e $c = c_1 + c_2$ (che sono strettamente positive in quanto somme di costanti positive), otteniamo esattamente la definizione della classe $\Theta$. L'affermazione (i) è dunque **vera**.

---

### iii. Controesempio punto (ii)

**Tesi:** $f(n) \in \Theta(g(n))$ e $f'(n) \in \Theta(g(n)) \implies f(n) \cdot f'(n) \in \Theta(g(n))$

Questa affermazione **non è in generale vera**, e possiamo dimostrarlo con un controesempio.
Siano $f(n) = n$, $f'(n) = n$ e $g(n) = n$.

È evidente che valga $f(n) \in \Theta(g(n))$ e anche $f'(n) \in \Theta(g(n))$.
Moltiplicando le due funzioni, otteniamo $f(n) \cdot f'(n) = n \cdot n = n^2$.

Se la tesi fosse vera, dovrebbe valere che $n^2 \in \Theta(n)$.
Per definizione della classe $\Theta$, dovrebbero esistere delle costanti $c, d > 0$ e un $n_0 \in \mathbb{N}$ tali che:

$$
d \cdot n \le n^2 \le c \cdot n \quad \text{per ogni } n \ge n_0
$$

Analizziamo il limite superiore:

$$
n^2 \le c \cdot n
$$

Dividendo per $n$ (lecito per $n > 0$), otteniamo:

$$
n \le c
$$

Questa disuguaglianza impone che $n$ sia limitato superiormente da una costante $c$. Questo genera una contraddizione, poiché per $n \to +\infty$ il termine $n$ supererà inevitabilmente qualsiasi costante prefissata $c$. Non potendo soddisfare la disuguaglianza $\forall n \ge n_0$, concludiamo che la seconda affermazione è **falsa**.
