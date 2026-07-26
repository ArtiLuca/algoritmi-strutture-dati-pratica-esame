# Domanda B — Alberi binari di ricerca

[← Torna all'appello](README.md)

## Testo

**Domanda B (7 punti)**

Dare la definizione di albero binario di ricerca.

Specificare l'albero ottenuto inserendo, con la procedura vista a lezione, a
partire da un albero vuoto, i nodi aventi le seguenti chiavi:

```text
10, 5, 3, 15, 7, 12
```

Si supponga che dall'albero così ottenuto si cancelli il nodo con chiave `5` e
si indichi l'albero ottenuto.

Sia per gli inserimenti che per la cancellazione, motivare sinteticamente il
risultato ottenuto.

---

## Soluzione

## Definizione di ABR

Un **albero binario di ricerca** è un albero binario in cui, per ogni nodo `x`,
vale la seguente proprietà:

- tutte le chiavi nel sottoalbero sinistro di `x` sono minori o uguali a `x.key`;
- tutte le chiavi nel sottoalbero destro di `x` sono maggiori o uguali a `x.key`.

Questa proprietà non è solo locale rispetto ai figli immediati, ma riguarda
tutti i nodi contenuti nei sottoalberi sinistro e destro.

---

## Inserimenti

Inseriamo le chiavi nell'ordine:

```text
10, 5, 3, 15, 7, 12
```

Partiamo da un albero vuoto.

- Inseriamo `10`: l'albero è vuoto, quindi `10` diventa la radice.
- Inseriamo `5`: poiché `5 <= 10`, viene inserito come figlio sinistro di `10`.
- Inseriamo `3`: poiché `3 <= 10` e `3 <= 5`, viene inserito come figlio
  sinistro di `5`.
- Inseriamo `15`: poiché `15 >= 10`, viene inserito come figlio destro di `10`.
- Inseriamo `7`: poiché `7 <= 10` e `7 >= 5`, viene inserito come figlio destro
  di `5`.
- Inseriamo `12`: poiché `12 >= 10` e `12 <= 15`, viene inserito come figlio
  sinistro di `15`.

L'albero ottenuto è:

```text
          10
         /  \
        5    15
       / \   /
      3   7 12
```

---

## Cancellazione del nodo con chiave 5

Ora cancelliamo il nodo con chiave `5`.

Il nodo `5` ha due figli:

```text
3 e 7
```

Quindi siamo nel caso di cancellazione di un nodo con due figli.

In questo caso si sostituisce il nodo da eliminare con il suo successore, cioè
con il minimo del suo sottoalbero destro.

Il sottoalbero destro di `5` contiene solo il nodo `7`, quindi il successore di
`5` è proprio `7`.

Poiché `7` è il figlio destro diretto di `5`, la sostituzione è semplice:

- `7` prende il posto di `5`;
- il vecchio sottoalbero sinistro di `5`, cioè il nodo `3`, diventa il
  sottoalbero sinistro di `7`;
- il resto dell'albero rimane invariato.

L'albero finale è:

```text
          10
         /  \
        7    15
       /     /
      3     12
```

La proprietà di albero binario di ricerca è mantenuta:

- nel sottoalbero sinistro di `10` troviamo `7` e `3`, entrambi minori di `10`;
- `3` è minore di `7`;
- nel sottoalbero destro di `10` troviamo `15` e `12`, entrambi maggiori di `10`;
- `12` è minore di `15`.
