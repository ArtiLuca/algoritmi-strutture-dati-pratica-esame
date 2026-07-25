# Domanda A — Ricorrenza con Master Theorem

[← Torna all'appello](README.md)

## Testo

**Domanda A (5 punti)**

Si determini la soluzione asintotica della seguente equazione di ricorrenza:

```math
T(n)=3T(n/3)+n^2+1.
```

---

## Soluzione

Applichiamo il Master Theorem alla ricorrenza:

```math
T(n)=3T(n/3)+n^2+1.
```

Abbiamo:

```math
a=3,
\qquad
b=3,
\qquad
f(n)=n^2+1.
```

Calcoliamo quindi:

```math
n^{\log_b a}
=
n^{\log_3 3}
=
n.
```

Confrontiamo ora $f(n)$ con $n^{\log_b a}$:

```math
f(n)=n^2+1.
```

Quindi $f(n)$ è polinomialmente più grande di $n$. In particolare:

```math
f(n)=\Omega(n^{1+\varepsilon})
```

per esempio scegliendo $\varepsilon=1$.

Siamo quindi nel possibile caso 3 del Master Theorem, ma dobbiamo verificare
anche la condizione di regolarità.

La condizione richiede che esistano una costante $c<1$ e un valore $n_0$ tali
che, per ogni $n\ge n_0$:

```math
a\cdot f(n/b) \le c\cdot f(n).
```

Nel nostro caso:

```math
3f(n/3)
=
3\left(\left(\frac{n}{3}\right)^2+1\right)
=
3\left(\frac{n^2}{9}+1\right)
=
\frac{n^2}{3}+3.
```

Dobbiamo quindi confrontare:

```math
\frac{n^2}{3}+3
```

con:

```math
n^2+1.
```

Infatti:

```math
\lim_{n\to\infty}
\frac{\frac{n^2}{3}+3}{n^2+1}
=
\frac{1}{3}.
```

Quindi possiamo scegliere una costante $c$ tale che:

```math
\frac{1}{3}<c<1,
```

ad esempio $c=\frac{1}{2}$, per $n$ sufficientemente grande.

La condizione di regolarità è quindi soddisfatta.

Per il caso 3 del Master Theorem otteniamo:

```math
T(n)=\Theta(f(n)).
```

Poiché:

```math
f(n)=n^2+1=\Theta(n^2),
```

concludiamo che:

```math
\boxed{T(n)=\Theta(n^2)}.
```
