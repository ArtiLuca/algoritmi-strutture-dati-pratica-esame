# Domanda B — Longest Common Subsequence (LCS)

Scrivere la ricorrenza sulle lunghezze $\ell(i,j)$ per il problema della Longest Common Subsequence (LCS).

---

### i. Definizioni Preliminari

Date due stringhe (o sequenze):
$X = \langle x_1, x_2, \dots , x_m \rangle$
$Y = \langle y_1, y_2, \dots , y_n \rangle$

Definiamo i loro prefissi di lunghezza $i$ e $j$ rispettivamente come $X_i = \langle x_1, \dots, x_i \rangle$ e $Y_j = \langle y_1, \dots, y_j \rangle$.
Indichiamo con $\ell(i, j)$ la lunghezza della più lunga sottosequenza comune (LCS) tra i prefissi $X_i$ e $Y_j$, ovvero:

$$
\ell(i, j) = |\text{LCS}(X_i, Y_j)|
$$

---

### ii. Ricorrenza

La caratterizzazione ricorsiva per la lunghezza $\ell(i, j)$ è definita come segue:

$$
\ell(i, j) =
\begin{cases}
0 & \text{se } i = 0 \text{ oppure } j = 0 \\
1 + \ell(i-1, j-1) & \text{se } i, j > 0 \text{ e } x_i = y_j \\
\max(\ell(i-1, j), \ell(i, j-1)) & \text{se } i, j > 0 \text{ e } x_i \ne y_j
\end{cases}
$$

Il valore finale che ci interessa per risolvere il problema della LCS sull'intero input sarà ovviamente $\ell(m, n)$.
