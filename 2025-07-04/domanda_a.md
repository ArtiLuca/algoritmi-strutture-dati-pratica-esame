# Domanda A — Ricorrenza con metodo di sostituzione

[← Torna all'appello](README.md)

## Testo

**Domanda A (6 punti)**

Si dimostri che la ricorrenza che segue ha soluzione $T(n)=\Theta(n)$:

```math
T(n)=\frac{2}{3}T(n-1)+2n.
```

---

## Soluzione

Vogliamo dimostrare che:

```math
T(n)=\Theta(n).
```

Usiamo il metodo di sostituzione, dimostrando separatamente:

```math
T(n)=O(n)
```

e:

```math
T(n)=\Omega(n).
```

---

## Limite superiore

Dimostriamo che $T(n)=O(n)$.

Vogliamo trovare una costante $c>0$ tale che, per $n$ sufficientemente grande:

```math
T(n)\le cn.
```

Supponiamo per ipotesi induttiva che:

```math
T(n-1)\le c(n-1).
```

Allora:

```math
\begin{aligned}
T(n)
&=\frac{2}{3}T(n-1)+2n\\
&\le \frac{2}{3}c(n-1)+2n\\
&=\frac{2}{3}cn-\frac{2}{3}c+2n\\
&=\left(\frac{2}{3}c+2\right)n-\frac{2}{3}c.
\end{aligned}
```

Vogliamo che questa quantità sia al più $cn$.

È sufficiente scegliere $c$ tale che:

```math
\frac{2}{3}c+2\le c.
```

Quindi:

```math
2\le \frac{1}{3}c,
```

da cui basta prendere:

```math
c\ge 6.
```

Con $c=6$ otteniamo:

```math
T(n)\le 6n-4\le 6n.
```

Quindi $T(n)=O(n)$.

---

## Limite inferiore

Dimostriamo ora che $T(n)=\Omega(n)$.

Vogliamo trovare una costante $d>0$ tale che, per $n$ sufficientemente grande:

```math
T(n)\ge dn.
```

Supponiamo per ipotesi induttiva che:

```math
T(n-1)\ge d(n-1).
```

Allora:

```math
\begin{aligned}
T(n)
&=\frac{2}{3}T(n-1)+2n\\
&\ge \frac{2}{3}d(n-1)+2n\\
&=\frac{2}{3}dn-\frac{2}{3}d+2n\\
&=\left(\frac{2}{3}d+2\right)n-\frac{2}{3}d.
\end{aligned}
```

Vogliamo che questa quantità sia almeno $dn$.

Scegliendo $d=2$, otteniamo:

```math
T(n)\ge \left(\frac{4}{3}+2\right)n-\frac{4}{3}
=
\frac{10}{3}n-\frac{4}{3}.
```

Per ogni $n\ge 1$ vale:

```math
\frac{10}{3}n-\frac{4}{3}\ge 2n.
```

Quindi, con $d=2$, abbiamo:

```math
T(n)\ge 2n.
```

Di conseguenza $T(n)=\Omega(n)$.

---

## Conclusione

Abbiamo dimostrato sia:

```math
T(n)=O(n)
```

sia:

```math
T(n)=\Omega(n).
```

Quindi:

```math
\boxed{T(n)=\Theta(n)}.
```
