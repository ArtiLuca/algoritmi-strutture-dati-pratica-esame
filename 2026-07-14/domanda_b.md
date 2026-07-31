# Soluzione - Domanda B

Date due stringhe:

$$X = \langle x_1, \dots, x_m \rangle \qquad Y = \langle y_1, \dots, y_n \rangle,$$

la lunghezza della Longest Common Subsequence (LCS) $\ell(i,j)$ tra i prefissi $X[1..i]$ e $Y[1..j]$ è definita come:

$$
\ell(i,j)=
\begin{cases}
0 & \text{se } i=0 \text{ oppure } j=0, \\
\ell(i-1,j-1)+1 & \text{se } i,j>0 \text{ e } x_i=y_j, \\
\max\{\ell(i-1,j),\ell(i,j-1)\} & \text{se } i,j>0 \text{ e } x_i\ne y_j.
\end{cases}
$$

La ricorrenza segue dalle seguenti osservazioni:

*   **Casi base:** se uno dei due prefissi è vuoto, cioè $i=0$ oppure $j=0$, allora la lunghezza della LCS è 0.
*   **Caratteri uguali:** se i caratteri correnti corrispondono, cioè $x_i=y_j$, allora possiamo estendere di 1 la LCS trovata eliminando entrambi i caratteri correnti.
*   **Caratteri diversi:** se i caratteri correnti differiscono, cioè $x_i\ne y_j$, allora dobbiamo valutare se conviene scartare l'ultimo carattere di $X$ oppure l'ultimo carattere di $Y$, prendendo il massimo tra le due possibilità.

La lunghezza della LCS delle due stringhe intere è quindi:

$$\ell(m,n)$$
