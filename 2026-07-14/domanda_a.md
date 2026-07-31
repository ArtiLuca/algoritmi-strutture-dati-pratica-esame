# Soluzione - Domanda A

Abbiamo la ricorrenza:

```math
T(n)=\frac{3}{2}T(n-1)+2.
```

## Dimostrazione del limite superiore: `T(n) = O(2^n)`

Vogliamo dimostrare che:

```math
\exists c>0,\ \exists n_0\in\mathbb{N},\ \forall n\ge n_0:
T(n)\le c\cdot 2^n.
```

Assumiamo come ipotesi induttiva che la proprietà valga per `n-1`, cioè:

```math
T(n-1)\le c\cdot 2^{n-1}.
```

Applicando l'ipotesi induttiva alla ricorrenza otteniamo:

```math
T(n)
=
\frac{3}{2}T(n-1)+2
\le
\frac{3}{2}\left(c\cdot 2^{n-1}\right)+2.
```

Quindi:

```math
T(n)
\le
\frac{3}{4}c\cdot 2^n + 2.
```

Per concludere la dimostrazione vogliamo che:

```math
\frac{3}{4}c\cdot 2^n + 2
\le
c\cdot 2^n.
```

Spostando i termini:

```math
2
\le
\frac{1}{4}c\cdot 2^n.
```

Questa disuguaglianza è vera, per esempio, scegliendo `c >= 8` e considerando
`n >= 0`.

Infatti, per `n >= 0` vale `2^n >= 1`, quindi:

```math
\frac{1}{4}c\cdot 2^n
\ge
\frac{1}{4}\cdot 8 \cdot 1
=
2.
```

Con una scelta opportuna della costante `c`, che tenga conto anche del caso
base, segue che:

```math
T(n)=O(2^n).
```

---

## Dimostrazione del limite inferiore: `T(n) = Omega(2^n)`

La seconda affermazione, invece, **non è vera**.

Per dimostrarlo in modo più preciso, espandiamo la ricorrenza.

Per semplicità, assumiamo un caso base costante `T(0)`. Allora:

```math
T(n)
=
\left(\frac{3}{2}\right)^n T(0)
+
2\sum_{k=0}^{n-1}\left(\frac{3}{2}\right)^k.
```

La somma geometrica vale:

```math
\sum_{k=0}^{n-1}\left(\frac{3}{2}\right)^k
=
\frac{\left(\frac{3}{2}\right)^n-1}{\frac{3}{2}-1}
=
2\left(\left(\frac{3}{2}\right)^n-1\right).
```

Quindi:

```math
T(n)
=
\left(\frac{3}{2}\right)^n T(0)
+
4\left(\left(\frac{3}{2}\right)^n-1\right).
```

Ovvero:

```math
T(n)
=
(T(0)+4)\left(\frac{3}{2}\right)^n-4.
```

Quindi la ricorrenza cresce asintoticamente come:

```math
T(n)=\Theta\left(\left(\frac{3}{2}\right)^n\right).
```

Ora confrontiamo `T(n)` con `2^n`.

Consideriamo il rapporto:

```math
\frac{T(n)}{2^n}
=
\frac{(T(0)+4)\left(\frac{3}{2}\right)^n-4}{2^n}.
```

Separando i termini:

```math
\frac{T(n)}{2^n}
=
(T(0)+4)\left(\frac{3}{4}\right)^n
-
\frac{4}{2^n}.
```

Facendo tendere `n` all'infinito:

```math
\lim_{n\to\infty}\frac{T(n)}{2^n}=0.
```

Questo significa che `T(n)` cresce strettamente più lentamente di `2^n`.

Quindi non può esistere una costante `d > 0` tale che, definitivamente:

```math
T(n)\ge d\cdot 2^n.
```

Perciò:

```math
T(n)\ne \Omega(2^n).
```

In conclusione:

```math
T(n)=O(2^n)
```

ma:

```math
T(n)\ne \Omega(2^n).
```
