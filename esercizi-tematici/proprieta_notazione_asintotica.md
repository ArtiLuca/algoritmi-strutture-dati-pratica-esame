# Dimostrare le seguenti uguaglianze:

1. $f(n)=O(g(n))$ sse $g(n)=\Omega(f(n))$
2. $\Theta(g(n))=O(g(n))\cap\Omega(g(n))$
3. $f(n)=\Theta(f(n))$
4. $f(n)=\Theta(g(n))$ sse $\Theta(f(n))=\Theta(g(n))$ sse $g(n)=\Theta(f(n))$
5. $f(n)=O(g(n))$ e $g(n)=O(h(n))$ implica $f(n)=O(h(n))$

Ricordo le definizioni delle tre classi $\mathcal{O}, \Omega, \Theta$ per due funzioni arbitrarie $f(n), g(n) > 0$:

$$ \mathcal{O}(g(n)) = \{f(n) \mid \exists c > 0, \exists n_0 \in \mathbb{N}, \forall n\ge n_0 : 0 \le f(n) \le c \cdot g(n)\} $$

$$ \Omega(g(n)) = \{f(n) \mid \exists d > 0, \exists n_0 \in \mathbb{N}, \forall n\ge n_0 : 0 \le d \cdot g(n) \le f(n)\} $$

$$ \Theta(g(n)) = \{f(n) \mid \exists c,d > 0, \exists n_0 \in \mathbb{N}, \forall n\ge n_0 : 0 \le c \cdot g(n) \le f(n) \le d \cdot g(n) \} $$

---

### (1) $f(n)=O(g(n))$ sse $g(n)=\Omega(f(n))$

Si tratta di una bi-implicazione, quindi dobbiamo dimostrare entrambi i versi.

**Verso 1:** $f(n) = \mathcal{O}(g(n)) \implies g(n) = \Omega(f(n))$
**Ipotesi:** $f(n) = \mathcal{O}(g(n))$, ovvero $\exists c>0, \exists n_0 \in \mathbb{N}$ tale che $0 \le f(n) \le c \cdot g(n)$ per $\forall n\ge n_0$.
**Tesi:** $g(n) = \Omega(f(n))$

Se prendiamo la nostra ipotesi e dividiamo entrambi i lati della disuguaglianza per $c$ (va bene perché $c > 0$) otteniamo quindi:
$$0 \le \frac{1}{c} \cdot f(n) \le g(n)$$
Ricordando la definizione della classe $\Omega$ e utilizzando come costante moltiplicativa $d = \frac{1}{c}$ otteniamo $0 \le d \cdot f(n) \le g(n)$ che è la nostra tesi.

**Verso 2:** $g(n) = \Omega(f(n)) \implies f(n) = \mathcal{O}(g(n))$
**Ipotesi:** $g(n) = \Omega(f(n))$, ovvero $\exists d>0, \exists n_0 \in \mathbb{N}$ tale che $0 \le d \cdot f(n) \le g(n)$ per $\forall n\ge n_0$.
**Tesi:** $f(n) = \mathcal{O}(g(n))$

Dividendo l'ipotesi per $d$ (poiché $d > 0$), otteniamo:
$$0 \le f(n) \le \frac{1}{d} \cdot g(n)$$
Usando come costante moltiplicativa $c = \frac{1}{d}$, ritroviamo $0 \le f(n) \le c \cdot g(n)$, completando la dimostrazione (C.V.D).

---

### (2) $\Theta(g(n))=O(g(n))\cap\Omega(g(n))$

Per dimostrare che vale questa disuguaglianza possiamo notare che si tratta di due inclusioni:
1. $\Theta(g(n)) \subseteq \mathcal{O}(g(n)) \cap \Omega(g(n))$
2. $\mathcal{O}(g(n)) \cap \Omega(g(n)) \subseteq \Theta(g(n))$

Dimostriamo le due inclusioni separatamente:

Per dimostrare la **prima inclusione**, sia $f(n) = \Theta(g(n))$ allora abbiamo per definizione della classe $\Theta$ che $\exists c,d > 0, \exists n_0 \in \mathbb{N}$ tali che $0 \le c \cdot g(n) \le f(n) \le d \cdot g(n)$.
Per la definizione di $\mathcal{O}$ abbiamo che vale $f(n) = \mathcal{O}(g(n))$, utilizzando $d$ come costante moltiplicativa.
In modo analogo, per la definizione di $\Omega$ abbiamo che vale $f(n) = \Omega(g(n))$, usando $c$ come costante moltiplicativa. Pertanto segue che $f(n) \in \mathcal{O}(g(n)) \cap \Omega(g(n))$.

Per dimostrare la **seconda inclusione**, sia $f(n) \in \mathcal{O}(g(n)) \cap \Omega(g(n))$ allora:
Dato che $f(n) = \mathcal{O}(g(n))$ segue che $\exists c_1 > 0, \exists n_1 \in \mathbb{N}$ tale che $f(n) \le c_1 \cdot g(n)$ per $n \ge n_1$.
Dato che $f(n) = \Omega(g(n))$ segue che $\exists d_1 > 0, \exists n_2 \in \mathbb{N}$ tale che $d_1 \cdot g(n) \le f(n)$ per $n \ge n_2$.

Quindi, scegliendo $n_0 = \max(n_1,n_2)$ abbiamo:
$$0 \le d_1 \cdot g(n) \le f(n) \le c_1 \cdot g(n)$$

Ricordando la definizione della classe $\Theta$ e utilizzando $c=d_1$ e $d=c_1$ come costanti moltiplicative segue pertanto che $f(n) = \Theta(g(n))$.
Avendo mostrato che valgono entrambe le inclusioni abbiamo finito la dimostrazione.

---

### (3) $f(n) = \Theta(f(n))$

Segue direttamente dalla definizione della classe $\Theta$ utilizzando $c=d=1$ come costanti moltiplicative.

---

### (4) $f(n)=\Theta(g(n))$ sse $\Theta(f(n))=\Theta(g(n))$ sse $g(n)=\Theta(f(n))$

Questo è bello lungo quindi lo lascio per dopo, però l’idea sarebbe di usare i punti (1) e (2) precedenti per dimostrare la bi-implicazione $f(n)=\Theta(g(n)) \iff \Theta(f(n))=\Theta(g(n))$ e poi resta solo da dimostrare la bi-implicazione $f(n)=\Theta(g(n)) \iff g(n)=\Theta(f(n))$.
Essendo a corto di tempo (priorità ad altri concetti per esame) lo lascio per magari un’altra volta.

---

### (5) $f(n)=O(g(n))$ e $g(n)=O(h(n))$ implica $f(n)=O(h(n))$

Abbiamo le seguenti ipotesi e tesi:

**Ipotesi 1:** $f(n)=O(g(n))$, che per definizione di $\mathcal{O}$ vuol dire che $\exists c_1>0, \exists n_1 \in \mathbb{N}$ tale che $f(n) \le c_1 \cdot g(n)$ per ogni $n \ge n_1$.
**Ipotesi 2:** $g(n)=O(h(n))$, che in modo analogo alla prima ipotesi vuol dire che $\exists c_2 > 0, \exists n_2 \in \mathbb{N}$ tale che $g(n) \le c_2 \cdot h(n)$ per ogni $n \ge n_2$.
**Tesi:** $f(n)=O(h(n))$, che vuol dire dimostrare che $\exists c >0, \exists n_0 \in \mathbb{N}$ tale che $f(n) \le c \cdot h(n)$ per ogni $n \ge n_0$.

Se applichiamo la ipotesi 1 alla ipotesi 2 otteniamo:
$$f(n) \le c_1 \cdot (c_2 \cdot h(n))$$

Possiamo riscrivere questo in modo più compatto:
$$f(n) \le (c_1 \cdot c_2) \cdot h(n)$$

Scegliendo $n_0 = \max(n_1,n_2)$ e usando come costante moltiplicativa $c = c_1 \cdot c_2$, segue $f(n) \le c \cdot h(n)$ che è la nostra tesi (C.V.D).
