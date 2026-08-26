# Esercizio 2 — Scheduling greedy e somma dei tempi di completamento (10 punti)

Abbiamo $n$ programmi da eseguire sul nostro computer. Ogni programma $j$, con $j \in \{1, 2, \dots, n\}$, ha lunghezza $\ell_j$, che rappresenta la quantità di tempo richiesta per la sua esecuzione. Dato un ordine di esecuzione $\sigma = j_1, j_2, \dots, j_n$, il tempo di completamento $C_{j_i}(\sigma)$ del programma $j_i$ è dato dalla somma delle lunghezze dei programmi fino a $i$: $j_1, j_2, \dots, j_i$.
L'obiettivo è trovare un ordine di esecuzione $\sigma$ che minimizza la somma dei tempi di completamento di tutti i programmi, cioè: $\sum_{j=1}^{n} C_j(\sigma)$.

- **(a)** Dare un semplice algoritmo greedy per questo problema, e valutarne la complessità.
- **(b)** Dimostrare la proprietà di scelta greedy dell'algoritmo del punto (a), cioè che esiste un ordine di esecuzione ottimo $\sigma^\star$ che contiene la scelta greedy.

---

### (a) Algoritmo Greedy e Complessità

Possiamo minimizzare la somma dei tempi di completamento di tutti i programmi facendo la scelta greedy di eseguire sempre per primo il programma di lunghezza minore (SJF - *Shortest Job First*). Ovvero, un ordine di esecuzione ottimale può essere $\sigma = j_1, j_2, \dots, j_n$ dove i programmi sono ordinati per tempo di esecuzione crescente, tale che valga:

$$
\ell_{j_1} \le \ell_{j_2} \le \dots \le \ell_{j_n}
$$

Questa scelta necessita che i programmi vengano prima ordinati. Possiamo fare ciò utilizzando un array di supporto $P[1\dots n]$ per memorizzare gli indici dei programmi per poi ordinare $P$ in modo che i programmi risultino disposti in ordine crescente in base a $\ell[P[i]]$, dove $\ell[1\dots n]$ è l'array con i tempi di esecuzione.
Dopo l’ordinamento, si eseguono i programmi uno dopo l’altro, accumulando il tempo di completamento totale.

```text
ScheduleOPT(l, n)

    // allocazione array ausiliario per gli indici
    allocate P[1...n]
    for i = 1 to n
        P[i] = i

    ordina P per valori crescenti di l[P[i]]

    time = 0
    total = 0
    for i = 1 to n
        j = P[i]
        time = time + l[j]
        total = total + time

    return total, P[1...n]
```

**Complessità:** La complessità in questo caso è dominata dal costo dovuto all’ordinamento iniziale, che possiamo assumere sia $\Theta(n \log n)$ se usiamo un qualsiasi algoritmo ottimo di ordinamento per confronti (come `MergeSort` o `HeapSort`). Il calcolo successivo richiede tempo lineare $\Theta(n)$. Pertanto, la complessità totale è $T(n) = \Theta(n \log n)$.

---

### (b) Dimostrazione della proprietà di scelta greedy

Vogliamo dimostrare che esiste una soluzione ottimale che contiene la nostra scelta greedy, ovvero eseguire per primo il programma con tempo di esecuzione minore.

Sia $\sigma^\star$ una soluzione ottimale, ovvero un ordine di esecuzione che minimizza il tempo di completamento totale. Sia $j_m$ il programma che ha il tempo di esecuzione minore fra tutti, ovvero tale che $\ell_{j_m} = \min(\{\ell_{j_h} : j_h \in \sigma^\star\})$.

- Se $j_m$ coincide con il primo programma eseguito in $\sigma^\star$, allora la scelta greedy è già contenuta nell'ottimo e abbiamo dimostrato il teorema.
- Altrimenti, se $j_m$ non è il primo programma in assoluto in $\sigma^\star$, significa che esiste un programma $j_k$ che precede immediatamente l’esecuzione di $j_m$. Essendo che $j_m$ è per definizione il programma di lunghezza minima, avremo che vale $\ell_k \ge \ell_m$.

Prendiamo in considerazione solamente il tempo di completamento per questi due programmi adiacenti, assumendo che sia passato un lasso di tempo $T$ prima della loro esecuzione. Poiché scambiare due programmi adiacenti non modifica i tempi di completamento dei programmi precedenti (che terminano prima di $T$) né di quelli successivi (che inizieranno comunque al tempo $T + \ell_k + \ell_m$), il cambiamento nel costo totale dipenderà solo da questi due.

Se $\sigma^\star$ esegue questi programmi nell'ordine $j_k$ e poi $j_m$, la somma locale dei loro tempi di completamento sarà:

$$
C_{\text{locale}}(\sigma^\star) = (T + \ell_k) + (T + \ell_k + \ell_m) = 2T + 2\ell_k + \ell_m
$$

Se ora creiamo una nuova soluzione $\sigma^\prime$ scambiando l’ordine di esecuzione, in modo che venga eseguito prima $j_m$ e poi $j_k$, la nuova somma locale sarà:

$$
C_{\text{locale}}(\sigma^\prime) = (T + \ell_m) + (T + \ell_m + \ell_k) = 2T + 2\ell_m + \ell_k
$$

Confrontiamo il costo totale prima e dopo lo scambio (le restanti parti della sommatoria si elidono):

$$
C(\sigma^\star) - C(\sigma^\prime) = (2T + 2\ell_k + \ell_m) - (2T + 2\ell_m + \ell_k) = \ell_k - \ell_m
$$

Poiché $\ell_k \ge \ell_m$, vale che $\ell_k - \ell_m \ge 0$, il che implica:

$$
C(\sigma^\star) \ge C(\sigma^\prime)
$$

Visto che $\sigma^\star$ era per definizione una soluzione ottima (quindi col costo minimo possibile), deve necessariamente valere $C(\sigma^\star) = C(\sigma^\prime)$. Di conseguenza, anche $\sigma^\prime$ risulta essere un ordine di esecuzione ottimale.

Se $j_m$ non è ancora in prima posizione in $\sigma^\prime$, possiamo ripetere questo scambio con il programma adiacente a sinistra (al massimo $n-1$ volte) per farlo "risalire" in prima posizione, senza mai peggiorare il tempo di completamento totale.
Quindi, abbiamo dimostrato con un argomento di scambio che esiste sempre una soluzione ottima che contiene la nostra scelta greedy.
