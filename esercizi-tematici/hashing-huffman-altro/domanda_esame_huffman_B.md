# Domanda Esame B — 5 punti

Indicare, in forma di albero binario, il codice libero da prefissi ottenuto tramite l'algoritmo di Huffman per l'alfabeto $\{a, b, c, d, e, f\}$ supponendo che ogni carattere appaia con le seguenti frequenze:

$$
\begin{array}{c|cccccc}
& a & b & c & d & e & f \\
\hline
\text{frequenza} & 45 & 13 & 12 & 16 & 9 & 5
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### i. Processo di costruzione del codice

L’algoritmo di Huffman utilizza un approccio greedy bottom-up tramite l’utilizzo di una coda con priorità $Q$ (implementata come min-heap). Inizialmente, ciascun simbolo distinto viene reso nodo foglia e inserito nella coda $Q$ utilizzando la rispettiva frequenza come priorità.

Dopodiché, finché $|Q| > 1$ si estraggono i due nodi di priorità minore, si costruisce un nuovo nodo interno con priorità uguale alla somma dei due minimi estratti e si impostano come figlio sinistro e destro del nuovo nodo rispettivamente il primo e il secondo minimo estratto. Infine, si re-inserisce il nuovo nodo interno creato nella coda $Q$.

Questo processo termina quando è rimasto un solo elemento, ovvero la radice, al quale punto si etichettano i bordi dell’albero binario costruito con $0$ e $1$ (per convenzione $0$ quando si scende a sinistra e $1$ quando si scende a destra). Ciascun simbolo è situato in una foglia dell’albero binario e si può ricostruire il suo codice libero da prefissi concatenando gli $0$ e $1$ trovati percorrendo il cammino dalla radice alla sua foglia.

---

### ii. Evoluzione della coda di priorità

Con i simboli e le frequenze date nell’esercizio, ordinandole inizialmente per frequenza crescente abbiamo la seguente coda:
$Q = (f:5), (e:9), (c:12), (b:13), (d:16), (a:45)$

Mostriamo la coda aggiornata dopo ogni estrazione dei due minimi, creazione del nodo interno e re-inserimento (scorrendo da $i=1$ a $5$):

*   **i=1:** Estratti $f:5$ ed $e:9$ (somma $14$).
    $Q = (c:12), (b:13), 14, (d:16), (a:45)$
*   **i=2:** Estratti $c:12$ e $b:13$ (somma $25$).
    $Q = 14, (d:16), 25, (a:45)$
*   **i=3:** Estratti $14$ e $d:16$ (somma $30$).
    $Q = 25, 30, (a:45)$
*   **i=4:** Estratti $25$ e $30$ (somma $55$).
    $Q = (a:45), 55$
*   **i=5:** Estratti $45$ e $55$ (somma $100$).
    $Q = 100$ (la radice dell'albero)

---

### iii. Costruzione dell'Albero Binario

L'albero finale ottenuto dalle unioni precedenti è il seguente:

```text
                     100
                   /     \
                 55       a:45
               /    \
             30      25
            /  \    /  \
          14 d:16 c:12 b:13
         /  \
       f:5  e:9
```

---

### iv. Codici Generati

Con la convenzione di etichettare con $0$ quando scendiamo a sinistra e $1$ quando scendiamo a destra, otteniamo i seguenti codici liberi da prefissi:

*   **a**: $1$
*   **b**: $011$
*   **c**: $010$
*   **d**: $001$
*   **e**: $0001$
*   **f**: $0000$
