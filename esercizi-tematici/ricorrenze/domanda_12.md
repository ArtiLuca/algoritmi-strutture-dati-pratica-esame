### **Domanda 12**

Dare la definizione di $\Omega(f(n))$. Dimostrare che la ricorrenza che segue ha soluzione $T(n) = \Omega(2^n)$

$$
T(n) = \sum_{k=1}^{n-1} T(k) T(n - k)
$$

---

Per la prima parte, ricordiamo che date due funzioni arbitrarie asintoticamente positive $f(n), g(n) > 0$ possiamo definire la classe $\Omega$ come segue:

$$
\Omega(f(n)) = \{g(n) \mid \exists c > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0: 0 \le c \cdot f(n) \le g(n) \}
$$

Quindi, data la ricorrenza sopra, dimostrare che vale $T(n) = \Omega(2^n)$ vuol dire dimostrare che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \ge c \cdot 2^n$.

Assumiamo come ipotesi induttiva che questo sia vero per valori $k < n$, ovvero che valga $T(k) \ge c \cdot 2^k$ con $1 \le k \le n-1$. Applichiamo questa ipotesi alla nostra ricorrenza:

$$
T(n) = \sum_{k=1}^{n-1} T(k)T(n-k) \ge \sum_{k=1}^{n-1} (c \cdot 2^k) \cdot (c \cdot 2^{n-k})
$$

Sviluppando il prodotto abbiamo per le proprietà degli esponenziali che $2^k \cdot 2^{n-k} = 2^{k+n-k} = 2^n$.
Quindi abbiamo:

$$
\sum_{k=1}^{n-1} (c \cdot 2^k) \cdot (c \cdot 2^{n-k}) = \sum_{k=1}^{n-1} (c^2 \cdot 2^n)
$$

Possiamo portare fuori dalla sommatoria il termine $(c^2 \cdot 2^n)$ essendo che non dipende dall’indice $k$ e possiamo vedere inoltre che stiamo semplicemente sommando $1$ un totale di $n-1$ volte. Quindi abbiamo:

$$
\sum_{k=1}^{n-1} (c^2 \cdot 2^n) = (c^2 \cdot 2^n) \sum_{k=1}^{n-1} 1 = (c^2 \cdot 2^n) \cdot (n-1)
$$

Vogliamo che $(c^2 \cdot 2^n)(n-1) \ge c \cdot 2^n$ e quindi dividendo per $c \cdot 2^n$ (lecito perché $n > 0$) abbiamo la seguente disuguaglianza:

$$
c(n-1) \ge 1 \implies c \ge \frac{1}{n-1}
$$

Affinché sia definita la sommatoria, serve che $n-1 \ge k \ge 1$ che quindi impone $n \ge 2$.

Con una scelta di $c=1$ si soddisfa la disuguaglianza sopra per qualsiasi valore $n_0 \ge 2$, ad esempio $n_0=2$.
Con questa scelta abbiamo quindi dimostrato che vale $T(n) = \Omega(2^n)$.
