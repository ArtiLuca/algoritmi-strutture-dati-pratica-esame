# Domanda A — Classe \(\Omega\) e proprietà asintotiche

[← Torna all'appello](README.md)

## Testo

**Domanda A (7 punti)**

Dare la definizione formale della classe \(\Omega(f(n))\) per una funzione
\(f(n)\).

Mostrare che, date due funzioni \(f(n)\) e \(g(n)\), che si possono assumere
sempre positive, se:

\[
f(n)=\Omega(n^2),
\]

allora:

\[
f(n)+g(n)=\Omega(n^2+g(n)).
\]

Vale anche:

\[
f(n)-g(n)=\Omega(n^2-g(n))?
\]

Dimostrarlo oppure fornire un controesempio.

---

## Soluzione

### Definizione formale di \(\Omega\)

Sia \(h(n)\) una funzione asintoticamente non negativa. La classe
\(\Omega(h(n))\) è definita come:

\[
\Omega(h(n))
=
\left\{
q(n)\ \middle|\
\exists c>0,\ \exists n_0\in\mathbb{N}
\text{ tali che }
\forall n\ge n_0,\
0\le c\,h(n)\le q(n)
\right\}.
\]

In altre parole, \(q(n)\in\Omega(h(n))\) se, a partire da un certo valore di
\(n\), la funzione \(q(n)\) è inferiormente limitata da un multiplo positivo di
\(h(n)\).

---

### Prima proprietà

Vogliamo dimostrare che:

\[
f(n)=\Omega(n^2)
\quad\Longrightarrow\quad
f(n)+g(n)=\Omega(n^2+g(n)).
\]

Per ipotesi:

\[
f(n)=\Omega(n^2).
\]

Quindi esistono una costante \(c_1>0\) e un valore \(n_1\in\mathbb{N}\) tali
che, per ogni \(n\ge n_1\),

\[
f(n)\ge c_1n^2.
\]

Poiché \(g(n)>0\), sommando \(g(n)\) a entrambi i membri otteniamo:

\[
f(n)+g(n)\ge c_1n^2+g(n).
\]

Scegliamo ora:

\[
c=\min\{c_1,1\}.
\]

Poiché \(c_1>0\), vale anche \(c>0\). Inoltre:

\[
c\le c_1
\qquad\text{e}\qquad
c\le 1.
\]

Di conseguenza:

\[
c_1n^2+g(n)
\ge
cn^2+cg(n)
=
c\bigl(n^2+g(n)\bigr).
\]

Pertanto, per ogni \(n\ge n_1\),

\[
f(n)+g(n)
\ge
c\bigl(n^2+g(n)\bigr).
\]

Per definizione segue che:

\[
\boxed{
f(n)+g(n)=\Omega(n^2+g(n))
}
\]

---

### Seconda proprietà

Consideriamo ora l'affermazione:

\[
f(n)=\Omega(n^2)
\quad\Longrightarrow\quad
f(n)-g(n)=\Omega(n^2-g(n)).
\]

Questa affermazione è falsa.

Consideriamo, per \(n\ge 3\), le due funzioni positive:

\[
f(n)=\frac12n^2
\]

e:

\[
g(n)=\frac12n^2-n.
\]

La funzione \(f(n)\) appartiene chiaramente a \(\Omega(n^2)\), perché:

\[
f(n)=\frac12n^2.
\]

Calcoliamo ora la differenza:

\[
f(n)-g(n)
=
\frac12n^2-\left(\frac12n^2-n\right)
=
n.
\]

D'altra parte:

\[
n^2-g(n)
=
n^2-\left(\frac12n^2-n\right)
=
\frac12n^2+n.
\]

Se fosse vero che:

\[
f(n)-g(n)=\Omega(n^2-g(n)),
\]

allora dovrebbero esistere \(c>0\) e \(n_0\in\mathbb{N}\) tali che, per ogni
\(n\ge n_0\),

\[
n
\ge
c\left(\frac12n^2+n\right).
\]

Dividendo entrambi i membri per \(\frac12n^2+n>0\), otterremmo:

\[
c
\le
\frac{n}{\frac12n^2+n}
=
\frac{1}{\frac12n+1}.
\]

Tuttavia:

\[
\lim_{n\to+\infty}
\frac{1}{\frac12n+1}
=
0.
\]

Non può quindi esistere una costante positiva \(c\) che soddisfi la
disuguaglianza per ogni \(n\) sufficientemente grande.

Pertanto:

\[
\boxed{
f(n)-g(n)\notin\Omega(n^2-g(n))
}
\]

e l'implicazione proposta è falsa.
