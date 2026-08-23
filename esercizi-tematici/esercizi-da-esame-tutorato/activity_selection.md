# Esercizio - Selezione Attività Compatibili

Si consideri il problema di selezione di attività compatibili, con $n$ attività
$a_1, \dots, a_n$ che ci vengono date attraverso due vettori $\mathbf{s}$ e $\mathbf{f}$ di
tempi di inizio e fine, e ordinate per tempo di *inizio*, cioè:

$$ 0 < s_1 \le s_2 \le \dots \le s_n $$

**(a)** Scrivere un algoritmo greedy iterativo che implementa la scelta greedy
di selezionare l'attività che inizia per ultima.

**(b)** Determinare l'insieme di attività restituito dall'algoritmo al punto
(a) quando eseguito sul seguente insieme di 6 attività, caratterizzate dai
seguenti vettori $\mathbf{s}$ e $\mathbf{f}$ di tempi di inizio e fine:

$$ \mathbf{s} = (1, 2, 3, 5, 7, 10) $$
$$ \mathbf{f} = (3, 9, 10, 7, 11, 12) $$

**(c)** Dimostrare la proprietà di scelta greedy, cioè che esiste soluzione
ottima che contiene l'attività che inizia per ultima.

---

### (a) Algoritmo Greedy

Per il punto (a) possiamo definire prima il problema generale, ovvero della selezione di attività compatibili.
Il problema consiste nel trovare un insieme $S = \{a_i : 1 \le i \le n\}$ di attività mutualmente compatibili di cardinalità massima.

In generale, abbiamo che un'attività è $a_i = [s_i, f_i)$ e diciamo che due attività $a_i, a_j$ sono compatibili se e solo se non si sovrappongono temporalmente, ovvero se $[s_i, f_i) \cap [s_j, f_j) = \emptyset$. In altre parole, serve che:
$f_i \le s_j$ oppure $f_j \le s_i$.

In questo caso la scelta greedy richiesta è quella di selezionare l’attività che inizia per ultima. Quindi, se le attività sono ordinate per tempo di inizio crescente, allora la scelta greedy equivale all’attività $a_n$.
Dopodiché, si scorrono le attività da $n-1 \dots 1$ e si seleziona un’attività $a_m$ solo se è compatibile con l’ultima attività selezionata (indicata con `last`). Ovvero, solo se l’attività $a_m$ finisce prima (o nel momento esatto) che inizia l’ultima attività selezionata ($f_m \le s_{\text{last}}$), nel qual caso viene aggiornato `last` per indicare l’ultima attività selezionata.

```algorithmic
GreedySelLast(s, f) // s,f vettori di tempo di inizio/fine

    // inizialmente, la soluzione contiene l'attività che inizia per ultima
    // essendo ordinate per tempo di inizio crescente, si sceglie a_n
    S = {a_n}
    last = n

    // scorro le attività all'indietro
    for m = n - 1 downto 1
        if f_m <= s_last
            S = S U {a_m}
            // aggiorna l'ultima attività selezionata
            last = m

    return S				
```

---

### (b) Esecuzione dell'algoritmo

Se abbiamo i vettori $\mathbf{s} = (1, 2, 3, 5, 7, 10)$ e $\mathbf{f} = (3, 9, 10, 7, 11, 12)$ di tempo di inizio/fine, allora abbiamo le seguenti attività:

- $a_1 = [1, 3)$
- $a_2 = [2, 9)$
- $a_3 = [3, 10)$
- $a_4 = [5, 7)$
- $a_5 = [7, 11)$
- $a_6 = [10, 12)$

Quindi inizialmente $S = \{a_6\}$ e $last = 6$.
- Non viene selezionata $a_5$ (perché $f_5 = 11 \not\le s_6 = 10$).
- Viene selezionata $a_4$ essendo che $f_4 = 7 \le s_6 = 10$, e quindi $S = \{a_6, a_4\}$ e $last = 4$.
- Le attività $a_3, a_2$ non sono compatibili (finiscono a $10$ e $9$, che non sono $\le s_4 = 5$).
- Invece $a_1$ è compatibile perché $f_1 = 3 \le s_4 = 5$.

Quindi alla fine l’algoritmo restituisce come soluzione l’insieme:

$$
S = \{a_6, a_4, a_1\}
$$

---

### (c) Dimostrazione della proprietà della scelta greedy

Vogliamo dimostrare che $\exists$ una soluzione ottima $A_{ij}^{\ast}$ che contiene la nostra scelta greedy, ovvero tale che $a_m \in A_{ij}^{\ast}$ (dove $a_m$ è la nostra scelta greedy, ovvero l'attività che inizia per ultima fra tutte).

Possiamo indicare la soluzione ottima $A_{ij}^{\ast}$ con la nostra scelta greedy come:

$$
A_{ij}^{\ast} = A_{im}^{\ast} \cup \{a_m\} \cup A_{mj}^{\ast}
$$

dove $A_{im}^{\ast}$ è soluzione ottima per il sottoproblema $S_{im}$ mentre $A_{mj}^{\ast}$ è soluzione ottima per il sottoproblema $S_{mj}$, dove possiamo vedere che $S_{mj} = \emptyset$ necessariamente, perché non esiste alcuna attività che inizia dopo $a_m$ (essendo $a_m$ la nostra scelta greedy che inizia per ultima).

Quindi, sia $A_{ij}^{\ast}$ una soluzione ottima per il problema $S_{ij}$ di selezione di attività compatibili di cardinalità massima, e sia $a_k$ l'attività al suo interno che inizia per ultima, ovvero $s_k = \max\{s_l : a_l \in A_{ij}^{\ast}\}$.

- Se $a_k = a_m$ allora coincide con la nostra scelta greedy e quindi abbiamo finito.
- Altrimenti, se $a_k \ne a_m$, allora sia $A_{ij}^{\ast}$ una soluzione ottima che non contiene la nostra scelta greedy.

Se unissimo questa soluzione con la nostra scelta greedy scambiandola con $a_k$, ovvero:

$$
A_{ij}^{\prime} = (A_{ij}^{\ast} \setminus \{a_k\}) \cup \{a_m\}
$$

otterremmo una soluzione ancora ammissibile.
Infatti, $|A_{ij}^{\prime}| = |A_{ij}^{\ast}|$ essendo che abbiamo solo scambiato un elemento (la cardinalità resta massima).
Inoltre, essendo che $a_m$ è l'attività che inizia per ultima in assoluto, allora vale per definizione che $s_k \le s_m$. L'attività $a_k$ non si sovrapponeva con alcuna attività in $A_{ij}^{\ast}$, il che significa che per ogni altra attività $a_l$ all’interno della soluzione valeva $f_l \le s_k$. Dalla transitività otteniamo $f_l \le s_k \le s_m$, e quindi $a_m$ è temporalmente compatibile con ogni altra attività $a_l$ rimasta nell'insieme.

Quindi, abbiamo dimostrato tramite un argomento di scambio che esiste una soluzione ottima che contiene la nostra scelta greedy.
