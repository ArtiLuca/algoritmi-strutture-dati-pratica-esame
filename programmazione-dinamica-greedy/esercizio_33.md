# Esercizio Soste Auto (Greedy)

Si supponga di voler viaggiare dalla città `A` alla città `B` con un'auto che ha
un'autonomia pari a `d` km.

Lungo il percorso si trovano `n - 1` distributori:

```math
D_1, \dots, D_{n-1},
```

a distanze:

```math
d_1, \dots, d_n
```

con `d_i <= d`, come indicato in figura:

```text
D_0 = A ... D_1 ... D_2 ... D_{n-1} ... D_n = B
```

L'auto ha inizialmente il serbatoio pieno e l'obiettivo è quello di percorrere
il viaggio da `A` a `B`, minimizzando il numero di soste ai distributori per il
rifornimento.

- **i.** Introdurre la nozione di soluzione per il problema e di costo della
  soluzione. Mostrare che vale la proprietà della sottostruttura ottima e
  individuare una scelta che gode della proprietà della scelta greedy.
- **ii.** Sulla base della scelta greedy individuata al passo precedente,
  fornire un algoritmo greedy `stop(d,n)` che dato in input l'array delle
  distanze `d[1..n]` restituisce una soluzione ottima.
- **iii.** Valutare la complessità dell'algoritmo.

---  

In generale una soluzione per il problema è $S = D_0, D_1, \dots, D_n$, ovvero i distributori a cui decidiamo di fermarci per fare il pieno. Più specificamente, possiamo definire una soluzione per il problema come l’insieme dei distributori $S = D_{i_0} \dots D_{i_k}$ dove $D_{i_0} = A$ e $D_{i_k} = B$.

In particolare possiamo definire per ogni coppia di distributori $D_i, D_j$ con $i \le j$ la distanza fra questi usando la notazione:

$$
d_{i,j} = \sum_{h=i+1}^{j} d_h
$$

Deve valere che per ogni $j \in \{0 \dots k-1\}$ si ha $d_{i_j, i_{j+1}} \le d$, cioè non possiamo superare l’autonomia $d$ dell'auto a disposizione tra due distributori.
Quindi, il costo può essere espresso semplicemente come il numero di soste che effettuiamo ai vari distributori, ovvero definiamo il costo come $c(S) = k - 1$.

La scelta greedy è di riuscire ad arrivare al distributore più lontano con l’autonomia che abbiamo a disposizione.
Ovvero, se ci troviamo al distributore $D_i$ allora vogliamo arrivare al distributore $D_k$ più lontano, ovvero vogliamo trovare $k = \max\{j \mid d_{i,j} \le d\}$, che è la distanza massima che possiamo percorrere senza finire l’autonomia dell’auto.

---

### i. Dimostrazione della proprietà della scelta greedy

Sia $S^{\ast}$ una soluzione ottima. Supponiamo che $D_x$ sia la prima sosta effettuata partendo da $D_0 = A$.
Sia $D_k$ il distributore che rappresenta la nostra scelta greedy, ovvero il distributore più lontano raggiungibile da $D_0$. Poiché $D_x$ è raggiungibile da $D_0$, per definizione di scelta greedy vale $x \le k$.

- Se $x = k$, allora la soluzione ottima contiene già la scelta greedy.
- Altrimenti, se $x < k$, vogliamo costruire una soluzione ottima alternativa che contenga $D_k$.

Consideriamo in $S^{\ast}$ la prima sosta $D_y$ che si trova dopo $D_k$.
Tutte le eventuali soste di $S^{\ast}$ tra $D_x$ e $D_k$ possono essere eliminate, perché scegliendo $D_k$ siamo arrivati più avanti senza usare più soste.

Inoltre, il tratto da $D_k$ a $D_y$ è percorribile. Infatti, nella soluzione $S^\ast$, il distributore $D_y$ veniva raggiunto partendo da una sosta precedente $D_z$ con $z \le k$. Poiché $D_k$ si trova più avanti di $D_z$, la distanza da $D_k$ a $D_y$ non è maggiore della distanza da $D_z$ a $D_y$, che era già percorribile.

Otteniamo quindi una soluzione ammissibile che contiene la scelta greedy $D_k$ e usa un numero di soste non maggiore di $S^\ast$.
Poiché $S^\ast$ era ottima, anche questa nuova soluzione è ottima.
Dunque esiste una soluzione ottima che contiene la scelta greedy.

---

### ii. Dimostrazione della proprietà di sottostruttura ottima

Supponiamo che $S^{\ast}$ sia una soluzione ottima per il problema $A \dots B$, e che la prima sosta effettuata sia al distributore $D_k$.
Quindi $S^* = \{D_k\} \cup S_{k,B}$ dove $S_{k,B}$ è soluzione per il problema $D_k \dots B$.

Supponiamo per assurdo che la tratta rimanente per arrivare da $D_k$ a $B$ non sia ottimale, ovvero che esista un sottoinsieme di soste $S_{k,B}^{\prime}$ che risolve il problema di arrivare da $D_k$ a $B$ usando un numero minore di soste.

Questo vorrebbe dire che se unissimo questa ipotetica soluzione con la prima sosta $D_k$ otterremmo una soluzione $S^{\prime}$ tale che:

$$
S^{\prime} = S_{k,B}^{\prime} \cup \{D_k\}
$$

con un numero minore di soste.
Ovvero tale che $\vert{}S^{\prime}\vert{} < \vert{}S^{\ast}\vert{}$, che è assurdo perché abbiamo definito $S^{\ast}$ come soluzione ottima per il problema con il minor numero di soste.

---

### iii. Pseudocodice

Un possibile pseudocodice per la procedura `stop(d, n)` prende in input l’array $d[1\dots n]$ delle distanze e restituisce l’insieme $S[1\dots n-1]$ dei distributori scelti a cui fermarsi.
*Nota: la prima e ultima sosta sono scelte sempre, quindi non serve indicarlo.*

```algorithmic
// assumendo d_max sia l'autonomia massima
stop(d, n)
    S = ∅
    dist = 0

    for i = 1 to n
        // se una singola tratta supera l'autonomia, il viaggio è impossibile
        if d[i] > d_max
            return IMPOSSIBLE

        // se aggiungere la prossima tratta supera l'autonomia,
        // mi fermo al distributore precedente
        if dist + d[i] > d_max
            S = S U {i - 1}
            dist = d[i]
        else
            dist = dist + d[i]

    return S
```

---

### iv. Complessità

La complessità attesa sarà $\Theta(n)$ essendo una semplice scansione lineare dell'array delle distanze.
La complessità spaziale è $\mathcal{O}(n)$ per memorizzare l'insieme $S$ delle soste effettuate.

Se non si considera lo spazio necessario per restituire la soluzione, lo spazio ausiliario usato dall'algoritmo è $\Theta(1)$.
