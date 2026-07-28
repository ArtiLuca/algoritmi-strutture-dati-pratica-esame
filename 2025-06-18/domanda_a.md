# Domanda A — Classi O e Ω

[← Torna all'appello](README.md)

## Testo

**Domanda A (7 punti)**

Dare la definizione formale delle classi $O(f(n))$ e $\Omega(f(n))$ per una
funzione $f(n)$.

Mostrare che se:

```math
f(n)=O(n)
```

e:

```math
g(n)=n^2-f(n),
```

allora:

```math
g(n)=\Omega(n^2).
```

---

## Soluzione

## Definizioni formali

Siano $f(n)$ e $h(n)$ due funzioni asintoticamente non negative.

La classe $O(f(n))$ è definita come:

```math
O(f(n)) =
\{h(n) : \exists c>0,\ \exists n_0 \in \mathbb{N}
\text{ tali che } 0 \le h(n) \le c f(n)
\text{ per ogni } n \ge n_0\}.
```

La classe $\Omega(f(n))$ è definita come:

```math
\Omega(f(n)) =
\{h(n) : \exists d>0,\ \exists n_0 \in \mathbb{N}
\text{ tali che } 0 \le d f(n) \le h(n)
\text{ per ogni } n \ge n_0\}.
```

Nelle definizioni ho usato $h(n)$ come funzione generica, così da non confonderla
con la funzione $g(n)$ usata nella seconda parte della domanda.

---

## Dimostrazione

Per ipotesi:

```math
f(n)=O(n).
```

Quindi esistono due costanti $c_1>0$ e $n_1 \in \mathbb{N}$ tali che, per ogni
$n \ge n_1$:

```math
0 \le f(n) \le c_1 n.
```

Inoltre:

```math
g(n)=n^2-f(n).
```

Usando l'ipotesi $f(n)\le c_1 n$, otteniamo, per ogni $n \ge n_1$:

```math
g(n)=n^2-f(n) \ge n^2-c_1 n.
```

Vogliamo mostrare che $g(n)=\Omega(n^2)$, cioè vogliamo trovare due costanti
$d_1>0$ e $n_2 \in \mathbb{N}$ tali che, per ogni $n \ge n_2$:

```math
g(n) \ge d_1 n^2.
```

Dalla disuguaglianza precedente basta imporre:

```math
n^2-c_1 n \ge d_1 n^2.
```

Scegliamo, ad esempio:

```math
d_1=\frac{1}{2}.
```

Allora dobbiamo avere:

```math
n^2-c_1 n \ge \frac{1}{2}n^2.
```

Equivalentemente:

```math
\frac{1}{2}n^2 \ge c_1 n.
```

Per $n>0$, dividendo per $n$, otteniamo:

```math
n \ge 2c_1.
```

Quindi scegliendo:

```math
n_2=\max\{n_1,\lceil 2c_1\rceil\}
```

si ha, per ogni $n \ge n_2$:

```math
g(n) \ge \frac{1}{2}n^2.
```

Poiché $\frac{1}{2}>0$, abbiamo dimostrato che:

```math
g(n)=\Omega(n^2).
```
