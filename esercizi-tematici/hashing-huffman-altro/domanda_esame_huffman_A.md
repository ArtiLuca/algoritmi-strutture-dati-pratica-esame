# Domanda Esame A — 5 punti

Indicare, in forma di albero binario, il codice libero da prefissi ottenuto tramite l'algoritmo di Huffman per l'alfabeto $\{a,b,c,d,e\}$ supponendo che ogni carattere appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccc}
& a & b & c & d & e \\
\hline
\text{frequenza} & 12 & 10 & 13 & 57 & 8
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### i. Processo di costruzione del codice

L’algoritmo di Huffman utilizza un approccio greedy per calcolare il codice libero da prefissi ottimo tra tutti i codici che associano una codeword a ogni singolo carattere. Usa un approccio bottom-up assieme a una coda con priorità (implementata come un min-heap). In particolare, ogni nodo $z$ ha attributi $f(z)$ per indicare la frequenza del nodo, $left(z)$ per indicare il figlio sinistro e $right(z)$ per indicare il figlio destro.

Inizialmente, si inserisce ogni simbolo distinto dell’alfabeto dato come nodo foglia $z$ nella coda, usando la frequenza $f(z)$ come priorità del min-heap. Dopo aver inserito ciascun nodo come foglia, si applica la scelta greedy.
Ovvero, si continua finché la coda $Q$ non contiene un solo elemento, prendendo iterativamente i due nodi di priorità minore e costruendo un nuovo nodo che ha come priorità la somma dei due nodi estratti (cioè le loro frequenze). Nello specifico, si estraggono i due nodi $x$ e $y$ di frequenza minima e si crea un nuovo nodo interno $z$. Si imposta $f(z) = f(x) + f(y)$ e si impostano i riferimenti $left(z) = x$ e $right(z) = y$. Dopodiché, si re-inserisce questo nuovo nodo $z$ nella coda con priorità $Q$.

Si continua così finché non è rimasto un solo elemento all'interno della coda, che corrisponderà alla radice dell'albero finale.

L’albero binario ottenuto viene poi etichettato usando, per convenzione, $0$ quando si scende verso sinistra e $1$ quando si scende verso destra; la sequenza di questi $0$ e $1$ dalla radice alla foglia contenente un carattere rappresenta il suo codice prefisso.

---

### ii. Costruzione dell'Albero Binario

Con i simboli e le frequenze date dall’esercizio otteniamo l'albero binario mostrato di seguito:

```text
                  100
                 /    \
              43      d:57
             /  \
           18    25
          / \    / \
        e:8 b:10 a:12 c:13
```

---

### iii. Codici Generati

Con la convenzione di etichettare con $0$ quando scendiamo a sinistra e $1$ quando scendiamo a destra, otteniamo i seguenti codici liberi da prefissi:

*   **a**: $010$
*   **b**: $001$
*   **c**: $011$
*   **d**: $1$
*   **e**: $000$
