# Esercizi Huffman

### Esercizio 1

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffman per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\
\hline
\text{frequenza} & 37 & 4 & 12 & 6 & 9 & 17 & 8
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

**i. Processo di costruzione**
L’algoritmo di Huffman è un algoritmo greedy per la costruzione di codici liberi da prefissi per un dato alfabeto di caratteri date le corrispondenti frequenze. Utilizza un approccio bottom-up mediante una coda con priorità $Q$ (tipicamente implementata come min-heap).

Inizialmente, ciascun simbolo distinto viene reso nodo foglia usando la sua frequenza come priorità, e tutti questi nodi vengono inseriti nella coda $Q$. Dopodiché, finché $|Q| > 1$, si estraggono iterativamente i due nodi di priorità minima e si crea un nuovo nodo interno. Questo nuovo nodo ha come priorità la somma delle priorità dei due nodi estratti, i quali diventano rispettivamente il suo figlio sinistro e destro. Il nuovo nodo interno viene poi re-inserito nella coda $Q$.

Quando rimane un solo nodo nella coda, questo rappresenta la radice dell’albero binario completo. Ciascun simbolo si trova su una foglia e il suo codice libero da prefissi si ottiene tracciando il cammino dalla radice alla foglia, adottando per convenzione l'etichettatura con il bit $0$ quando si scende verso il figlio sinistro e con il bit $1$ quando si scende verso il figlio destro.

**ii. Albero e Codici Generati**
L’albero binario ottenuto con le frequenze fornite è il seguente:

```text
                93
               /  \
             56   a:37      
           /   \
        22      34
       /  \    /   \
     10 c:12  17 f:17
    /  \     /  \
   b:4 d:6  g:8 e:9
```

Applicando la convenzione ($0$ a sinistra, $1$ a destra), i codici liberi da prefissi ottimi sono:
*   **a**: $1$
*   **b**: $0000$
*   **c**: $001$
*   **d**: $0001$
*   **e**: $0101$
*   **f**: $011$
*   **g**: $0100$

---
<br>

### Esercizio 2

Dato un file sull'alfabeto $\{A,B,C,D,E\}$ con frequenze, rispettivamente, 12%, 11%, 53%, 10%, 14%, si determinino le 5 codeword ottenute con la codifica di Huffman.

---

**i. Evoluzione della coda di priorità**
Simuliamo l'evoluzione della coda con priorità $Q$ contenente le frequenze percentuali. All’inizio abbiamo i simboli ordinati per frequenza crescente:
$Q = (D:10), (B:11), (A:12), (E:14), (C:53)$

Estraendo i due minimi ad ogni passo (da $i=1$ a $4$), otteniamo:
*   **i=1:** Estratti $D:10$ e $B:11$ (somma $21$).
    $Q = (A:12), (E:14), 21, (C:53)$
*   **i=2:** Estratti $A:12$ ed $E:14$ (somma $26$).
    $Q = 21, 26, (C:53)$
*   **i=3:** Estratti $21$ e $26$ (somma $47$).
    $Q = 47, (C:53)$
*   **i=4:** Estratti $47$ e $C:53$ (somma $100$).
    $Q = 100$ (radice dell'albero)

**ii. Codici Generati**
Sviluppando mentalmente l'albero corrispondente alle unioni appena fatte e assumendo di etichettare i bordi con la stessa convenzione usata nell'esercizio 1 ($0$ per le diramazioni a sinistra e $1$ per quelle a destra), si ottengono i seguenti codici liberi da prefissi $e(X)$:

*   **e(A)** = $010$
*   **e(B)** = $001$
*   **e(C)** = $1$
*   **e(D)** = $000$
*   **e(E)** = $011$
