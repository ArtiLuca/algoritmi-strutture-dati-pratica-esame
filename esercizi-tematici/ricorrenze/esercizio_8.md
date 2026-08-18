# Esercizio 8 - Dimostrazione O(n log n)

Sia data la seguente equazione di ricorrenza:

$$ 
T(n) = T(n - 1) + \log n 
$$

Si dimostri che $T(n) = \mathcal{O}(n \log n)$.

---

### Dimostrazione con il Metodo di Sostituzione

Per dimostrare che vale $T(n) = \mathcal{O}(n \log n)$ bisogna verificare che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tale per cui valga:

$$ 
T(n) \le c n \log n \quad \forall n \ge n_0 
$$

Assumiamo come ipotesi induttiva che questo valga per scelte di $m < n$, ovvero che valga $T(m) \le c m \log m$.
Utilizzando l'ipotesi induttiva sulla nostra ricorrenza, il che è lecito perché $n - 1 < n$, otteniamo:

$$
\begin{aligned}
T(n) &= T(n-1) + \log n \\
&\le c(n-1)\log(n-1) + \log n
\end{aligned}
$$

Poiché la funzione logaritmo è strettamente crescente, sappiamo che $\log(n-1) < \log n$ per ogni $n \ge 2$. Possiamo quindi fare una maggiorazione sostituendo $\log(n-1)$ con $\log n$:

$$
\begin{aligned}
T(n) &\le c(n-1)\log n + \log n \\
&= cn\log n - c\log n + \log n \\
&= cn\log n - (c-1)\log n
\end{aligned}
$$

Vogliamo che la nostra espressione maggiorata sia minore o uguale al limite asintotico cercato:

$$ 
cn\log n - (c-1)\log n \le cn \log n 
$$

Questo implica che il termine sottrattivo debba essere non negativo:

$$ 
-(c-1)\log n \le 0 \implies (c-1)\log n \ge 0 
$$

Poiché $\log n > 0$ per ogni $n \ge 2$, affinché il prodotto sia maggiore o uguale a zero è sufficiente imporre che:

$$ 
c - 1 \ge 0 \implies c \ge 1 
$$

Scegliendo, ad esempio, $c = 1$ e $n_0 = 2$, la disuguaglianza è sempre soddisfatta.
Abbiamo così dimostrato formalmente che $T(n) = \mathcal{O}(n\log n)$.
