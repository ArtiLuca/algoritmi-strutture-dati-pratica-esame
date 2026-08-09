# Esercizi Tematici — Programmazione Dinamica e Greedy

[← Torna alla raccolta principale](../README.md)

Questa cartella raccoglie esercizi tematici su **Programmazione Dinamica** e
**Algoritmi Greedy**, due argomenti ricorrenti negli esercizi d'esame.

L'obiettivo è fare pratica mirata su problemi che richiedono di riconoscere una
struttura ottima e tradurla in una soluzione algoritmica completa, in stile
esame.

Per la **Programmazione Dinamica**, mi concentro soprattutto su:

1. sottostruttura ottima e caratterizzazione ricorsiva;
2. algoritmo bottom-up o top-down con memoization;
3. ricostruzione della soluzione ottima;
4. valutazione della complessità.

Per gli **Algoritmi Greedy**, mi concentro soprattutto su:

1. formalizzazione della soluzione e del costo;
2. proprietà della sottostruttura ottima;
3. individuazione di una scelta greedy sicura;
4. dimostrazione della proprietà di scelta greedy;
5. pseudocodice e complessità.

## Stato delle soluzioni

### Programmazione Dinamica

| Esercizio | Argomento principale | Stato |
|---|---|---|
| Esercizio 18 | Sottostringa palindroma di lunghezza massima | [Da completare](esercizio_18.md) |
| Esercizio 19 | Parentetizzazione ottima di un'espressione | [Da completare](esercizio_19.md) |
| Esercizio 20 | Shortest Common Supersequence (SCS) | [Completato](esercizio_20.md) |
| Esercizio 21 | Resto con numero minimo di banconote | [Completato](esercizio_21.md) |
| Esercizio 22 | Cammino di costo minimo in una griglia | [Completato](esercizio_22.md) |
| Esercizio 23 | Tragitto in treno di costo minimo (con cambi) | [Da completare](esercizio_23.md) |
| Esercizio 24 | Percorso tra stati con costo minimo dei visti | [Da completare](esercizio_24.md) |
| Esercizio 25 | Lunghezza esatta annodando pezzi di corda | [Da completare](esercizio_25.md) |
| Esercizio 26 | Allocazione massima di un'aula (attività) | [Da completare](esercizio_26.md) |
| Esercizio 27 | Attraversamento griglia con guadagno massimo | [Completato](esercizio_27.md) |
| Esercizio 28 | Longest Increasing Subsequence (LIS) | [Completato](esercizio_28.md) |
| Esercizio 29 | Edit Distance con costo variabile | [Da completare](esercizio_29.md) |
| Esercizio 30 | Knapsack bilanciato / coalizione di governo | [Da completare](esercizio_30.md) |
| Esercizio 31 | Sottosequenza palindroma di lunghezza massima | [Da completare](esercizio_31.md) |
| Esercizio 32 | Sottoarray contiguo di somma massima | [Completato](esercizio_32.md) |

### Greedy

| Esercizio | Argomento principale | Stato |
|---|---|---|
| Esercizio 33 | Soste minime ai distributori | [Da completare](esercizio_33.md) |
| Esercizio 34 | Turni minimi per coprire richieste | [Da completare](esercizio_34.md) |

---

## Testi degli Esercizi

### **Esercizio 18**
Dare un algoritmo per individuare, all'interno di una stringa $a_1 \dots a_n$, una sottostringa (di caratteri consecutivi) palindroma di lunghezza massima. Ad esempio, nella stringa "colonna" la sottostringa palindroma di lunghezza massima è "olo". Più precisamente:
- **i.** dare una caratterizzazione ricorsiva della lunghezza massima $l_{i,j}$ di una sottostringa palindroma di $a_i \dots a_j$;
- **ii.** tradurre tale definizione in un algoritmo (bottom up o top down con memoization) che determina la lunghezza massima;
- **iii.** trasformare l'algoritmo in modo che permetta anche di individuare la stringa, non solo la sua lunghezza;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 19**
Sia data un'espressione $\xi = x_1 op_1 x_2 op_2 \dots x_{n-1} op_{n-1} x_n$, con $n \ge 2$ dove ogni $x_i$ è un intero positivo e $op_i \in \{+, *\}$ di somma o di moltiplicazione (dati). Utilizzando la programmazione dinamica si determini una parentetizzazione dell'espressione che rende il valore dell'espressione minimo. Ad esempio, l'input `7 + 10 * 2` può essere parentetizzato come `((7 + 10) * 2) = 34` oppure come `(7 + (10 * 2)) = 27`. In questo caso, la parentetizzazione desiderata è quindi la seconda. Più precisamente:
- **i.** dare una caratterizzazione ricorsiva del valore minimo $v_{i,j}$ prodotto da una parentetizzazione della sottoespressione $x_i op_i \dots op_{j-1} x_j$;
- **ii.** tradurre tale definizione in un algoritmo (bottom up o top down con memoization) che determina il valore minimo;
- **iii.** trasformare l'algoritmo in modo che permetta anche di stampare l'espressione;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 20**
Si ricordi che data una sequenza $X = x_1 \dots x_k$ si indica con $X_i$ il prefisso $x_1 \dots x_i$. Una sottosequenza di $X$ è $x_{i_1} \dots x_{i_h}$ con $1 \le i_1 < i_2 < \dots < i_h \le k$, ovvero è una sequenza ottenuta da $X$ eliminando alcuni elementi. Quando $Y$ è sottosequenza di $X$ si scrive $Y \sqsubseteq X$.
Realizzare un algoritmo che, date due sequenze $X = x_1 \dots x_k$ e $Y = y_1 \dots y_h$ determina una *shortest common supersequence* (SCS) ovvero una sequenza $Z$, di lunghezza minima, tale che $Y \sqsubseteq Z$. Ad esempio, per $X$ = "abf" e $Y$ = "afgj" una SCS è "abfgj".
- **i.** dare una caratterizzazione ricorsiva della lunghezza $l_{i,j}$ di una SCS di $X_i$ e $Y_j$ e dedurne un algoritmo;
- **ii.** trasformare l'algoritmo in modo che fornisca una SCS di $X$ e $Y$;
- **iii.** valutare la complessità dell'algoritmo.

---

### **Esercizio 21**
Si supponga di dover pagare una certa somma $s$. Per farlo si hanno a disposizione le banconote $b_1, \dots, b_n$ ciascuna di valore $v_1, \dots, v_n$ (numeri naturali). Si vuole determinare, se esiste, un insieme di banconote $b_{i_1}, \dots, b_{i_k}$ che totalizzi esattamente la somma richiesta e che minimizzi il numero $k$ di banconote utilizzate.
- **i.** mostrare che vale la proprietà della sottostruttura ottima e fornire una caratterizzazione ricorsiva del costo $c(s',j)$ della soluzione ottima per il sottoproblema di dare una somma pari a $s'$ con le banconote in $b_1, \dots, b_j$, con $j \le n$;
- **ii.** tradurre tale definizione in un algoritmo (bottom up o top down con memoization) che determina il costo della soluzione ottima;
- **iii.** trasformare l'algoritmo in modo che permetta anche di individuare la soluzione, non solo il suo costo;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 22**
Si supponga di avere una scacchiera $n \times n$. Si vuole spostare un pezzo dall'angolo in basso a sinistra $(1,1)$ a quello in alto a destra $(n,n)$. Il pezzo può muoversi di una casella verso l'alto o verso destra. Un passo dalla casella $(i,j)$ ha un costo $u(i,j)$ se verso l'alto e $r(i,j)$ se verso destra. Realizzare un algoritmo `MinPath(u,r,n)` che dati in input gli array `u[1..n, 1..n]` e `r[1..n, 1..n]` dei costi dei singoli passi fornisce il cammino minimo. Più in dettaglio:
- **i.** fornire una caratterizzazione ricorsiva del costo minimo di un cammino $c(i,j)$ per andare dalla casella $(i,j)$ alla casella $(n,n)$;
- **ii.** tradurre tale definizione in un algoritmo `MinPath(u,r,n)` (bottom up o top down con memoization) che determina il costo di un cammino minimo da $(1,1)$ a $(n,n)$;
- **iii.** trasformare l'algoritmo in modo che stampi la sequenza di passi di costo minimo;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 23**
Sia data una sequenza di città $c_1, c_2, \dots, c_n$ collegate da un percorso ferroviario. Da ciascuna città $c_i$ è possibile raggiungere $c_j$ con $i < j$ con un treno diretto. Sapendo che per $i, j \in \{1, \dots, n\}$, con $i < j$, il costo del biglietto del treno diretto da $c_i$ a $c_j$ risulta essere $b[i,j]$, determinare il costo minimo di un tragitto, con possibili cambi intermedi, da $c_1$ a $c_n$. Più in dettaglio:
- **i.** fornire una caratterizzazione ricorsiva del costo minimo $min[i]$ di un tragitto dalla città $c_i$ alla città $c_n$;
- **ii.** tradurre tale definizione in un algoritmo `MinTrain(b,n)` (bottom up o top down con memoization) che determina il costo di un tragitto di costo minimo dalla città $c_1$ alla città $c_n$;
- **iii.** trasformare l'algoritmo di modo che determini anche la sequenza dei cambi necessari per ottenere il tragitto di costo minimo, privilegiando - a parità di costo - soluzioni che minimizzano il numero dei cambi;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 24**
Si supponga che il mondo consista di $n$ stati $S_1, \dots, S_n$ e che spostarsi dallo stato $S_i$ allo stato $S_j$ imponga l'ottenimento di un visto di ingresso che ha un costo $v_{i,j}$, maggiore di 0. Realizzare un algoritmo che determini una sequenza di stati che conviene percorrere per andare dallo stato $S_1$ allo stato $S_n$ minimizzando il costo complessivo dei visti. Più precisamente:
- **i.** dare una caratterizzazione ricorsiva del costo complessivo minimo $v_i$ dei visti per andare dallo stato $S_i$ allo stato $S_n$;
- **ii.** usare la caratterizzazione al punto precedente per ottenere un algoritmo `ESP(v,n)` che dato l'array dei costi dei visti `v[1..n, 1..n]` determina il costo minimo dei visti per andare da $S_1$ a $S_n$;
- **iii.** trasformare l'algoritmo in modo che determini oltre al costo minimo anche la sequenza degli stati da attraversare per ottenerlo;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 25**
Un marinaio ha $n$ pezzi di corda di lunghezze intere $l_1, \dots, l_n$ ($l_i \ge 2$) e deve annodarli per ottenere una corda di lunghezza esattamente $d$. Tenendo conto che fare un nodo richiede una lunghezza pari ad 1 (ad es. se annodo due pezzi lunghi 5 e 7 la corda che ottengo è lunga 11), individuare, se esiste, un insieme minimo di pezzi che annodati producano una corda della lunghezza $d$ desiderata. Più precisamente:
- **i.** dare una caratterizzazione ricorsiva del numero minimo $m(i,d')$ di pezzi di corda scelti in $l_1, \dots, l_i$ che possono essere annodati per produrre la lunghezza $d'$ ($+\infty$ se non è possibile ottenere $d'$ con nessuna combinazione);
- **ii.** usare la caratterizzazione al punto precedente per ottenere un algoritmo `Rope(l,n,d)` che dato l'array delle lunghezze `l[1..n]` determina il numero minimo di pezzi da annodare per ottenere $d$ (se esiste);
- **iii.** trasformare l'algoritmo in modo che restituisca oltre al numero anche l'indicazione di quali pezzi usare;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 26**
Siano date $n$ attività $a_1, \dots, a_n$, che devono essere svolte in un'aula. Ogni attività ha tempo di inizio $s_i$ e tempo di fine $f_i$, con $s_i < f_i$. Si vuole trovare un sottoinsieme di attività che possano essere svolte nell'aula, quindi senza sovrapposizioni, e che massimizzi il tempo di utilizzo dell'aula.
Più precisamente, assumendo che le attività siano ordinate in modo crescente per tempo di fine:
- **i.** dare una caratterizzazione ricorsiva del tempo massimo $u(i,f)$ di utilizzo dell'aula, quando le attività da allocare siano $a_1, \dots, a_i$ e l'aula sia disponibile fino al tempo $f$ (ovvero nell'intervallo $[0, f)$);
- **ii.** usare la caratterizzazione al punto precedente per ottenere un algoritmo `allocate(s,f,n)` che dati gli array dei tempi di inizio e fine delle attività `s[1..n]` e `f[1..n]` determini il tempo di utilizzo massimo.

> **Suggerimento:** è utile osservare che nel calcolo di $u(i,f)$ i valori significativi di $f$ sono i tempi di inizio delle varie attività e quindi è possibile limitarsi a $u(i,j)$, ovvero tempo massimo di utilizzo dell'aula, con attività $a_1, \dots, a_i$, quando l'aula sia disponibile fino al tempo $s_j$.

- **iii.** trasformare l'algoritmo in modo che restituisca oltre al tempo anche l'indicazione di quali attività allocare;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 27**
Mario deve attraversare una griglia dall'alto verso il basso e per farlo, ad ogni passo salta verso il basso di una riga, spostandosi contestualmente a destra di quanto vuole. Ogni casella contiene una moneta di un certo valore (possibilmente negativo) per cui nell'attraversamento Mario totalizzerà un certo guadagno.
Supponendo che la griglia abbia dimensione $m \times n$ e che per $i \in \{1, \dots, m\}$ e $j \in \{1, \dots, n\}$ la casella $(i, j)$ contenga una moneta di valore $V[i,j]$, realizzare un algoritmo che identifica un attraversamento di valore massimo. Più precisamente:
- **i.** dare una caratterizzazione ricorsiva del guadagno massimo $G[i,j]$ di un attraversamento della sottogriglia $[i \dots m, j \dots n]$;
- **ii.** usare la caratterizzazione al punto precedente per ottenere un algoritmo `mario(V,m,n)` che dato l'array $V$ con il valore delle monete determini il guadagno massimo di un attraversamento;
- **iii.** trasformare l'algoritmo in modo che restituisca oltre al guadagno anche l'indicazione dell'attraversamento da seguire;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 28**
Data una sequenza di numeri $X = x_1 x_2 \dots x_n$ si vuole determinare una sottosequenza $x_{i_1} x_{i_2} \dots x_{i_k}$ di $X$, crescente, ovvero tale che $x_{i_1} \le x_{i_2} \le \dots \le x_{i_k}$ di lunghezza massima. Ad esempio, se $X = [77, 69, 70, 19, 71, 25, 52, 26, 28, 64]$, una sottosequenza crescente di lunghezza massima è $[19, 25, 26, 28, 64]$.
- **i.** fornire una caratterizzazione ricorsiva della lunghezza $l_i$ di una sottosequenza crescente di lunghezza massima che abbia come primo carattere $x_i$;
- **ii.** tradurre tale definizione in un algoritmo `LIS(X,n)` (bottom up o top down con memoization) che determina la lunghezza di una sottosequenza crescente di lunghezza massima della sequenza $X[1 \dots n]$;
- **iii.** trasformare l'algoritmo in modo che individui anche la sottosequenza, non solo la sua lunghezza;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 29**
Date due sequenze $X = x_1 \dots x_m$ e $Y = y_1 \dots y_n$ su di un alfabeto $\Sigma = \{a_1, \dots, a_l\}$ si definisce edit distance il costo minimo di un insieme di operazioni che trasforma la sequenza $X$ nella sequenza $Y$. Le operazioni possibili sono:
- **insert**, ovvero l'inserimento di un simbolo in qualche posizione in $X$ (costo 1);
- **delete**, ovvero la cancellazione di un simbolo in qualche posizione in $X$ (costo 1);
- **replace**, ovvero la sostituzione di un simbolo in qualche posizione in $X$, con costo che dipende dai simboli coinvolti: sostituire il simbolo $a$ con il simbolo $b$, con $a \ne b$ ha un costo $c(a,b) > 0$. Ad esempio per trasformare "gesto" in "gelo" posso fare una replace $s \rightarrow l$ e una delete di $t$ con costo $c(s,l)+1$, oppure una delete di $s$ e una replace $t \rightarrow l$ con costo $1+c(t,l)$, ecc.

Fornire un algoritmo di programmazione dinamica che dati $X$, $Y$ e la funzione $c$ dei costi di replace (per $a, b \in \Sigma$, $c(a,b)$ è il costo dell'operazione $a \rightarrow b$) calcola la edit distance tra $X$ e $Y$. In dettaglio:
- **i.** indicata con $e(i,j)$ la edit distance tra $X^i = x_1 \dots x_i$ e $Y^j = y_1 \dots y_j$, con $i \in \{0, \dots, m\}$ e $j \in \{0, \dots, n\}$, darne una caratterizzazione ricorsiva;
- **ii.** tradurre tale definizione in un algoritmo (bottom up o top down con memoization) che determina l'edit distance;
- **iii.** trasformare l'algoritmo in modo che fornisca anche le operazioni di edit che trasformano $X$ in $Y$ con costo minimo;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 30**
Nello stato di Frattalia, si è appena insediato il nuovo governo, sostenuto da due partiti, Arancio e Cobalto. La coalizione Arancio-Cobalto ha sottoscritto un contratto di governo che prevede diversi punti, alcuni proposti dagli Arancio altri dai Cobalto. Tuttavia ogni punto ha un costo economico, così che non è possibile realizzarli tutti: il debito pubblico non può oltrepassare una certa soglia. Occorre quindi scegliere un sottoinsieme di punti da realizzare e tale insieme deve essere bilanciato, ovvero devono essere scelti in egual numero punti degli Arancio e dei Cobalto.
Si supponga che i punti proposti dal partito Arancio siano $n$ con costi $a_1, \dots, a_n$ e analogamente i punti proposti dai Cobalto siano $m$ con costi $c_1, \dots, c_m$. Fornire un algoritmo di programmazione dinamica che individui un sottoinsieme bilanciato dei punti del contratto, di dimensione massima e tale che la somma dei costi non oltrepassi un limite fissato $d$. Più precisamente:
- **i.** dare una caratterizzazione ricorsiva della cardinalità massima $p_{i,j,d}$ di un insieme bilanciato di punti di programma scelti in $a_1, \dots, a_i, c_1, \dots, c_j$ con costo $\le d$;
- **ii.** tradurre tale definizione in un algoritmo (bottom up o top down con memoization) che determina il numero massimo;
- **iii.** trasformare l'algoritmo in modo che fornisca anche i punti del contratto scelti, non solo il loro numero;
- **iv.** valutare la complessità dell'algoritmo. Esiste la possibilità di applicare un algoritmo greedy?

---

### **Esercizio 31**
Dare un algoritmo per individuare, all'interno di una stringa $a_1 \dots a_n$ una sottosequenza (quindi una sequenza di caratteri possibilmente non consecutivi) palindroma di lunghezza massima. Ad esempio, nella stringa "corollario" la sottosequenza palindroma di lunghezza massima è "orllro". Più precisamente:
- **i.** dare una caratterizzazione ricorsiva della lunghezza massima $l_{i,j}$ di una sottosequenza palindroma di $a_i \dots a_j$;
- **ii.** tradurre tale definizione in un algoritmo (bottom up o top down con memoization) che determina la lunghezza massima;
- **iii.** trasformare l'algoritmo in modo che fornisca anche la sottosequenza, non solo la sua lunghezza;
- **iv.** valutare la complessità dell'algoritmo.

---

### **Esercizio 32**
Realizzare, con tecniche di programmazione dinamica, un algoritmo che dato un array $A[1 \dots n]$, non vuoto, trova un sottoarray non vuoto di somma massima, ovvero due indici $i$ e $j$ con $1 \le i \le j \le n$ tali che $A[i]+A[i+1]+\dots+A[j]$ sia massima. Ad esempio per `[-10, 4, 1, -1, 2, -1]` il sottoarray di somma massima è `[4, 1, -1, 2]`. Più precisamente:
- **i.** indicato con $l_j$ la somma massima di un sottoarray di $A[1 \dots n]$ che termini con $A[j]$ (quindi del tipo $A[i \dots j]$), darne una caratterizzazione ricorsiva;
- **ii.** tradurre tale definizione in un algoritmo (bottom up o top down con memoization) che determina la somma massima;
- **iii.** trasformare l'algoritmo in modo che fornisca anche la sottostringa, non solo la sua somma;
- **iv.** valutare la complessità dell'algoritmo.

---

## Esercizi Greedy

### **Esercizio 33**

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

### **Esercizio 34**

L'ufficio postale offre un servizio di ritiro pacchi in sede su prenotazione.

Il destinatario, avvisato della presenza del pacco, deve comunicare l'orario
preciso al quale si recherà allo sportello.

Sapendo che gli impiegati dedicano a questa mansione turni di un'ora, con inizio
in un momento qualsiasi, si chiede di scrivere un algoritmo che individui
l'insieme minimo di turni di un'ora sufficienti a soddisfare tutte le richieste.

Più in dettaglio, data una sequenza di richieste:

```math
\vec r = r_1, \dots, r_n,
```

dove `r_i` è l'orario della `i`-ma prenotazione, si vuole determinare una
sequenza di turni:

```math
\vec t = t_1, \dots, t_k,
```

con `t_j` orario di inizio del `j`-mo turno, che abbia dimensione minima e tale
che i turni coprano tutte le richieste.

- **i.** Formalizzare la nozione di soluzione per il problema e il relativo
  costo. Mostrare che vale la proprietà della sottostruttura ottima e
  individuare una scelta che gode della proprietà della scelta greedy.
- **ii.** Sulla base della scelta greedy individuata al passo precedente,
  fornire un algoritmo greedy `time(R,n)` che dato in input l'array delle
  richieste `r[1..n]` restituisce una soluzione ottima.
- **iii.** Valutare la complessità dell'algoritmo.
