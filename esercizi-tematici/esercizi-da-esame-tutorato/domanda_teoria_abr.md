# Domanda B — Alberi binari di ricerca

Dare la definizione di albero binario di ricerca.
Specificare l'albero ottenuto inserendo, con la procedura vista a lezione, a partire da un albero vuoto, i nodi aventi le seguenti chiavi: $10, 5, 3, 15, 7, 12$.
Si supponga che dall'albero così ottenuto si cancelli il nodo con chiave `5` e si indichi l'albero ottenuto.
Sia per gli inserimenti che per la cancellazione, motivare sinteticamente il risultato ottenuto.

---

### i. Definizione di Albero Binario di Ricerca (ABR)

Un albero binario di ricerca $T$ è un albero binario le cui chiavi sono mantenute ordinate in modo da soddisfare una specifica proprietà (non locale). Assumendo che ogni nodo $x$ abbia i campi $x.key$, $x.left$, $x.right$, $x.p$, per ogni nodo $x$ di $T$ vale che:
- $\forall y$ appartenente al sottoalbero sinistro radicato in $x$, si ha $y.key \le x.key$.
- $\forall y$ appartenente al sottoalbero destro radicato in $x$, si ha $y.key \ge x.key$.

---

### ii. Processo di Inserimento

L’inserimento avviene "simulando" una ricerca della chiave da inserire per individuare la sua posizione corretta. Partendo dalla radice, finché il nodo corrente non è `nil`, ci si sposta a sinistra se la chiave da inserire è minore del nodo corrente, oppure a destra se è maggiore o uguale, mantenendo traccia del genitore.
Raggiunto un puntatore `nil`, la nuova chiave viene inserita come foglia (figlio sinistro o destro) dell'ultimo genitore attraversato.

Processo di inserimento per le chiavi fornite:
- **10**: albero vuoto, viene inserito alla radice ($T.root$).
- **5**: $5 \le 10$, inserito come figlio sinistro di $10$.
- **3**: $3 \le 10 \implies 3 \le 5$, inserito come figlio sinistro di $5$.
- **15**: $15 \ge 10$, inserito come figlio destro di $10$.
- **7**: $7 \le 10 \implies 7 \ge 5$, inserito come figlio destro di $5$.
- **12**: $12 \ge 10 \implies 12 \le 15$, inserito come figlio sinistro di $15$.

L’albero risultante dopo tutti gli inserimenti è il seguente:

```text
            10
           /  \
          5    15
         / \   /
        3   7 12
```

---

### iii. Processo di Cancellazione

Vogliamo eliminare il nodo con chiave $5$. Notiamo che il nodo $5$ ha due figli (il sottoalbero sinistro radicato in $3$ e il sottoalbero destro radicato in $7$).
Secondo la procedura standard di cancellazione, un nodo con due figli viene sostituito dal suo **successore** (il minimo del suo sottoalbero destro).

In questo caso, il sottoalbero destro di $5$ è composto solo dal nodo $7$. Quindi il successore è esattamente $7$. Essendo $7$ il figlio destro diretto di $5$, la procedura di trapianto (`Transplant`) sostituisce il nodo $5$ con il nodo $7$. Infine, il sottoalbero sinistro originario di $5$ (il nodo $3$) viene agganciato come nuovo figlio sinistro di $7$.

L'albero risultante dopo la cancellazione è il seguente:

```text
            10
           /  \
          7    15
         /     /
        3     12
```
