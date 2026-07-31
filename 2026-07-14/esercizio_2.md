# Soluzione - Esercizio 2

## Punto (a)

Per quanto riguarda il punto (a), una scelta di $n = 60$ con monete $\{50, 20, 1\}$ non restituisce una soluzione ottima con la logica greedy di selezionare sempre la moneta di valore massimo.

Infatti, con la scelta greedy si ha:

$$M_{\text{greedy}}=\{50,1,1,1,1,1,1,1,1,1,1\}$$

Questa soluzione usa 11 monete.

Invece, una soluzione ottima è:

$$M^\star=\{20,20,20\}$$

Questa soluzione usa solo 3 monete.

Quindi:

$$|M_{\text{greedy}}|=11>3=|M^\star|$$

Pertanto, per il sistema di monete $\{50, 20, 1\}$, la scelta greedy della moneta massima non è sempre ottima.

---

## Punto (b)

Per quanto riguarda il punto (b), consideriamo il sistema di monete:

$$\{10,5,1\}$$

Sia $n$ l'importo positivo che vogliamo ottenere e sia $g$ la scelta greedy, cioè la moneta di valore massimo tale che:

$$g \le n$$

Dobbiamo dimostrare che esiste una soluzione ottima che contiene la scelta greedy $g$.

Sia $M^*$ una soluzione ottima, cioè un multinsieme di monete che somma a $n$ usando il minor numero possibile di monete.

Se $M^*$ contiene già $g$, allora abbiamo finito.

Supponiamo invece che $M^*$ non contenga $g$.

Allora $M^*$ contiene solo monete di valore strettamente minore di $g$. Vogliamo mostrare che in $M^*$ deve esistere un insieme di monete più piccole che somma esattamente a $g$.

Questo è vero per il sistema $\{10,5,1\}$:

*   **se $g = 1$**: allora la scelta greedy è l'unica moneta utilizzabile, quindi ogni soluzione ammissibile deve contenerla;
*   **se $g = 5$**: allora $5 \le n < 10$. Se una soluzione ottima non usa la moneta da 5, allora usa solo monete da 1. Poiché deve sommare almeno a 5, contiene almeno cinque monete da 1, che possono essere sostituite da una sola moneta da 5;
*   **se $g = 10$**: allora $n \ge 10$. Se una soluzione ottima non usa la moneta da 10, allora usa solo monete da 5 e da 1. In ogni caso, tra queste monete esiste un sottoinsieme che somma a 10: due monete da 5, oppure una moneta da 5 e cinque monete da 1, oppure dieci monete da 1.

Quindi, se $M^*$ non contiene $g$, esiste un sottoinsieme $X$ di monete di $M^*$ tale che:

$$\sum_{x \in X} x = g$$

Inoltre, siccome tutte le monete in $X$ sono più piccole di $g$, il sottoinsieme $X$ contiene almeno due monete:

$$|X| > 1$$

Costruiamo allora una nuova soluzione $M'$ sostituendo le monete di $X$ con la sola moneta $g$:

$$M' = (M^* \setminus X) \cup \{g\}$$

La nuova soluzione è ancora ammissibile, perché la somma totale non cambia: abbiamo rimosso monete che sommano a $g$ e inserito una moneta di valore $g$.

Però il numero di monete diminuisce:

$$|M'| = |M^*| - |X| + 1$$

Poiché $|X| > 1$, segue che:

$$|M'| < |M^*|$$

Questo contraddice l'ipotesi che $M^*$ fosse una soluzione ottima.

Quindi l'ipotesi che $M^*$ non contenga $g$ è falsa. Dunque esiste una soluzione ottima che contiene la scelta greedy.

Questo dimostra la proprietà di scelta greedy per il sistema di monete $\{10,5,1\}$.
