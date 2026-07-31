# Soluzione - Domanda B

Date due stringhe $X = \{x_1, \dots, x_m\}$ e $Y = \{y_1, \dots, y_n\}$, la lunghezza della Longest Common Subsequence (LCS) $\ell(i,j)$ tra i prefissi di lunghezza $i$ e $j$ è definita come:

$$
\ell(i,j) = \begin{cases}
0 & \text{se } i=0 \text{ oppure } j=0 \\
\ell(i-1,j-1) + 1 & \text{se } i,j > 0 \text{ e } x_i = y_j \\
\max(\ell(i-1,j), \ell(i,j-1)) & \text{se } i,j > 0 \text{ e } x_i \ne y_j
\end{cases}
$$

La ricorrenza segue dalle seguenti osservazioni:

* **Casi base:** se i prefissi sono vuoti ($i=0$ oppure $j=0$), allora la lunghezza della LCS è 0.
* **Caratteri uguali:** se i caratteri correnti corrispondono ($x_i = y_j$), estendiamo di 1 la LCS trovata finora eliminando entrambi i caratteri correnti.
* **Caratteri diversi:** se i caratteri correnti differiscono ($x_i \ne y_j$), dobbiamo valutare se ci conviene scartare l'ultimo carattere di $X$ oppure l'ultimo carattere di $Y$ per massimizzare la LCS (prendendo il massimo tra le due opzioni).
