# Domanda 15

Data la ricorrenza $T(n) = T(n/2) + T(n/3) + \sqrt{n} + 2$, dimostrare che ha soluzione $T(n) = \mathcal{O}(n)$.
Il limite è stretto, ovvero vale anche $T(n) = \Omega(n)$?

---

### i. Dimostrazione del limite superiore $\mathcal{O}(n)$

Per la prima richiesta sulla dimostrazione del limite superiore, abbiamo che $T(n) = \mathcal{O}(n)$ se $\exists c > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \le cn$.
Assumendo come ipotesi induttiva che questo valga per valori $m < n$, ovvero che valga $T(m) \le cm$, applichiamo l'ipotesi alla nostra ricorrenza, il che è lecito essendo che $\frac{n}{2}, \frac{n}{3} < n$:

$$
T(n) = T\left(\frac{n}{2}\right) + T\left(\frac{n}{3}\right) + \sqrt{n} + 2 \le c\left(\frac{n}{2}\right) + c\left(\frac{n}{3}\right) + \sqrt{n} + 2 = \frac{5}{6}cn + \sqrt{n} + 2
$$

Assumendo che $n > 0$ vale $\sqrt{n} \le n$ e quindi possiamo effettuare una maggiorazione:

$$
\frac{5}{6}cn + \sqrt{n} + 2 \le \frac{5}{6}cn + n + 2 = \left(\frac{5}{6}c + 1\right)n + 2
$$

Vogliamo che $\left(\frac{5}{6}c + 1\right)n + 2 \le cn$ e quindi dividendo per $n$ (lecito avendo assunto $n > 0$) otteniamo la disuguaglianza:

$$
\frac{5}{6}c + 1 + \frac{2}{n} \le c \implies 1 + \frac{2}{n} \le \frac{1}{6}c \implies c \ge 6 + \frac{12}{n}
$$

Quest'ultima disuguaglianza ad esempio è soddisfatta per $c \ge 7$ e $n \ge 12$.
Quindi una scelta di $c = 7$ e $n_0 = 12$ sono sufficienti per concludere la dimostrazione del limite superiore e quindi posso concludere che vale $T(n) = \mathcal{O}(n)$ per ogni $n \ge n_0$.

---

### ii. Analisi del limite inferiore $\Omega(n)$

Per la seconda richiesta, provo a dimostrare un limite inferiore, ovvero che $T(n) = \Omega(n)$.
Quindi, verifico che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tale che $T(n) \ge dn$ e procedo per induzione forte.

$$
T(n) = T\left(\frac{n}{2}\right) + T\left(\frac{n}{3}\right) + \sqrt{n} + 2 \ge d\left(\frac{n}{2}\right) + d\left(\frac{n}{3}\right) + \sqrt{n} + 2 = \frac{5}{6}dn + \sqrt{n} + 2
$$

Vogliamo dimostrare che $\frac{5}{6}dn + \sqrt{n} + 2 \ge dn$, ovvero $2 + \sqrt{n} \ge \frac{1}{6}dn$, e quindi dividendo per $\frac{1}{6}n$ (assumendo che $n > 0$) arriviamo alla seguente disuguaglianza:

$$
6 \cdot \left(\frac{\sqrt{n} + 2}{n}\right) \ge d
$$

Però per $n \to \infty$ abbiamo che $\lim_{n\to \infty} \frac{\sqrt{n}+2}{n} = 0$ e quindi $6 \cdot 0 \ge d \implies d \le 0$, che non può essere vero in quanto per definizione della classe $\Omega$ serve che la costante sia $d > 0$.
Quindi la dimostrazione per il limite inferiore con il metodo di sostituzione fallisce.

Però, il fatto che la dimostrazione per sostituzione fallisce non è abbastanza per concludere che non vale $T(n) = \Omega(n)$. Quindi proviamo a dimostrare formalmente che $T(n) = \mathcal{O}(n^{\alpha})$ per una costante $\alpha < 1$.
Nella dimostrazione ho trovato che un valore di $\alpha = \frac{5}{6}$ funziona (vedi sotto).

Quindi, procedendo induttivamente come per il caso del limite superiore iniziale, cerchiamo $c > 0, n_0 \in \mathbb{N}$ tale che $T(n) \le cn^{\alpha}$.

$$
T(n) = T\left(\frac{n}{2}\right) + T\left(\frac{n}{3}\right) + \sqrt{n} + 2 \le c\left(\frac{n}{2}\right)^{\alpha} + c\left(\frac{n}{3}\right)^{\alpha} + \sqrt{n} + 2
$$

Possiamo notare che $\sqrt{n} + 2 \le n^{\alpha}$ per $n \ge 5$ e con $\alpha = \frac{5}{6}$, quindi facciamo una maggiorazione:

$$
c\left(\frac{n}{2}\right)^{\alpha} + c\left(\frac{n}{3}\right)^{\alpha} + \sqrt{n} + 2 \le c\left(\frac{n}{2}\right)^{\alpha} + c\left(\frac{n}{3}\right)^{\alpha} + n^{\alpha} = cn^{\alpha}\left(\frac{1}{2}\right)^{\alpha} + cn^{\alpha}\left(\frac{1}{3}\right)^{\alpha} + n^{\alpha}
$$

Possiamo quindi riscrivere come:

$$
cn^{\alpha}\left(\left(\frac{1}{2}\right)^{\alpha} + \left(\frac{1}{3}\right)^{\alpha}\right) + n^{\alpha}
$$

Noi vogliamo che la somma sia minore o uguale a $cn^{\alpha}$:

$$
cn^{\alpha}\left(\left(\frac{1}{2}\right)^{\alpha} + \left(\frac{1}{3}\right)^{\alpha}\right) + n^{\alpha} \le cn^{\alpha}
$$

Questo vale se:

$$
c\left(1 - \left(\frac{1}{2}\right)^{\alpha} - \left(\frac{1}{3}\right)^{\alpha}\right)n^{\alpha} \ge n^{\alpha}
$$

Avendo scelto $\alpha = \frac{5}{6}$ possiamo vedere che il termine costante è positivo, ovvero si ha $1 - \left(\frac{1}{2}\right)^{\alpha} - \left(\frac{1}{3}\right)^{\alpha} > 0$.
Quindi, dividendo e semplificando i termini $n^{\alpha}$ abbiamo:

$$
c\left(1 - \left(\frac{1}{2}\right)^{\alpha} - \left(\frac{1}{3}\right)^{\alpha}\right) \ge 1
$$

E quindi basta poi scegliere un $c$ tale che:

$$
c \ge \frac{1}{1 - \left(\frac{1}{2}\right)^{\alpha} - \left(\frac{1}{3}\right)^{\alpha}}
$$

con un $n_0 \ge 5$.
Questo dimostra quindi che $T(n) = \mathcal{O}(n^{5/6})$ e quindi dimostra inequivocabilmente che è impossibile che la ricorrenza sia $T(n) = \Omega(n)$, confutando l'ipotesi iniziale.
