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

Assumiamo, come usuale per una ricorrenza di questo tipo, che il caso base sia positivo, ad esempio $T(1)=1$.

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

Vogliamo che:

$$
(c^2 \cdot 2^n)(n-1) \ge c \cdot 2^n
$$

Dividendo per $c \cdot 2^n$ otteniamo:

$$
c(n-1) \ge 1
$$

Quindi, scegliendo ad esempio $c=\frac14$, la disuguaglianza del passo induttivo è verificata per ogni $n \ge 5$.

Resta da verificare i casi iniziali. Assumendo $T(1)=1$, otteniamo:

$$
T(1)=1 \ge \frac14 2^1
$$

$$
T(2)=T(1)T(1)=1 \ge \frac14 2^2
$$

$$
T(3)=T(1)T(2)+T(2)T(1)=2 \ge \frac14 2^3
$$

$$
T(4)=T(1)T(3)+T(2)T(2)+T(3)T(1)=5 \ge \frac14 2^4
$$

Per induzione segue quindi che, per ogni $n$ sufficientemente grande,

$$
T(n) \ge \frac14 2^n
$$

Abbiamo dunque dimostrato che:

$$
T(n)=\Omega(2^n)
$$
