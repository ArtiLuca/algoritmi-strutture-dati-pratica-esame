# Soluzione - Esercizio 2

## Punto (a)

Per quanto riguarda il punto (a), una scelta di $n=60$ con monete $\{50, 20, 1\}$ non restituisce una soluzione ottima con la logica greedy di selezionare sempre la moneta di valore massimo.

Infatti, con la scelta greedy si ha:
$$M_{greedy} = \{50, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1\}$$

Mentre invece, una soluzione ottima sarebbe stata:
$$M^\star = \{20, 20, 20\}$$

Infatti $|M_{greedy}| = 11 > |M^\star| = 3$.

---

## Punto (b)

Per quanto riguarda il punto (b), siano $\{10, 5, 1\}$ le nostre monete, $n$ l'intero positivo a cui vogliamo arrivare e $M^\star$ una soluzione ottima. Dobbiamo dimostrare che $M^\star$ contiene sempre la scelta greedy, ovvero la moneta $g$ di valore maggiore tale che $g \le n$.

Se $M^\star$ contiene già $g$, allora abbiamo finito.

Altrimenti, supponiamo per assurdo che $M^\star$ non contenga la nostra scelta greedy $g$. Questo significa che $M^\star$ contiene solo monete di valore strettamente inferiore a $g$.

Poiché la somma di $M^\star$ deve totalizzare $n \ge g$, ed essendo che nel sistema $\{10, 5, 1\}$ ogni valore maggiore è un multiplo esatto dei tagli minori, all'interno di $M^\star$ deve per forza esistere un sottoinsieme di monete minori $X \subseteq M^\star$ che somma esattamente a $g$. Poiché le monete in $X$ sono più piccole di $g$, avremo sicuramente $|X| > 1$.

Consideriamo ora una nuova soluzione ammissibile $M'$ in cui scambiamo l'insieme $X$ con la nostra scelta greedy $g$:
$$M' = (M^\star \setminus X) \cup \{g\}$$

Calcoliamo la cardinalità di questa nuova soluzione:
$$|M'| = |M^\star| - |X| + 1$$

Dato che $|X| > 1$ (ovvero $|X| \ge 2$), segue che:
$$|M'| \le |M^\star| - 2 + 1 = |M^\star| - 1$$
Quindi $|M'| < |M^\star|$.

Questo però contraddice l'ipotesi di ottimalità di $M^\star$, poiché abbiamo trovato una soluzione ammissibile $M'$ con cardinalità strettamente minore. L'assurdo deriva dall'aver ipotizzato $g \notin M^\star$.

Quindi, abbiamo dimostrato che ogni soluzione ottima al problema contiene sempre la nostra scelta greedy.
