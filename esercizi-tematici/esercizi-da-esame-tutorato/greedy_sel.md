# Domanda Greedy-Sel

**(a) Definire il problema.**
**(b) Descrivere brevemente l'algoritmo ottimo GREEDY-SEL visto in classe.**
**(c) Fornire un esempio di algoritmo greedy non ottimo, motivandone la non ottimalità.**

---

### (a) Definizione del problema

Il problema della selezione di attività compatibili consiste nel trovare un insieme di attività $S = \{a_i : 1 \le i \le n\}$ mutualmente compatibili di cardinalità massima, dove una attività è definita dall'intervallo $a_i = [s_i, f_i)$ con $0 \le s_i < f_i$.

Diciamo che due attività $a_i$ e $a_j$ sono compatibili se e solo se i loro intervalli non si sovrappongono, ovvero $[s_i, f_i) \cap [s_j, f_j) = \emptyset$. Matematicamente, questo significa che $f_i \le s_j$ oppure $f_j \le s_i$.
Per semplicità, possiamo assumere che le attività siano fornite già ordinate per tempo di fine crescente, ovvero:

$$
0 < f_1 \le f_2 \le \dots \le f_n
$$

Indichiamo con $S_{ij}$ lo spazio dei sottoproblemi, che indica l’insieme delle attività $a_k$ che sono temporalmente compatibili sia con l’attività $a_i$ sia con l’attività $a_j$:

$$
S_{ij} = \{a_k : f_i \le s_k < f_k \le s_j\}
$$

Ovvero, si tratta di quelle attività che iniziano dopo (o nel momento esatto in cui) finisce l’attività $a_i$ (cioè $f_i \le s_k$) e contemporaneamente finiscono prima (o nel momento esatto in cui) inizia l’attività $a_j$ (cioè $f_k \le s_j$).

---

### (b) Algoritmo ottimo GREEDY-SEL

L’algoritmo `GREEDY-SEL` visto a lezione implementa la scelta greedy di selezionare sempre l’attività che finisce per prima tra quelle ancora compatibili con le attività già selezionate.

Visto che assumiamo le attività già ordinate per tempo di fine crescente, all’inizio si sceglie semplicemente $a_1$, quindi $A = \{a_1\}$.
Dopodiché, l'algoritmo scorre tutte le attività $a_m$ con $m = 2 \dots n$, tenendo traccia dell’indice dell’ultima attività scelta. Si aggiunge un’attività alla soluzione solo se questa inizia dopo (o nel momento esatto in cui) finisce l’ultima attività selezionata, ovvero se $s_m \ge f_{\text{last}}$, e in quel caso si aggiorna l’indice dell’ultima attività selezionata.

La correttezza dell'algoritmo si basa sul fatto che esiste sempre una soluzione ottima che contiene l'attività compatibile che termina per prima; dopo averla scelta, il problema residuo mantiene la stessa struttura.

Lo pseudocodice visto a lezione è il seguente:

```algorithmic
// s, f vettori di tempo di inizio/fine
GREEDY_SEL(s, f)
    A = {a_1}
    last = 1 // indice dell'ultima attivita selezionata

    for m = 2 to n
        if s_m >= f_last
            A = A U {a_m}
            last = m

    return A
```

> **Complessità:** Assumendo che le attività siano già ordinate per tempo di fine, l'algoritmo effettua una singola passata lineare, risultando in una complessità $\Theta(n)$. Se invece le attività non fossero già ordinate, bisognerebbe prima ordinarle per tempo di fine, con costo $\Theta(n\log n)$.

---

### (c) Esempio di algoritmo greedy non ottimo

Un esempio di algoritmo greedy non ottimale sarebbe implementare come scelta greedy l'attività di **durata minore** (ovvero minimizzare $f_i - s_i$).

Infatti, consideriamo le seguenti tre attività (ordinate per tempo di fine crescente):
- $a_1 = [1, 11)$
- $a_2 = [10, 13)$
- $a_3 = [12, 20)$

La scelta dell'attività di durata minore selezionerebbe per prima $a_2$ (che ha durata 3). Tuttavia, l'attività $a_2$ si sovrappone temporalmente sia ad $a_1$ che ad $a_3$, impedendo ulteriori scelte. Questo risulterebbe in una soluzione $A = \{a_2\}$ di cardinalità 1.
Una soluzione ottimale, invece, avrebbe evitato $a_2$ per selezionare $A = \{a_1, a_3\}$, ottenendo la cardinalità massima di 2.

Altri esempi di scelte greedy non ottimali sarebbero scegliere l'attività che inizia per prima, quella che finisce per ultima, oppure l'attività con il minor numero di sovrapposizioni.
