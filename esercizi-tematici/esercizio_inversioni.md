# Conteggio delle inversioni

Realizzare con approccio divide et impera una funzione `Inv(A, p, r)` che ritorna il numero di inversioni in $A[p \dots r]$, ovvero il numero di coppie di indici $i,j$ tali che:

$$i < j \quad \text{e} \quad A[i] > A[j]$$

*Suggerimento: modificare il MergeSort.*

---

### Soluzione

Come suggerito, possiamo utilizzare una versione leggermente modificata del `MergeSort` per contare il numero di inversioni, visto che l’ordinamento del `MergeSort` si basa sullo scambio di elementi e sul confronto tra porzioni di array.
Si basa su un approccio *Divide et Impera* per suddividere l’array $A$ in due sottoarray, ordinarli, e ricombinarli finché tutto $A$ non sia ordinato in senso crescente.

Usiamo `Inv(A, p, r)` come procedura principale che ordina $A$ in senso crescente esattamente come si fa nel `MergeSort` con l’unica modifica sul valore di ritorno: alla fine si restituisce il numero totale di inversioni trovate durante l’ordinamento.

Per fare ciò, utilizziamo una versione della procedura ausiliaria `Merge` leggermente modificata. La procedura `MergeInv(A, p, q, r)` ordina i due sottoarray $L[p\dots q]$ e $R[q+1\dots r]$ e poi li ricombina assieme, restituendo il numero di inversioni trovate durante il processo.

In particolare, i sottoarray $L$ e $R$ sono già ordinati. Ogni volta che si trovano due elementi $L[i]$ e $R[j]$ tali che $L[i] > R[j]$, allora si dovranno "scambiare" (ovvero, $R[j]$ viene inserito prima in $A$). Questa coppia forma un'inversione. Inoltre, poiché $L$ è ordinato in senso crescente, se $L[i] > R[j]$, allora anche tutti gli elementi successivi in $L$ (cioè $L[i+1], L[i+2], \dots, L[n_1]$) saranno strettamente maggiori di $R[j]$.
Quindi, non troviamo una sola inversione, ma ne troviamo esattamente $n_1 - i + 1$, che andiamo ad accumulare in una variabile locale `count`.

La procedura `Inv(A, p, r)` restituisce il numero totale di inversioni trovate. Ovvero, restituisce il valore dato da:
`Inv(A, p, q) + Inv(A, q+1, r) + MergeInv(A, p, q, r)`
che equivale al numero di inversioni trovate nella chiamata ricorsiva sul sottoarray sinistro, più quelle sul sottoarray destro, più quelle trovate "a cavallo" dalla procedura `MergeInv`.

Alla fine, $A[1\dots n]$ sarà ordinato in senso crescente come nel `MergeSort` e quindi l'algoritmo avrà una complessità invariata, cioè $\Theta(n\log n)$.

### Pseudocodice

```text
// Ordina A e restituisce il numero totale di inversioni trovate
Inv(A, p, r)
    count = 0
    if p < r
        q = floor((p+r)/2)
        // Sommo tutte le inversioni trovate (sx + dx + "a cavallo")
        count = Inv(A, p, q) + Inv(A, q+1, r) + MergeInv(A, p, q, r)
    return count

MergeInv(A, p, q, r)
    // Come nel MergeSort, si creano due sottoarray temporanei
    n1 = q - p + 1
    n2 = r - q
    allocate L[1...n1+1]
    allocate R[1...n2+1]

    // Si riempiono i sottoarray
    for i = 1 to n1
        L[i] = A[p+i-1]
    for j = 1 to n2
        R[j] = A[q+j]

    // Inserimento dei valori sentinella      
    L[n1+1] = +∞
    R[n2+1] = +∞

    i = 1
    j = 1

    // Inizializziamo il contatore di inversioni per questa fase
    count = 0

    for k = p to r
        if L[i] <= R[j]
            A[k] = L[i]
            i = i + 1
        else
            A[k] = R[j]
            // Se L[i] > R[j], formano un'inversione R[j] con L[i]
            // e con tutti gli elementi successivi in L
            count = count + (n1 - i + 1)
            j = j + 1                               

    return count
```
