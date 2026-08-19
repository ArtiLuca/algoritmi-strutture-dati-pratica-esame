# Esercizio 17 - Definizione e Transitività di Omega

**Domanda 17**
Dare la definizione di $\Omega(f(n))$. Mostrare che se $f(n) = \Omega(g(n))$ e $g(n) = \Omega(h(n))$ allora $f(n) = \Omega(h(n))$.

---

### i. Definizione di $\Omega(f(n))$

Date due funzioni arbitrarie asintoticamente positive $f(n)$ e $g(n)$, la definizione formale della classe $\Omega(f(n))$ è la seguente:

$$ 
\Omega(f(n)) = \{g(n) \mid \exists c > 0, \exists n_0 \in \mathbb{N} \text{ t.c. } \forall n \ge n_0 : 0 \le c \cdot f(n) \le g(n) \} 
$$

*(Nota: questo definisce l'insieme delle funzioni $g(n)$ limitate inferiormente da $f(n)$. Specularmente, scrivere $f(n) = \Omega(g(n))$ significa che $\exists c > 0, \exists n_0 \text{ t.c. } f(n) \ge c \cdot g(n) \ge 0$).*

---

### ii. Dimostrazione della Transitività

Vogliamo dimostrare che:

$$ 
f(n) = \Omega(g(n)) \text{ e } g(n) = \Omega(h(n)) \implies f(n) = \Omega(h(n)) 
$$

Dalla prima ipotesi $f(n) = \Omega(g(n))$, per la definizione della classe $\Omega$, sappiamo che $\exists c_1 > 0, \exists n_1$ tali che valga:

$$ 
f(n) \ge c_1 \cdot g(n) \quad \text{per ogni } n \ge n_1 
$$

Dalla seconda ipotesi $g(n) = \Omega(h(n))$, sempre per definizione, sappiamo che $\exists c_2 > 0, \exists n_2$ tali che valga:

$$ 
g(n) \ge c_2 \cdot h(n) \quad \text{per ogni } n \ge n_2 
$$

La nostra tesi è che $f(n) = \Omega(h(n))$, ovvero vogliamo dimostrare che $\exists c > 0, \exists n_0$ tali che:

$$ 
f(n) \ge c \cdot h(n) \quad \text{per ogni } n \ge n_0 
$$

Scegliamo un $n_0$ sufficientemente grande in modo che valgano contemporaneamente entrambe le ipotesi. Il valore corretto è:

$$ 
n_0 = \max(n_1, n_2) 
$$

Per ogni $n \ge n_0$, possiamo applicare la seconda disuguaglianza all'interno della prima, ottenendo:

$$
\begin{aligned}
f(n) &\ge c_1 \cdot g(n) \\
&\ge c_1 \cdot (c_2 \cdot h(n)) \\
&= (c_1 \cdot c_2) \cdot h(n)
\end{aligned}
$$

Definendo una nuova costante positiva $c = c_1 \cdot c_2$ (il che è lecito poiché il prodotto di due costanti positive è a sua volta una costante positiva), otteniamo esattamente:

$$ 
f(n) \ge c \cdot h(n) 
$$

Che è proprio la nostra tesi. Abbiamo così dimostrato che $f(n) = \Omega(h(n))$ utilizzando $c = c_1 \cdot c_2$ e $n_0 = \max(n_1, n_2)$.
