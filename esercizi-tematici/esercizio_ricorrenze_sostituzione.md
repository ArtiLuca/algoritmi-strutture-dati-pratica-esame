# Esercizi Ricorrenze - Metodo di Sostituzione

Usare il metodo di sostituzione per dimostrare le ricorrenze:

- $T(n) = T(n-1) + n$ ha soluzione $\mathcal{O}(n^2)$
- $T(n) = T(n/2) + \Theta(1)$ ha soluzione $\mathcal{O}(\log n)$
- $T(n) = 2T(n/2) + n$ ha soluzione $\Theta(n \log n)$
- $T(n) = 2T(n/2 + 17) + n$ ha soluzione $\mathcal{O}(n \log n)$
- $T(n) = 2T(n/3) + \Theta(n)$ ha soluzione $\Theta(n)$
- $T(n) = 4T(n/2) + \Theta(n)$ ha soluzione $\Theta(n^2)$

---

### (1) $T(n) = T(n-1) + n$ ammette soluzione $\mathcal{O}(n^2)$

Dobbiamo dimostrare che $\exists c > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \le c n^2$ per ogni $n \ge n_0$.

Assumiamo per ipotesi induttiva che questo sia vero per $n - 1 < n$, ovvero che:

$$ T(n-1) \le c(n-1)^2 $$

Applichiamo questa ipotesi alla nostra ricorrenza:

$$
\begin{aligned}
T(n) &= T(n-1) + n \\
&\le c(n-1)^2 + n \\
&= c(n^2 - 2n + 1) + n \\
&= c n^2 - 2nc + c + n \\
&= c n^2 + (1 - 2c)n + c
\end{aligned}
$$

Vogliamo che $c n^2 + (1 - 2c)n + c \le c n^2$, ovvero:

$$ (1 - 2c)n + c \le 0 $$

Basta imporre che il coefficiente di $n$ sia non positivo, ovvero $1 - 2c \le 0 \implies c \ge \frac{1}{2}$.

Scegliendo $c = 1$, otteniamo:

$$ (1 - 2)n + 1 = -n + 1 \le 0 $$

Questa disuguaglianza è verificata per $n \ge 1$. 

Quindi possiamo concludere che, con $c = 1$ e $n_0 = 1$, vale $T(n) = \mathcal{O}(n^2)$ per ogni $n \ge n_0$.

---

### (2) $T(n) = T(n/2) + \Theta(1)$ ammette soluzione $\mathcal{O}(\log n)$

Per dimostrare che la ricorrenza ammette soluzione $\mathcal{O}(\log n)$, dobbiamo dimostrare che $\exists c > 0, \exists n_0 \in \mathbb{N}$ per cui vale $T(n) \le c \log_2 n$.

Per assorbire il costo asintotico di $\Theta(1)$, usiamo una costante $d > 0$ e riscriviamo la ricorrenza come $T(n) \le T(n/2) + d$.

Assumiamo per ipotesi induttiva che valga per $n/2 < n$, ovvero $T(n/2) \le c \log_2(n/2)$.

Applicando l'ipotesi nella ricorrenza:

$$
\begin{aligned}
T(n) &\le T(n/2) + d \\
&\le c \log_2\left(\frac{n}{2}\right) + d \\
&= c(\log_2 n - \log_2 2) + d \\
&= c \log_2 n - c + d
\end{aligned}
$$

Vogliamo che $c \log_2 n - c + d \le c \log_2 n$, il che si semplifica in:

$$ -c + d \le 0 \implies c \ge d $$

Scegliendo, ad esempio, $d = 1$ e $c = 2$, con $n_0 = 2$ (per avere logaritmi ben definiti e positivi), la disuguaglianza è soddisfatta.

Dimostriamo così che $T(n) = \mathcal{O}(\log n)$.

---

### (3) $T(n) = 2T(n/2) + n$ ammette soluzione $\Theta(n \log n)$

Per dimostrare che la ricorrenza ammette soluzione $\Theta(n \log n)$, dimostriamo separatamente i limiti superiore ($\mathcal{O}$) e inferiore ($\Omega$).

**Limite Superiore: $T(n) = \mathcal{O}(n \log n)$**

Dobbiamo verificare che $\exists c > 0, \exists n_0 \in \mathbb{N}$ per cui vale $T(n) \le c n \log_2 n$.

Assumiamo per ipotesi induttiva che valga per $m = n/2 < n$, ovvero $T(m) \le c m \log_2 m$.

Applicando l'ipotesi alla ricorrenza otteniamo:

$$
\begin{aligned}
T(n) &\le 2c\left(\frac{n}{2} \log_2\frac{n}{2}\right) + n \\
&= c n(\log_2 n - \log_2 2) + n \\
&= c n(\log_2 n - 1) + n \\
&= c n \log_2 n - cn + n \\
&= c n \log_2 n + (1 - c)n
\end{aligned}
$$

Vogliamo che $c n \log_2 n + (1 - c)n \le c n \log_2 n$. Basta imporre che $(1 - c)n \le 0$, ovvero $1 - c \le 0 \implies c \ge 1$.

Scegliendo $c = 2$, abbiamo la disuguaglianza $2n \log_2 n - n \le 2n \log_2 n$, che è vera per qualsiasi scelta di $n_0 \ge 2$. Dunque $T(n) = \mathcal{O}(n \log n)$.

**Limite Inferiore: $T(n) = \Omega(n \log n)$**

Dobbiamo verificare che $\exists d > 0, \exists n_0 \in \mathbb{N}$ per cui vale $T(n) \ge d n \log_2 n$.

Assumiamo per ipotesi induttiva che $T(n/2) \ge d(n/2) \log_2(n/2)$. Procedendo in modo analogo:

$$
\begin{aligned}
T(n) &\ge 2d\left(\frac{n}{2} \log_2\frac{n}{2}\right) + n \\
&= d n(\log_2 n - 1) + n \\
&= d n \log_2 n - dn + n \\
&= d n \log_2 n - (d - 1)n
\end{aligned}
$$

Vogliamo che $d n \log_2 n - (d - 1)n \ge d n \log_2 n$. Imponiamo che $d - 1 \le 0 \implies d \le 1$.

Scegliendo $d = 1$, la disuguaglianza diventa $n \log_2 n \ge n \log_2 n$, che è sempre vera per $n > 0$. 

Dunque una scelta di $d = 1$ e $n_0 = 2$ è sufficiente per concludere che $T(n) = \Omega(n \log n)$.

Avendo dimostrato sia il limite superiore che inferiore, possiamo concludere che $T(n) = \Theta(n \log n)$.

---

### (4) $T(n) = 2T(n/2 + 17) + n$ ammette soluzione $\mathcal{O}(n \log n)$

Qui c'è il termine $+17$ che "romperebbe" la dimostrazione del limite superiore. Ovvero non funziona dimostrare che $T(n) \le cn \log_2 n$ per una costante $c > 0$.
Quindi, possiamo provare a dimostrare il limite superiore "spostando" la variabile $n$ di una costante $\alpha > 0$.

Ovvero, proviamo a dimostrare che $T(n) = \mathcal{O}(n\log n)$ se $\exists c,\alpha > 0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \le c(n-\alpha)\log_2(n-\alpha)$. In particolare, per la scelta del valore per la costante $\alpha$, vogliamo una scelta tale che quando andiamo a sostituire $\frac{n}{2} + 17$ nella ricorrenza, il valore sia esattamente la metà di $(n - \alpha)$. 
Ovvero vogliamo che:

$$ \frac{n}{2} + 17 - \alpha = \frac{n - \alpha}{2} = \frac{n}{2} - \frac{\alpha}{2} $$

Quindi se vogliamo $\frac{n}{2} + 17 - \alpha = \frac{n}{2} - \frac{\alpha}{2}$, ovvero $17 - \alpha = -\frac{\alpha}{2}$ segue:

$$ 17 = \alpha - \frac{\alpha}{2} \implies \alpha = 34 $$

Quindi per dimostrare che $T(n) = \mathcal{O}(n\log n)$ dimostriamo che $\exists c>0, \exists n_0 \in \mathbb{N}$ tali che $T(n) \le c(n-34)\log_2(n-34)$ dove usiamo $\alpha = 34$ come la costante per lo "shift" della variabile $n$.

**Ipotesi induttiva:**
Assumo che valga per valori $m < n$, ovvero che valga $T(m) \le c(m-34)\log_2(m-34)$.

**Passo induttivo:**
Applico l'ipotesi induttiva alla ricorrenza:

$$
\begin{aligned}
T(n) &= 2T\left(\frac{n}{2}+17\right) + n \\
&\le 2\left[c\left(\frac{n}{2}+17-34\right)\log_2\left(\frac{n}{2}+17-34\right)\right] + n \\
&= 2\left[c\left(\frac{n}{2}-17\right)\log_2\left(\frac{n}{2}-17\right)\right] + n
\end{aligned}
$$

Possiamo semplificare raccogliendo il $2$ al denominatore: 

$$ 2\left[c\left(\frac{n-34}{2}\right)\log_2\left(\frac{n-34}{2}\right)\right] + n $$

Poi il $2$ all'esterno si può semplificare con il fratto due e possiamo anche sfruttare la regola del quoziente dei logaritmi. Quindi otteniamo: 

$$
\begin{aligned}
c(n-34)[\log_2(n-34) - \log_2 2] + n &= c(n-34)[\log_2(n-34) - 1] + n \\
&= c(n-34)\log_2(n-34) - c(n-34) + n
\end{aligned}
$$

Ora serve che $c(n-34)\log_2(n-34) - c(n-34) + n \le c(n-34)\log_2(n-34)$.
Quindi occorre che il valore $-c(n-34) + n$ sia minore o uguale a 0.
Ovvero serve $-c(n-34) + n \le 0$, cioè:

$$ -cn + 34c + n \le 0 \implies (1-c)n + 34c \le 0 $$

Quindi occorre che $1-c < 0 \implies c > 1$.
Ad esempio, con $c=2$ otteniamo dalla disuguaglianza precedente: 

$$ -n + 68 \le 0 \implies n \ge 68 $$

**Conclusione:**
Quindi una scelta di $c=2$ e $n_0=68$ va bene e quindi abbiamo dimostrato che vale $T(n) = \mathcal{O}(n\log n)$ per ogni $n \ge n_0$.
In particolare, questo funziona perché spostiamo ("shift") la variabile $n$ di una costante $\alpha$ (in questo caso $34$) per compensare per il valore $+17$ dentro la ricorrenza.

---

### (5) $T(n) = 2T(n/3) + \Theta(n)$ ammette soluzione $\Theta(n)$

Per dimostrare che vale $T(n) = \Theta(n)$ devo provare separatamente che valgono sia $T(n) = \mathcal{O}(n)$ che $T(n) = \Omega(n)$.

**Limite Superiore: $T(n) = \mathcal{O}(n)$**  

Vale $T(n) = \mathcal{O}(n)$ se $\exists c>0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \le c \cdot n$ per ogni $n \ge n_0$.
Per assorbire il costo di $\Theta(n)$ usiamo una costante $k$ positiva e riscriviamo la ricorrenza come: 

$$ T(n) \le 2T\left(\frac{n}{3}\right) + kn $$

Assumo come ipotesi induttiva che vale per valori $m < n$, ovvero $T(m) \le cm$.
Applicando la nostra ipotesi induttiva alla ricorrenza (va bene perché $\frac{n}{3} < n$) abbiamo:

$$
\begin{aligned}
T(n) &\le 2c\left(\frac{n}{3}\right) + kn \\
&= \frac{2}{3}nc + kn \\
&= \left(\frac{2}{3}c + k\right)n
\end{aligned}
$$

Vogliamo che $\left(\frac{2}{3}c+k\right)n \le cn$ quindi dividendo per $n$ (assumendo $n > 0$) otteniamo la disuguaglianza:

$$ \frac{2}{3}c + k \le c \implies k \le \frac{1}{3}c \implies c \ge 3k $$

Quindi scegliendo opportune costanti $c \ge 3k$ e $n_0$ sufficientemente grande si dimostra che vale $T(n) = \mathcal{O}(n)$.

**Limite Inferiore: $T(n) = \Omega(n)$**  

Vale $T(n) = \Omega(n)$ se $\exists d>0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \ge d \cdot n$ per ogni $n \ge n_0$.
Per assorbire il costo di $\Theta(n)$ usiamo una costante $h$ positiva e riscriviamo la ricorrenza come:

$$ T(n) \ge 2T\left(\frac{n}{3}\right) + hn $$

Assumo come ipotesi induttiva che vale per valori $m < n$, ovvero $T(m) \ge dm$.
Applicando la nostra ipotesi induttiva alla ricorrenza (va bene perché $\frac{n}{3} < n$) abbiamo:

$$
\begin{aligned}
T(n) &\ge 2d\left(\frac{n}{3}\right) + hn \\
&= \frac{2}{3}dn + hn \\
&= \left(\frac{2}{3}d + h\right)n
\end{aligned}
$$

Vogliamo che $\left(\frac{2}{3}d + h\right)n \ge dn$ e quindi dividendo per $n$ (assumendo $n > 0$) otteniamo la disuguaglianza:

$$ \frac{2}{3}d + h \ge d \implies d \le 3h $$

Quindi scegliendo opportune costanti $d \le 3h$ e $n_0$ sufficientemente grande si dimostra che vale $T(n) = \Omega(n)$.

**Conclusione:**
Avendo dimostrato sia il limite superiore che inferiore, possiamo concludere che $T(n) = \Theta(n)$.

---

### (6) $T(n) = 4T(n/2) + \Theta(n)$ ammette soluzione $\Theta(n^2)$
*(Da completare)*
