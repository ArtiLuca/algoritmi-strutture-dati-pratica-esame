# Hashing & Huffman & Altro

[← Torna agli esercizi tematici](../README.md) · [Torna alla raccolta principale](../../README.md)

Questa cartella raccoglie esercizi su tabelle hash (indirizzamento aperto e chaining), costruzione di codici prefissi ottimi (algoritmo di Huffman), analisi ammortizzata di strutture dati e algoritmi greedy.

Gli esercizi sono pensati per allenarsi sulla parte teorica e algoritmica dell'esame: simulare l'inserimento in tabelle hash con varie tecniche di risoluzione delle collisioni, tracciare l'albero di Huffman e dimostrare limiti di costo ammortizzato.

Ogni esercizio completato conterrà una soluzione in stile esame, con passaggi espliciti, simulazioni passo-passo e dimostrazioni formali.

---

## Stato delle soluzioni

| Esercizio | Stato |
|---|---|
| Domanda 31 — Tabella hash (doppio hash, $m=8$) | Da completare |
| Domanda 32 — Tabella hash (doppio hash, $m=8$) | [Completato](domanda_32.md) |
| Domanda 33 — Tabella hash (doppio hash, $m=8$) | Da completare |
| Domanda 34 — Tabella hash (chaining, $m=8$) | [Completato](domanda_34.md) |
| Domanda 35 — Tabella hash (doppio hash, $m=9$) | [Completato](domanda_35.md) |
| Domanda B Esame — Hashing con doppio hash | [Completato](domanda_esame_doppio_hashing.md) |
| Domanda Esame — Codice di Huffman (5 simboli, 5 punti) | Da completare |
| Domanda 40 — Codice di Huffman (7 simboli) | Da completare |
| Domanda 41 — Codice di Huffman (7 simboli) | Da completare |
| Domanda 42 — Codice di Huffman (7 simboli) | Da completare |
| Domanda 43 — Codice di Huffman (7 simboli) | Da completare |
| Domanda 44 — Codice di Huffman (7 simboli) | Da completare |
| Domanda 45 — Codice di Huffman (7 simboli) | Da completare |
| Domanda 46 — Codice di Huffman (7 simboli) | Da completare |
| Esercizio Huffman Esame A | [Completato](domanda_esame_huffman_A.md) |
| Esercizio Huffman Esame B | [Completato](domanda_esame_huffman_B.md) |
| Esercizio 35 — Struttura dati (Half min, ammortizzata) | Da completare |
| Esercizio 36 — OrderedStack (ammortizzata) | Da completare |
| Esercizio 37 — Struttura dati (Half max, ammortizzata) | Da completare |
| Esercizio — Assegnamento frequenze Huffman (9 punti) | Da completare |
| Esercizio — Matching sulla linea (Greedy) | Da completare |

---

## Testi degli Esercizi

### **Domanda 31**

Si consideri una tabella hash di dimensione $m = 8$, e indirizzamento aperto con doppio hash basato sulle funzioni $h_1(k) = k \bmod m$ e $h_2(k) = 1 + (k \bmod (m - 2))$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: 12, 3, 22, 14, 38.

---

### **Domanda 32**

Si consideri una tabella hash di dimensione $m = 8$, e indirizzamento aperto con doppio hash basato sulle funzioni $h_1(k) = k \bmod m$ e $h_2(k) = 1 + 2 \cdot (k \bmod (m - 3))$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: 34, 12, 18, 9, 42.

---

### **Domanda 33**

Si consideri una tabella hash di dimensione $m = 8$, e indirizzamento aperto con doppio hash basato sulle funzioni $h_1(k) = k \bmod m$ e $h_2(k) = 1 + (k \bmod (m - 2))$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: 14, 22, 10, 16, 8.

---

### **Domanda 34**

Si consideri una tabella hash di dimensione $m = 8$, gestita mediante chaining (liste di trabocco) con funzione di hash $h(k) = k \bmod m$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: 14, 10, 22, 18, 19.

---

### **Domanda 35**

Si consideri una tabella hash di dimensione $m = 9$, e indirizzamento aperto con doppio hash basato sulle funzioni $h_1(k) = k \bmod m$ e $h_2(k) = 1 + (k \bmod (m - 2))$. Si descriva in dettaglio come avviene l'inserimento della sequenza di chiavi: 12, 3, 22, 14, 38.

---

### Domanda B Esame — Hashing con doppio hash

Si consideri una tabella hash di dimensione $m=7$, e indirizzamento aperto con doppio hash basato sulle funzioni:
$h_1(k) = k \bmod m$ e $h_2(k) = 1 + k \bmod (m-2)$.
Si descriva sinteticamente come avviene l'inserimento degli elementi e si specifichi il risultato dell'inserzione della sequenza di chiavi: $10, 20, 34, 35, 48$.

Sarebbe appropriato lavorare con una tabella di dimensione $m=8$ e le stesse funzioni hash?

---

### **Domanda Esame — 5 punti**

Indicare, in forma di albero binario, il codice libero da prefissi ottenuto tramite l'algoritmo di Huffman per l'alfabeto $\{a,b,c,d,e\}$ supponendo che ogni carattere appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccc}
& a & b & c & d & e \\ 
\hline
\text{frequenza} & 12 & 10 & 13 & 57 & 8
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### **Domanda 40**

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffmann per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\ 
\hline
\text{frequenza} & 16 & 12 & 2 & 8 & 3 & 9 & 6
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### **Domanda 41**

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffmann per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\ 
\hline
\text{frequenza} & 5 & 9 & 3 & 3 & 1 & 1 & 6
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### **Domanda 42**

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffmann per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\ 
\hline
\text{frequenza} & 6 & 21 & 12 & 8 & 3 & 23 & 8
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### **Domanda 43**

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffmann per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\ 
\hline
\text{frequenza} & 37 & 4 & 12 & 6 & 9 & 17 & 8
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### **Domanda 44**

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffmann per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\ 
\hline
\text{frequenza} & 10 & 6 & 2 & 8 & 19 & 31 & 15
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### **Domanda 45**

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffmann per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\ 
\hline
\text{frequenza} & 3 & 8 & 7 & 12 & 6 & 23 & 21
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### **Domanda 46**

Indicare il codice prefisso ottenuto utilizzando l’algoritmo di Huffmann per l’alfabeto $\{a, b, c, d, e, f, g\}$, supponendo che ogni simbolo appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccccc}
& a & b & c & d & e & f & g \\ 
\hline
\text{frequenza} & 2 & 12 & 16 & 8 & 6 & 9 & 3
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### Domanda Esame A — 5 punti

Indicare, in forma di albero binario, il codice libero da prefissi ottenuto tramite l'algoritmo di Huffman per l'alfabeto $\{a,b,c,d,e\}$ supponendo che ogni carattere appaia con le seguenti frequenze:

$$
\begin{array}{c|ccccc}
& a & b & c & d & e \\ 
\hline
\text{frequenza} & 12 & 10 & 13 & 57 & 8
\end{array}
$$

Spiegare il processo di costruzione del codice.

---

### Domanda Esame B — 5 punti

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

### **Esercizio 35**

Progettare una struttura dati per la gestione di un insieme dinamico di interi, con operazioni

* `New(S)` crea un insieme vuoto;
* `Ins(S, x)` inserisce l'elemento $x$ nell'insieme S;
* `Half(S)` cancella da S i $\lceil|S|/2\rceil$ elementi più piccoli.

Si richiede che una qualsiasi sequenza di $n$ operazioni venga eseguita in tempo $\mathcal{O}(n \log n)$.

i. Specificare le strutture dati di supporto utili e lo pseudo-codice delle operazioni suddette (questo può ridursi ad una chiamata di un'operazione della struttura scelta).
ii. Dimostrare, mediante un'analisi ammortizzata della complessità, che una sequenza di $n$ operazioni costa $\mathcal{O}(n \log n)$.

---

### **Esercizio 36**

Si consideri una struttura che chiamiamo `OrderedStack` con le seguenti operazioni:

* `OEmpty(S)`: Ritorna un booleano che dice se la struttura è vuota
* `OPop(S)`: Estrae l'ultimo elemento inserito
* `OTop(S)`: Ritorna il valore dell'ultimo elemento inserito
* `OPush(S, x)`: Inserisce nello stack $x$, eliminando prima ogni elemento che sia maggiore di $x$.

Utilizzando una struttura dati stack, fornire una implementazione della suddetta struttura ovvero

i. Specificare come è definita la struttura dati e fornire lo pseudocodice dei metodi elencati.
ii. Mostrare che una sequenza di $n$ operazioni, a partire da struttura vuota, ha costo ammortizzato $\mathcal{O}(n)$ (e quindi ogni singola operazione ha costo ammortizzato $\mathcal{O}(1)$).

---

### **Esercizio 37**

Progettare una struttura dati per la gestione di un insieme dinamico di interi, con operazioni

* `New(S)` crea un insieme vuoto;
* `Ins(S, x)` inserisce l'elemento $x$ nell'insieme S;
* `Half(S)` cancella da S i $\lceil|S|/2\rceil$ elementi più grandi.

Si richiede che una qualsiasi sequenza di $n$ operazioni venga eseguita in tempo $\mathcal{O}(n \log n)$.

i. Specificare le strutture dati di supporto utili e lo pseudo-codice delle operazioni suddette (questo può ridursi ad una chiamata di un'operazione della struttura scelta).
ii. Dimostrare, mediante un'analisi ammortizzata della complessità, che una sequenza di $n$ operazioni costa $\mathcal{O}(n \log n)$.

---

### **Esercizio — 9 punti**

Si consideri un file definito sull'alfabeto $\{a,b,c\}$ con frequenze $f(a),\ f(b),\ f(c)$.
Per ognuna delle seguenti codifiche determinare, se esiste, un opportuno assegnamento di valori alle $3$ frequenze per cui l'algoritmo di Huffman restituisca tale codifica, oppure argomentare che tale codifica non è mai ottenibile.

1. $e(a)=0,\qquad e(b)=10,\qquad e(c)=11$
2. $e(a)=1,\qquad e(b)=0,\qquad e(c)=11$
3. $e(a)=10,\qquad e(b)=01,\qquad e(c)=00$

---

### **Esercizio — Matching sulla linea**

Sia $S=\{s_1,s_2,\ldots,s_n\}$ un insieme di punti ordinati sulla linea reale, che rappresentano dei server.
Sia $C=\{c_1,c_2,\ldots,c_n\}$ un insieme di punti ordinati sulla linea reale, che rappresentano dei client.

Il costo di assegnare un client $c_i$ ad un server $s_j$ è $|c_i-s_j|$.

Fornire un algoritmo greedy che assegna ("match") ogni client ad un server distinto e che minimizzi il costo totale (equiv., medio) dell'assegnamento.
Per casa: dimostrare l'ottimalità dell'algoritmo.
