# Esercizio 2 — Algoritmo greedy per il resto delle monete

Supponiamo di avere un numero illimitato di monete di ciascuno dei seguenti valori: $\{50, 20, 1\}$.
Dato un numero intero positivo $n$, l'obiettivo è selezionare il più piccolo numero di monete tale che il loro valore totale sia $n$.
Consideriamo l'algoritmo greedy che consiste nel selezionare ripetutamente la moneta di valore più grande possibile.

- **(a)** Fornire un valore di $n$ per cui l'algoritmo greedy non restituisce una soluzione ottima.
- **(b)** Supponiamo ora che i valori delle monete siano $\{10, 5, 1\}$. In questo caso l'algoritmo greedy restituisce sempre una soluzione ottima: dimostrare che ogni insieme ottimo $M^\star$ di monete di valore totale $n$ contiene la scelta greedy.

---

### (a) Controesempio per il sistema $\{50, 20, 1\}$

Scegliamo come target il valore $n = 60$.

Applicando l'algoritmo greedy (che sceglie sempre la moneta di taglio maggiore $\le n$), otterremmo la seguente sequenza di scelte:
1. Sceglie $50$ (resto $10$).
2. Sceglie dieci monete da $1$ per coprire il resto.

La soluzione greedy prodotta è $S_{greedy} = \{50, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1\}$, che ha cardinalità $|S_{greedy}| = 11$.

Tuttavia, esiste palesemente una soluzione ottima $S^\star = \{20, 20, 20\}$ che totalizza $60$ con cardinalità $|S^\star| = 3$.
Poiché $3 < 11$, l'algoritmo greedy non ha restituito una soluzione ottima.

---

### (b) Dimostrazione della proprietà di scelta greedy per $\{10, 5, 1\}$

Vogliamo dimostrare che, dato il set $V = \{10, 5, 1\}$, una soluzione ottima $M^\star$ per una somma $n$ contiene sempre la scelta greedy, ovvero la moneta $a_m \in V$ di valore massimo tale che $a_m \le n$.

Procediamo per **assurdo** tramite un argomento di scambio.
Sia $n > 1$ (se $n=1$, l'unica scelta possibile è $1$, che è banale). Supponiamo esista una soluzione ottima $M'$ che *non* contiene la scelta greedy $a_m$. Essendo $M'$ valida, totalizza comunque $n$ usando monete di taglio strettamente inferiore ad $a_m$.
Analizziamo i casi possibili per $a_m$:

- **Caso 1: $n \ge 10 \implies a_m = 10$.**
Se $M'$ non contiene il $10$, usa solo monete da $5$ e da $1$. Affinché $M'$ sia ottima, non può contenere due monete da $5$ (perché potremmo scambiarle con una da $10$, riducendo il numero di monete da $2$ a $1$, contraddicendo l'ottimalità). Allo stesso modo, non può contenere cinque monete da $1$ (sostituibili con una da $5$).
Quindi, il massimo valore che $M'$ può totalizzare senza usare il $10$ e restando ottima è: $1 \times 5 + 4 \times 1 = 9$. Ma poiché $n \ge 10$, $M'$ non può raggiungere la somma $n$. **Contraddizione.**

- **Caso 2: $5 \le n < 10 \implies a_m = 5$.**
Se $M'$ non contiene il $5$, usa solo monete da $1$. Per essere ottima, non può contenere cinque monete da $1$ (sostituibili con una da $5$). Il massimo valore totalizzabile è quindi $4 \times 1 = 4$. Ma noi sappiamo che $n \ge 5$. **Contraddizione.**

- **Caso 3: $n < 5 \implies a_m = 1$.**
In questo caso il set a disposizione si riduce alla sola moneta da $1$, che deve necessariamente essere usata.

In ogni caso, l'assunzione che esista una soluzione ottima $M'$ priva della scelta greedy porta a una contraddizione (o fallisce nel raggiungere la somma, o può essere ottimizzata tramite uno scambio che ne riduce la cardinalità).
Di conseguenza, abbiamo dimostrato che ogni insieme ottimo $M^\star$ di monete per il sistema $\{10, 5, 1\}$ deve obbligatoriamente contenere la scelta greedy iniziale.
