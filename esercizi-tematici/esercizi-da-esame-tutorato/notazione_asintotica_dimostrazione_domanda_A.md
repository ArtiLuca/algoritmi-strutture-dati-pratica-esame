# Domanda A — Classi $\mathcal{O}$ e $\Omega$

Dare la definizione formale delle classi $\mathcal{O}(f(n))$ e $\Omega(f(n))$ per una funzione $f(n)$.
Mostrare che se $f(n) = \mathcal{O}(n)$ e $g(n) = n^2 - f(n),$ allora $g(n) = \Omega(n^2)$.

---

### i. Definizioni Formali

Date due funzioni arbitrarie $f(n), h(n)$ asintoticamente positive, possiamo definire le classi:

$$
\mathcal{O}(f(n)) = \{h(n) \mid \exists c > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0 : 0 \le h(n) \le c \cdot f(n)\}
$$

$$
\Omega(f(n)) = \{h(n) \mid \exists d > 0, \exists n_0 \in \mathbb{N}, \forall n \ge n_0 : 0 \le d \cdot f(n) \le h(n)\}
$$

---

### ii. Dimostrazione

Vogliamo dimostrare che:

$$
\text{se } f(n) = \mathcal{O}(n) \text{ e } g(n) = n^2 - f(n) \implies g(n) = \Omega(n^2)
$$

Abbiamo due ipotesi:
- **Ipotesi 1:** $f(n) = \mathcal{O}(n)$ da cui segue per definizione della classe $\mathcal{O}$ che $\exists c > 0, \exists n_1 \in \mathbb{N}$ tale che $f(n) \le c \cdot n$ per ogni $n \ge n_1$.
- **Ipotesi 2:** $g(n) = n^2 - f(n)$.

**La nostra tesi:** $g(n) = \Omega(n^2)$ che, per definizione della classe $\Omega$, significa dimostrare che $\exists d > 0, \exists n_0 \in \mathbb{N}$ tale che $g(n) \ge d \cdot n^2$ per ogni $n \ge n_0$.

**Svolgimento:**
Applicando l'Ipotesi 1 all'interno dell'Ipotesi 2, e invertendo il verso della disuguaglianza a causa del segno meno, otteniamo:

$$
g(n) = n^2 - f(n) \ge n^2 - cn
$$

Vogliamo trovare un $d > 0$ tale che valga la disuguaglianza della nostra tesi $g(n) \ge dn^2$. Imponendo quindi $n^2 - cn \ge dn^2$, scegliamo un valore arbitrario per $d > 0$, ad esempio $d = \frac{1}{2}$. Otteniamo la seguente serie di disuguaglianze:

$$
n^2 - cn \ge \frac{1}{2}n^2 \implies \frac{1}{2}n^2 - cn \ge 0 \implies \frac{1}{2}n^2 \ge cn
$$

Assumendo che $n > 0$, possiamo dividere entrambi i lati per $n$ ottenendo:

$$
\frac{1}{2}n \ge c \implies n \ge 2c
$$

Quindi, scegliendo $n_0 = \max(n_1, \lceil 2c \rceil)$, possiamo concludere che vale definitivamente $g(n) \ge dn^2$.
Avendo trovato una costante moltiplicativa $d = \frac{1}{2}$ e un $n_0$ validi, ricordando la definizione della classe $\Omega$, abbiamo dimostrato rigorosamente che:

$$
g(n) = \Omega(n^2)
$$
