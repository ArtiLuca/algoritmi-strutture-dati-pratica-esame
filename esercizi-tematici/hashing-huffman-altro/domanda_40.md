# Domanda 40

Indicare il codice prefisso ottenuto utilizzando l'algoritmo di Huffman per l'alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\
\hline
\text{frequenza} & 16 & 12 & 2 & 8 & 3 & 9 & 6
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### i. Processo di costruzione del codice

L’algoritmo di Huffman utilizza un approccio greedy bottom-up mediante una coda con priorità (implementata come un min-heap). Inizialmente, ciascun simbolo distinto dell’alfabeto viene reso nodo foglia e inserito nella coda $Q$ usando la corrispondente frequenza del simbolo come sua priorità.

Dopodiché, finché $Q$ non è vuota, si estraggono i due nodi di priorità minore. Questi due nodi vengono utilizzati per costruire un nuovo nodo interno, avente come priorità la somma delle priorità dei due minimi estratti, come figlio sinistro il primo nodo estratto e come figlio destro il secondo. Questo nuovo nodo interno viene poi re-inserito all'interno della coda $Q$.

Quando rimane un solo elemento nella coda, ovvero la radice, si possono etichettare i bordi dell’albero binario ottenuto usando per convenzione $0$ quando si scende a sinistra e $1$ quando si scende a destra (la scelta simmetrica di usare $1$ a sinistra e $0$ a destra è del tutto analoga e produce codici liberi da prefissi altrettanto validi). Il codice libero da prefissi per ciascun simbolo è poi ottenuto seguendo il suo percorso dalla radice dell’albero alla corrispondente foglia, tracciando la sequenza degli $0$ e $1$ trovati lungo il cammino.

---

### ii. Albero di Huffman

Con i simboli e le frequenze fornite, l’albero binario ottenuto dall’algoritmo di Huffman è il seguente:

```text
                     56 
                 /         \ 
               23           33   
             /    \        /   \
            11   b:12     17    a:16
         /     \         /   \ 
        5      g:6      d:8  f:9 
      /   \ 
     c:2   e:3
```

---

### iii. Codici Generati

Usando la convenzione di assegnare $0$ quando si scende a sinistra e $1$ quando si scende a destra, otteniamo i seguenti codici liberi da prefissi ottimi:

*   **a**: $11$
*   **b**: $01$
*   **c**: $0000$
*   **d**: $100$
*   **e**: $0001$
*   **f**: $101$
*   **g**: $001$
