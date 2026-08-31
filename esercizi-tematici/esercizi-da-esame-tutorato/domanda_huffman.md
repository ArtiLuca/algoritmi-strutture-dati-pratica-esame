# Esercizio — 9 punti

Si consideri un file definito sull'alfabeto $\{a, b, c\}$ con frequenze $f(a), f(b), f(c)$.
Per ognuna delle seguenti codifiche determinare, se esiste, un opportuno assegnamento di valori alle $3$ frequenze per cui l'algoritmo di Huffman restituisca tale codifica, oppure argomentare che tale codifica non è mai ottenibile.

1. $e(a)=0,\qquad e(b)=10,\qquad e(c)=11$
2. $e(a)=1,\qquad e(b)=0,\qquad e(c)=11$
3. $e(a)=10,\qquad e(b)=01,\qquad e(c)=00$

---

### Analisi e Soluzioni

Disegniamo i tre alberi binari corrispondenti a ciascuna delle codifiche. Utilizziamo la convenzione standard di etichettare con $0$ l'arco quando si scende a sinistra e con $1$ quando si scende a destra.

#### Caso 1: $e(a)=0,\ e(b)=10,\ e(c)=11$

**Albero generato:**

```text
           •
          / \
       a:0   •
            / \
         b:10 c:11  	   
```

**Risposta:**
Questa codifica **può essere** l'output dell'algoritmo di Huffman.
Affinché i nodi $b$ e $c$ vengano fusi per primi in un nodo interno, le loro frequenze devono essere le due più piccole dell'insieme. Una possibile assegnazione valida di frequenze che rispetta la condizione $f(b) \le f(c) < f(a)$ può essere:
$$f(b) = 25, \quad f(c) = 35, \quad f(a) = 45$$
In questo modo l'algoritmo unisce prima $25$ e $35$ (creando un nodo di peso $60$), e al passo successivo unisce questo nuovo nodo con $a$ ($45$), ottenendo la radice e l'albero mostrato.

---

#### Caso 2: $e(a)=1,\ e(b)=0,\ e(c)=11$

**Albero generato:**

```text
           •
          / \
       b:0  a:1
              \
             c:11   
```

**Risposta:**
Questa codifica **non è mai ottenibile** tramite l'algoritmo di Huffman.
Si può notare immediatamente che $e(a) = 1$ è un prefisso di $e(c) = 11$ (il nodo $a$ non è una foglia dell'albero, ma un nodo interno che ha $c$ come discendente). I codici generati da Huffman sono per definizione *codici liberi da prefissi* (tutti i simboli originali si devono trovare sulle foglie).

---

#### Caso 3: $e(a)=10,\ e(b)=01,\ e(c)=00$

**Albero generato:**

```text
               •
             /   \
            •     •
           / \   /  	 	
        c:00 b:01 a:10    
```

**Risposta:**
Questa codifica **non è mai ottenibile** tramite l'algoritmo di Huffman.
Come si evince dall'albero, il nodo interno di destra (raggiungibile con il bit $1$) possiede un solo figlio (il nodo $a$, a sinistra). Un albero di Huffman, per costruzione, genera sempre un **albero binario pieno** (ogni nodo interno ha esattamente due figli). Se un nodo interno avesse un solo figlio, la codifica non sarebbe ottima, poiché il bit extra potrebbe essere rimosso senza causare alcuna ambiguità nella decodifica (in questo caso $a$ potrebbe essere codificato semplicemente come $1$).
