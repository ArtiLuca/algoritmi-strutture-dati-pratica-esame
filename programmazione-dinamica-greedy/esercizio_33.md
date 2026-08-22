# Esercizio Soste Auto (Greedy)

In generale una soluzione per il problema è $S = D_0, D_1, \dots, D_n$, ovvero i distributori a cui decidiamo di fermarci per fare il pieno. Più specificamente, possiamo definire una soluzione per il problema come l’insieme dei distributori $S = D_{i_0} \dots D_{i_k}$ dove $D_{i_0} = A$ e $D_{i_k} = B$.

In particolare possiamo definire per ogni coppia di distributori $D_i, D_j$ con $i \le j$ la distanza fra questi usando la notazione:

$$d_{i,j} = \sum_{h=i+1}^{j} d_h$$

Deve valere che per ogni $j \in \{0 \dots k-1\}$ si ha $d_{i_j, i_{j+1}} \le d$, cioè non possiamo superare l’autonomia $d$ dell'auto a disposizione tra due distributori.
Quindi, il costo può essere espresso semplicemente come il numero di soste che effettuiamo ai vari distributori, ovvero definiamo il costo come $c(S) = k - 1$.

La scelta greedy è di riuscire ad arrivare al distributore più lontano con l’autonomia che abbiamo a disposizione.
Ovvero, se ci troviamo al distributore $D_i$ allora vogliamo arrivare al distributore $D_k$ più lontano, ovvero vogliamo trovare $k = \max\{j \mid d_{i,j} \le d\}$, che è la distanza massima che possiamo percorrere senza finire l’autonomia dell’auto.

---

### i. Dimostrazione della proprietà della scelta greedy

Sia $S^{\ast}$ una soluzione ottima. Supponiamo che $D_x$ sia la prima sosta effettuata partendo da $D_0 = A$.
Sia $D_k$ il distributore che contiene la nostra scelta greedy, ovvero il distributore più lontano raggiungibile, quindi con $k \ge x$.

- Se $x = k$ allora abbiamo finito.
- Altrimenti, se $x < k$, costruiamo una nuova soluzione $S^{\prime}$ che non contiene il distributore $D_x$ ma anzi contiene la nostra scelta greedy, ovvero:

$$S^{\prime} = (S^{\ast} \setminus \{D_x\}) \cup \{D_k\}$$

La soluzione è ancora ammissibile poiché per definizione si ha che $d_{0,k} \le d$. Inoltre, ripartire da $D_k$ verso la sosta successiva è più vantaggioso rispetto a ripartire da $D_x$, essendoci spostati in avanti.
La soluzione rimane ottimale, perché abbiamo solo effettuato uno scambio di un distributore con un altro, e quindi la cardinalità resta invariata.

Ovvero, il costo (numero totale di soste) rimane uguale ($c(S^{\prime}) = c(S^{\ast})$). Quindi abbiamo dimostrato così la proprietà della scelta greedy.

---

### ii. Dimostrazione della proprietà di sottostruttura ottima

Supponiamo che $S^{\ast}$ sia una soluzione ottima per il problema $A \dots B$, e che la prima sosta effettuata sia al distributore $D_k$.
Quindi $S^* = \{D_k\} \cup S_{k,B}$ dove $S_{k,B}$ è soluzione per il problema $D_k \dots B$.

Supponiamo per assurdo che la tratta rimanente per arrivare da $D_k$ a $B$ non sia ottimale, ovvero che esista un sottoinsieme di soste $S_{k,B}^{\prime}$ che risolve il problema di arrivare da $D_k$ a $B$ usando un numero minore di soste.

Questo vorrebbe dire che se unissimo questa ipotetica soluzione con la prima sosta $D_k$ otterremmo una soluzione $S^{\prime}$ tale che:

$$S^{\prime} = S_{k,B}^{\prime} \cup \{D_k\}$$

con un numero minore di soste.
Ovvero tale che $\vert{}S^{\prime}\vert{} < \vert{}S^{\ast}\vert{}$, che è assurdo perché abbiamo definito $S^{\ast}$ come soluzione ottima per il problema con il minor numero di soste.

---

### iii. Pseudocodice

Un possibile pseudocodice per la procedura `stop(d, n)` prende in input l’array $d[1\dots n]$ delle distanze e restituisce l’insieme $S[1\dots n-1]$ dei distributori scelti a cui fermarsi.
*Nota: la prima e ultima sosta sono scelte sempre, quindi non serve indicarlo.*

```text
// assumendo d_max sia l'autonomia massima
stop(d, n)
    S = ∅
    dist = d[1]

    for i = 2 to n
        // se la distanza è troppo grande allora devo fermarmi
        if dist + d[i] > d_max
            S = S U {i - 1}
            dist = d[i]
        else
            dist = dist + d[i]		
```

---

### iv. Complessità

La complessità attesa sarà $\Theta(n)$ essendo una semplice scansione lineare dell'array delle distanze. La complessità spaziale è $\mathcal{O}(n)$ per memorizzare l'insieme $S$ delle soste effettuate.
