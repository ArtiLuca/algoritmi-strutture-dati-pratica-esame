# Esercizio 1 — ABR arricchito con numero di foglie

[← Torna all'appello](README.md)

## Testo

**Esercizio 1 (9 punti)**

Realizzare un arricchimento degli alberi binari di ricerca che permetta di
ottenere per ogni nodo $x$, in tempo costante, il numero delle foglie nel
sottoalbero radicato in $x$.

Indicare quali campi occorre aggiungere ai nodi.

Fornire il codice per la funzione `leaves(x)` che restituisce il numero delle
foglie nel sottoalbero radicato in $x$ e per la procedura di inserimento di un
nodo `insert(T, z)`.

Per entrambe valutare la complessità.

---

## Soluzione

Assumiamo che ogni nodo $x$ di un albero binario di ricerca contenga già i campi
standard:

- `x.key`;
- `x.left`;
- `x.right`;
- `x.p`.

Per ottenere in tempo costante il numero di foglie nel sottoalbero radicato in
$x$, aggiungiamo a ogni nodo un campo:

```text
x.leafCount
```

Il significato del campo è:

```text
x.leafCount = numero di foglie nel sottoalbero radicato in x
```

Per convenzione:

```text
leaves(nil) = 0
```

Inoltre:

- se `x` è una foglia, allora `x.leafCount = 1`;
- se `x` non è una foglia, allora:

```math
x.leafCount =
leaves(x.left)+leaves(x.right).
```

---

## Funzione `leaves(x)`

La funzione `leaves(x)` restituisce direttamente il campo memorizzato nel nodo.

```text
leaves(x)
    if x == nil
        return 0
    else
        return x.leafCount
```

La complessità è:

```math
\Theta(1).
```

---

## Procedura `insert(T, z)`

L'inserimento è uguale all'inserimento standard in un ABR, ma alla fine bisogna
aggiornare il campo `leafCount` lungo il cammino dal nodo inserito fino alla
radice.

Ogni nuovo nodo viene inserito inizialmente come foglia, quindi:

```text
z.left = nil
z.right = nil
z.leafCount = 1
```

Poi, dopo aver collegato `z` all'albero, si risale lungo i suoi antenati e si
ricalcola `leafCount`.

```text
insert(T, z)
    x = T.root
    y = nil

    z.left = nil
    z.right = nil
    z.leafCount = 1

    while x != nil
        y = x

        if z.key < x.key
            x = x.left
        else
            x = x.right

    z.p = y

    if y == nil
        T.root = z
    else if z.key < y.key
        y.left = z
    else
        y.right = z

    x = z.p

    while x != nil
        x.leafCount = leaves(x.left) + leaves(x.right)
        x = x.p
```

---

## Correttezza dell'aggiornamento

Il nuovo nodo `z` viene inserito come foglia, quindi inizialmente il suo valore
`z.leafCount = 1` è corretto.

Gli unici nodi il cui sottoalbero può cambiare dopo l'inserimento sono gli
antenati di `z`.

Tutti gli altri nodi non hanno subito modifiche nei propri sottoalberi, quindi
il loro valore `leafCount` rimane corretto.

Per ogni antenato `x` di `z`, il numero di foglie nel sottoalbero radicato in
`x` è dato dalla somma delle foglie del sottoalbero sinistro e del sottoalbero
destro:

```math
x.leafCount =
leaves(x.left)+leaves(x.right).
```

Ricalcolando questo valore lungo il cammino da `z.p` fino alla radice,
ripristiniamo la correttezza del campo `leafCount` per tutti i nodi coinvolti.

---

## Complessità

La funzione `leaves(x)` legge semplicemente un campo del nodo, quindi costa:

```math
\Theta(1).
```

La procedura `insert(T, z)` esegue:

1. una normale ricerca della posizione di inserimento, che costa $O(h)$;
2. una risalita lungo gli antenati di `z`, che costa ancora $O(h)$.

Quindi il costo totale è:

```math
O(h)+O(h)=O(h).
```

Nel caso peggiore, se l'albero è completamente sbilanciato, $h=O(n)$ e quindi:

```math
O(h)=O(n).
```

Se l'albero è bilanciato, $h=O(\log n)$ e quindi l'inserimento costa:

```math
O(\log n).
```
