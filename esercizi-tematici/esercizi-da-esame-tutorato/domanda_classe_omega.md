# Domanda A — Dimostrazione Formale con Notazione Asintotica

Definire formalmente la classe $\mathcal{O}(g(n))$.
Dimostrare oppure confutare le seguenti affermazioni.

- **(i)** Se $f(n) = \mathcal{O}(g(n))$ e $h(n) = \mathcal{O}(g(n))$, allora $f(n) + h(n) = \mathcal{O}(g(n))$.
- **(ii)** Se $f(n) = \mathcal{O}(g(n))$, allora $2^{f(n)} = \mathcal{O}(2^{g(n)})$.

Per ciascuna affermazione, fornire una dimostrazione usando la definizione formale oppure un controesempio.

---

### i. Definizione Formale di $\mathcal{O}(g(n))$

Siano $g(n)$ e $k(n)$ due funzioni asintoticamente positive, possiamo definire la classe:

$$
\mathcal{O}(g(n)) = \{k(n) \mid \exists c > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0 : 0 \le k(n) \le c \cdot g(n)\}
$$

---

### ii. Dimostrazione punto (i)

**Tesi:** Se $f(n) = \mathcal{O}(g(n))$ e $h(n) = \mathcal{O}(g(n))$, allora $f(n) + h(n) = \mathcal{O}(g(n))$.

Vogliamo dimostrare che $f(n) + h(n) = \mathcal{O}(g(n))$, ovvero che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tale che, $\forall n \ge n_0$, valga:

$$
f(n) + h(n) \le c \cdot g(n)
$$

Per definizione, dalle due ipotesi ricaviamo che:
1. Poiché $f(n) = \mathcal{O}(g(n))$, segue che $\exists c_1 > 0, \exists n_1 \in \mathbb{N}$ tali che, $\forall n \ge n_1$, vale $f(n) \le c_1 \cdot g(n)$.
2. Poiché $h(n) = \mathcal{O}(g(n))$, segue che $\exists c_2 > 0, \exists n_2 \in \mathbb{N}$ tali che, $\forall n \ge n_2$, vale $h(n) \le c_2 \cdot g(n)$.

Scegliendo $n_0 = \max(n_1, n_2)$, siamo certi che per ogni $n \ge n_0$ valgono entrambe le disuguaglianze. Possiamo quindi sommarle membro a membro:

$$
f(n) + h(n) \le c_1 \cdot g(n) + c_2 \cdot g(n) = (c_1 + c_2) \cdot g(n)
$$

Impostando una nuova costante $c = c_1 + c_2$ (che è strettamente positiva essendo somma di costanti positive), otteniamo esattamente $f(n) + h(n) \le c \cdot g(n)$. L'affermazione è quindi **vera**.

---

### iii. Controesempio punto (ii)

**Tesi:** Se $f(n) = \mathcal{O}(g(n))$, allora $2^{f(n)} = \mathcal{O}(2^{g(n)})$.

Questa affermazione è **falsa**. Possiamo confutarla fornendo un controesempio.
Scegliamo le funzioni:
- $f(n) = 2n$
- $g(n) = n$

L'ipotesi di partenza è chiaramente rispettata: $2n = \mathcal{O}(n)$ (basta scegliere una costante $c \ge 2$).
Sostituiamo ora queste funzioni agli esponenti come richiesto dalla tesi:
- $2^{f(n)} = 2^{2n} = 4^n$
- $2^{g(n)} = 2^n$

Se la tesi fosse vera, dovrebbe valere che $4^n = \mathcal{O}(2^n)$. Per definizione, dovrebbe esistere una costante $c > 0$ e un $n_0 \in \mathbb{N}$ tali che, per ogni $n \ge n_0$:

$$
4^n \le c \cdot 2^n
$$

Dividendo entrambi i membri per $2^n$ (lecito per $n > 0$), otteniamo:

$$
2^n \le c
$$

Questa disuguaglianza genera un'evidente contraddizione: richiede che una funzione esponenziale strettamente crescente ($2^n$) sia limitata superiormente da una costante fissa $c$. Al tendere di $n \to +\infty$, il termine $2^n$ supererà inevitabilmente qualsiasi costante prefissata.
Non potendo soddisfare la condizione $\forall n \ge n_0$, concludiamo che la seconda affermazione è falsa.
