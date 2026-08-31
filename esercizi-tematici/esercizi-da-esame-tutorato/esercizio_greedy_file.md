# Esercizio 2 — Greedy con Argomento di Scambio

Si hanno $n$ file memorizzati in sequenza. Il file $i$ ha dimensione $s_i > 0$ e probabilità di accesso $p_i > 0$.

Dato un ordine $\sigma$, il costo atteso di accesso è:

$\sum_i p_i C_i(\sigma)$,

dove $C_i(\sigma)$ è la somma delle dimensioni dei file che precedono il file $i$ nell'ordine, più la dimensione del file $i$ stesso.

Trovare un ordinamento dei file che minimizzi il costo atteso.
Fornire la regola greedy, una dimostrazione tramite scambio di elementi adiacenti e la complessità.

---

### i. Regola Greedy

La regola greedy ottimale consiste nell'ordinare i file in senso decrescente in base al rapporto tra probabilità di accesso e dimensione. Ovvero, per ogni coppia di file $i$ e $j$, $f_i$ precede $f_j$ se:

$$
\frac{p_i}{s_i} \ge \frac{p_j}{s_j} \implies p_i s_j \ge p_j s_i
$$

*(A parità di rapporto, l'ordine è ininfluente).*

---

### ii. Dimostrazione (Argomento di Scambio)

Dimostriamo la correttezza della scelta greedy tramite un argomento di scambio.
Supponiamo per assurdo che esista una soluzione ottima $\sigma^*$ che *non* rispetta la nostra regola greedy. Questo significa che in $\sigma^*$ deve esistere almeno una coppia di file adiacenti in cui un file $f_j$ precede un file $f_i$ contravvenendo alla regola, ovvero tale che $\frac{p_i}{s_i} > \frac{p_j}{s_j}$ (che implica $p_i s_j - p_j s_i > 0$).

Sia $W$ la somma delle dimensioni di tutti i file che precedono la coppia $(f_j, f_i)$ in $\sigma^*$.
Il costo atteso relativo a questi due soli file nell'ordine di $\sigma^*$ (prima $f_j$, poi $f_i$) è:

$$
\text{Costo}(\sigma^*) = p_j(W + s_j) + p_i(W + s_j + s_i)
$$

Costruiamo ora un nuovo ordine $\sigma'$ ottenuto semplicemente **scambiando** $f_j$ e $f_i$ (mettendoli nell'ordine greedy, prima $f_i$ poi $f_j$), lasciando inalterato il resto dei file.
Il costo atteso per questa coppia in $\sigma'$ diventa:

$$
\text{Costo}(\sigma') = p_i(W + s_i) + p_j(W + s_i + s_j)
$$

Confrontiamo i due costi calcolando la differenza $\text{Costo}(\sigma^*) - \text{Costo}(\sigma')$:

$$
[p_j W + p_j s_j + p_i W + p_i s_j + p_i s_i] - [p_i W + p_i s_i + p_j W + p_j s_i + p_j s_j]
$$

Eliminando i termini comuni ($p_j W$, $p_j s_j$, $p_i W$, $p_i s_i$) otteniamo:

$$
\text{Costo}(\sigma^*) - \text{Costo}(\sigma') = p_i s_j - p_j s_i
$$

Per la nostra ipotesi iniziale sui due file scambiati, sappiamo che $p_i s_j - p_j s_i > 0$.
Di conseguenza, 

$$
\text{Costo}(\sigma^{\ast}) - \text{Costo}(\sigma^{\prime}) > 0 \implies \text{Costo}(\sigma^{\prime}) < \text{Costo}(\sigma^{\ast})
$$

Ma questo è un assurdo! Abbiamo appena trovato un ordine $\sigma'$ che ha un costo strettamente inferiore a $\sigma^*$, contraddicendo l'ottimalità di $\sigma^*$.
Quindi, una soluzione ottima non può contenere "inversioni" rispetto alla regola greedy. Possiamo perciò concludere che l'ordinamento prodotto dalla regola greedy è sempre globalmente ottimo.

---

### iii. Complessità

Per calcolare l'ordinamento ottimale, è sufficiente calcolare il rapporto $\frac{p_i}{s_i}$ per ciascuno degli $n$ file, operazione che richiede tempo $\mathcal{O}(n)$, e successivamente ordinare l'array in base a questo valore.
Utilizzando un algoritmo di ordinamento efficiente basato su confronti (come Merge Sort o Heap Sort), la complessità temporale totale risulta essere:

$$
T(n) = \mathcal{O}(n \log n)
$$
