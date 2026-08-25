# Esercizio 1 — Split con divide et impera

Sia dato un array $V[1..n]$ i cui valori rappresentano la variazione giornaliera del valore di un titolo azionario.

È noto che il titolo è stato prima in perdita, con valori sempre negativi, poi ha iniziato a oscillare in giorni consecutivi tra valori positivi e negativi, e infine si è stabilizzato su valori positivi. Dunque nella sequenza **non possono esserci due giorni positivi seguiti da un negativo**.

Realizzare un algoritmo divide et impera `Split(V)` che individua il giorno in cui il titolo ha iniziato a essere stabile su valori positivi, ovvero il minimo indice

$$
i \in [1,n]
$$

tale che

$$
\forall j \ge i,\quad V[j] > 0.
$$

Se il titolo non si stabilizza su valori positivi, ritornare `0`.

Esempi:

- per $V=[-1,-2,2,-1,6,3]$ si deve ritornare $5$;
- per $V=[-1,-2,2,-1,6,-3]$ si deve ritornare `0`.

Fornire lo pseudocodice di `Split(V)`, motivarne la correttezza e individuarne la complessità. Si assuma che non ci siano valori nulli.

---

### i. Idea e Predicato Logico

Dato $V[1\dots n]$, vogliamo verificare se esiste un indice stabile, ovvero il minimo indice $i \in [1\dots n]$ tale che $\forall j \ge i$ vale $V[j] > 0$.
Assumendo che tale indice stabile esista, possiamo visualizzare l’array $V[1\dots n]$ diviso concettualmente in due parti:
1. Una prima metà $V[1\dots i-1]$ che contiene valori interamente negativi oppure valori consecutivi alternanti tra negativi e positivi.
2. Una seconda metà stabile $V[i\dots n]$ che contiene esclusivamente valori positivi.

Per via del vincolo del problema ("non ci possono essere due giorni positivi seguiti da un negativo"), sappiamo che appena incontriamo due giorni positivi consecutivi (oppure un giorno positivo che è anche l'ultimo dell'array), abbiamo la certezza matematica di trovarci nella zona stabile. Possiamo dunque definire il seguente predicato $P(q)$:

$$
P(q) \iff V[q] > 0 \land (q == n \lor V[q+1] > 0)
$$

Possiamo quindi operare in maniera *divide et impera* sul sottoarray $V[p\dots r]$, calcolando l’indice centrale $q$ e verificando se vale $P(q)$. Utilizzo la funzione `Split(V)` come semplice “wrapper” che invoca la procedura ricorsiva `SplitRec(V, p, r, n)`.

---

### ii. Pseudocodice

```text
// Driver
Split(V)
    n = V.length
    return SplitRec(V, 1, n, n)

// Procedura ricorsiva
SplitRec(V, p, r, n)

    // caso base: la ricerca ha esaurito lo spazio senza successo
    if p > r		
        return 0

    // calcolo indice centrale
    q = floor((p + r) / 2)

    // verifico se vale il predicato P(q)
    if (V[q] > 0) and (q == n or V[q+1] > 0)
        // Se abbiamo trovato un candidato valido, ricorriamo a sinistra
        // per vedere se esiste un indice stabile antecedente a q
        first = SplitRec(V, p, q - 1, n)

        if first == 0
            return q       // q è effettivamente il primo
        else
            return first   // c'è un indice stabile precedente

    else
        // Non vale P(q), siamo ancora nella zona negativa/oscillante.
        // L'indice stabile deve per forza trovarsi a destra di q.
        return SplitRec(V, q + 1, r, n)								
```

---

### iii. Dimostrazione di Correttezza

Utilizziamo il predicato $P(q)$ precedentemente definito. Sia $k$ l’indice del primo giorno stabile cercato (se esiste).
Sappiamo che $\forall q < k$, $P(q)$ è falso poiché ci troviamo nella zona negativa o oscillante. Invece, $\forall q \ge k$, $P(q)$ è vero poiché ci troviamo nella zona stabilmente positiva.

Procediamo per induzione sulla lunghezza dell’intervallo di ricerca $\ell = r - p + 1$:
- **Caso base ($\ell = 0$):** Se $p > r$, il sottoarray è vuoto, il che implica che l'indice stabile non è presente in questa porzione. L'algoritmo restituisce correttamente `0`.
- **Passo induttivo ($\ell > 0$):**
  - **Se vale $P(q)$:** Siamo nella metà stabile dell’array, quindi $q$ è un candidato valido come indice stabile. Potrebbe però non essere il *primo* in assoluto (ovvero il minimo). Riduciamo il problema scartando la metà destra e chiamando ricorsivamente `SplitRec(V, p, q - 1, n)` su un sottoarray di lunghezza strettamente minore di $\ell$. Se questa chiamata restituisce `0`, significa che non ci sono indici stabili a sinistra, e quindi $q$ è correttamente il minimo. Altrimenti, l'algoritmo propaga e restituisce il minimo trovato a sinistra.
  - **Se non vale $P(q)$:** Siamo ancora nella porzione di valori negativi o oscillanti. Nessun indice $\le q$ può essere l'indice stabile cercato. È corretto scartare interamente la metà sinistra (incluso $q$) e chiamare `SplitRec(V, q + 1, r, n)` su un sottoarray di lunghezza strettamente minore di $\ell$.

In tutte le ramificazioni, l'algoritmo si riduce a un'istanza del problema di dimensione strettamente inferiore, che per ipotesi induttiva viene risolta correttamente. Dunque `SplitRec` è corretto.

---

### iv. Complessità

Nonostante la struttura del codice con un `if-else` possa apparentemente mostrare due percorsi, l'algoritmo esegue **esattamente una** chiamata ricorsiva per ogni livello di attivazione (su un input dimezzato), poiché nel ramo `if` esegue solo la ricerca a sinistra e nel ramo `else` esegue solo la ricerca a destra.

La relazione di ricorrenza per il tempo di esecuzione è quindi:

$$
T(n) = T(n/2) + \Theta(1)
$$

dove $\Theta(1)$ rappresenta il tempo costante speso per il calcolo dell'indice centrale e la valutazione del predicato.
Per il Master Theorem ($a=1, b=2, f(n)=1$), abbiamo $n^{\log_b a} = n^{\log_2 1} = n^0 = 1$. Essendo $f(n) = \Theta(n^{\log_b a})$, ci troviamo nel **CASO 2**.
Possiamo quindi concludere che la complessità temporale esatta è:

$$
T(n) = \Theta(\log n)
$$
