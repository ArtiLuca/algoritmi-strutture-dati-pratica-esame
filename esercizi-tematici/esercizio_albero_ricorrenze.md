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

Per ipotizzare una soluzione uso un albero delle ricorrenze con livelli indicati con $i=0\dots h$ dove $h$ è l’altezza dell’albero delle ricorrenze:

- $i=0$: ha un solo problema con costo locale $n$
- $i=1$: genera 4 sottoproblemi di taglia $n/2$ quindi il costo complessivo è $4\cdot\left(\frac{n}{2}\right)$
- $i=2$: genera 16 sottoproblemi di taglia $n/4$ quindi il costo complessivo è $16\cdot\left(\frac{n}{4}\right)$
- $i=3$: genera 64 sottoproblemi di taglia $n/8$ quindi il costo complessivo è $64\cdot\left(\frac{n}{8}\right)$
- $\dots$

Ad un livello generico $i$ quindi si ha che ci sono $4^i$ sottoproblemi, ciascuno di dimensione $\frac{n}{2^i}$ e quindi si ha un costo complessivo di $4^i \cdot \left(\frac{n}{2^i}\right)$ che possiamo riscrivere come $2^i \cdot n$.

Il costo dei sottoproblemi arriva al costo unitario $1$ alle foglie, ovvero al livello $h$.
Questo accade quando $i=h$ cioè quando $\frac{n}{2^h} = 1$ ovvero $2^h = n \implies h = \log_2 n$.

Quindi il costo totale è dato dalla somma dei nodi interni, cioè da $i=0\dots h-1$ e dal costo delle foglie.
Il costo dei nodi interni è dato da: 

$$ \sum_{i=0}^{h-1}n\cdot 2^i = n \cdot \sum_{i=0}^{\log_2 n - 1} 2^i $$

Ricordando la sommatoria nota (serie geometrica finita) $\sum_{i=0}^{k} q^i = \frac{q^{k+1} - 1}{q - 1}$, otteniamo dunque: 

$$ n \cdot \frac{2^{(\log_2 n - 1)+1}-1}{2-1} $$

e visto che $2^{\log_2 n} = n$ otteniamo quindi che il costo per i nodi interni equivale a $n \cdot \frac{n-1}{1} \approx n^2$.

Il costo di ciascuna foglia è costante/unitario (ad esempio indicandolo con una costante $c$ positiva).
Il numero di foglie è $a^h$ dato dalla disuguaglianza $a^{\log_b n} = 4^{\log_2 n} = n^{\log_2 4} = n^2$ e quindi il costo complessivo dell’ultimo livello è $c \cdot n^2 \approx n^2$. 

Essendo entrambi i costi $\mathcal{O}(n^2)$, ipotizzo una soluzione di $T(n) = \Theta(n^2)$.

**Dimostrazione con il metodo di sostituzione:**

Per dimostrare la ipotesi di soluzione provo separatamente limite superiore e inferiore.

**Limite Superiore $\mathcal{O}(n^2)$**  
La dimostrazione di $\mathcal{O}(n^2)$ fallisce a meno che non si sottragga un termine di ordine inferiore.
Ovvero per dimostrare che $T(n) = \mathcal{O}(n^2)$ si dimostra che $\exists c,k > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \le cn^2 - kn$.

Assumendo come ipotesi induttiva che valga per valori $m < n$, si procede come ho già fatto tante volte:

$$
\begin{aligned}
T(n) &= 4T\left(\frac{n}{2}\right) + n \\
&\le 4 \left(c\frac{n^2}{4} - k \frac{n}{2}\right) + n \\
&= cn^2 - 2kn + n \\
&= cn^2 + (1 - 2k)n
\end{aligned}
$$

Vogliamo che $cn^2 + (1 - 2k)n \le cn^2 - kn$ quindi occorre che $1 - 2k \le -k$, ovvero $1 \le k$.
Quindi con una scelta di $k=1, c=1$ si dimostra che $T(n) = \mathcal{O}(n^2)$.

**Limite Inferiore $\Omega(n^2)$**  
Per dimostrare che $T(n) = \Omega(n^2)$ basta verificare che $\exists d> 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \ge dn^2$.
Procedendo in modo analogo a prima (però senza bisogno di sottrarre un termine di ordine inferiore):

$$
\begin{aligned}
T(n) &= 4T\left(\frac{n}{2}\right) + n \\
&\ge 4\left(d\frac{n^2}{4}\right) + n \\
&= dn^2 + n
\end{aligned}
$$

Una qualsiasi scelta $d > 0$ soddisfa la disuguaglianza $dn^2 + n \ge dn^2$ con $n_0$ sufficientemente grande e quindi si conclude anche che $T(n) = \Omega(n^2)$.

**Conclusione:**  
Quindi, si può concludere che la ricorrenza iniziale ammette soluzione $T(n) = \Theta(n^2)$, come ipotizzato.

---

### (4) $T(n) = 3T(n-1) + 1$
*(Da completare)*
