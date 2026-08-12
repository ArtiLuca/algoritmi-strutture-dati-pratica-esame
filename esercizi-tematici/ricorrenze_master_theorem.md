# Ricorrenze Master Theorem

Il Master Theorem si applica per ricorrenze del tipo $T(n) = aT(n/b) + f(n)$ con $a \ge 1, b > 1$.  
Si basa sul confronto asintotico tra la *driving function* $f(n)$ e la *watershed function* $n^{\log_b a}$.

In tutte le 5 ricorrenze proposte i parametri sono $a=2$ e $b=4$, quindi la *watershed function* è sempre:  
$$n^{\log_b a} = n^{\log_4 2} = n^{1/2} = \sqrt{n}$$

---

### (1) $T(n) = 2T(n/4) + 1$

Qui abbiamo $f(n) = 1$.  
Si nota che $n^{\log_b a} \gg f(n)$, quindi cerchiamo un $\varepsilon > 0$ tale per cui $f(n) = \mathcal{O}(n^{\log_b a - \varepsilon})$.  

Valutiamo il limite:  

$$\lim_{n\to \infty} \frac{f(n)}{n^{\log_b a - \varepsilon}} = \lim_{n\to \infty} \frac{1}{n^{1/2 - \varepsilon}} = 0$$  
  
Questo è vero per qualsiasi $0 < \varepsilon < 1/2$.  
Siamo nel **CASO 1** del Master Theorem. Si conclude che:  

$$T(n) = \Theta(n^{\log_b a}) = \Theta(\sqrt{n})$$

---

### (2) $T(n) = 2T(n/4) + \sqrt{n}$

Qui abbiamo $f(n) = \sqrt{n}$. 

Si nota subito che $f(n)$ e la watershed function crescono in modo asintoticamente equivalente:  
  
$$f(n) = \Theta(n^{\log_b a})$$
  
Siamo nel **CASO 2** del Master Theorem. 

Si conclude direttamente che:  

$$T(n) = \Theta(n^{\log_b a} \cdot \log n) = \Theta(\sqrt{n} \log n)$$

---

### (3) $T(n) = 2T(n/4) + \sqrt{n}\log^2n$

Qui abbiamo $f(n) = \sqrt{n}\log^2 n$. 
La *watershed function* cresce più lentamente, ovvero $n^{\log_b a} \ll f(n)$.  
Potremmo essere nel Caso 3.  

Verifichiamo la prima condizione, ovvero se $\exists \varepsilon > 0$ tale che $f(n) = \Omega(n^{\log_b a + \varepsilon})$.  

Valutiamo il limite:  

$$\lim_{n\to \infty} \frac{\sqrt{n}\log^2 n}{n^{1/2+\varepsilon}} = \lim_{n\to \infty} \frac{\sqrt{n}\log^2 n}{\sqrt{n} \cdot n^\varepsilon} = \lim_{n\to \infty} \frac{\log^2 n}{n^\varepsilon}$$  


Poiché le funzioni polinomiali crescono sempre asintoticamente più velocemente di quelle logaritmiche, questo limite fa 0 per qualsiasi $\varepsilon > 0$.  
Pertanto, la condizione del Caso 3 fallisce.  
  
Ricorriamo quindi al **CASO 2 Generalizzato**, che si applica quando $f(n) = \Theta(n^{\log_b a} \cdot \log^k n)$.  
Nel nostro caso la condizione è verificata con $k=2$.
  
Si conclude che:  

$$T(n) = \Theta(n^{\log_b a} \cdot \log^{k+1} n) = \Theta(\sqrt{n}\log^3 n)$$

---

### (4) $T(n) = 2T(n/4) + n$

Qui abbiamo $f(n) = n$. Poiché $n^{\log_b a} \ll f(n)$, verifichiamo le condizioni del **CASO 3**.  

**Prima condizione:** $\exists \varepsilon > 0$ tale che $f(n) = \Omega(n^{\log_b a + \varepsilon})$.  
Valutando il limite  

$\lim_{n\to \infty} \frac{n}{n^{1/2+\varepsilon}} = +\infty$  
  
notiamo che è verificato per un valore $0 < \varepsilon < 1/2$  (oppure con limite finito per $\varepsilon = 1/2$).
  
**Seconda condizione (Regolarità):** $\exists k < 1$ tale che $a \cdot f(n/b) \le k \cdot f(n)$.  

$$2 \cdot \left(\frac{n}{4}\right) \le k \cdot n \implies \frac{1}{2}n \le k \cdot n$$  

La condizione è soddisfatta scegliendo una costante $k$ tale che $1/2 \le k < 1$.  

Entrambe le condizioni sono verificate. Si conclude che:  
   
$$T(n) = \Theta(f(n)) = \Theta(n)$$

---

### (5) $T(n) = 2T(n/4) + n^2$

Qui abbiamo $f(n) = n^2$. Come nel punto precedente, siamo nel **CASO 3**.  

**Prima condizione:** In modo analogo alla ricorrenza (4), si trova che una scelta di $\varepsilon$ (ad esempio $\varepsilon = 1$)  
soddisfa ampiamente la condizione $f(n) = \Omega(n^{\log_b a + \varepsilon})$.

**Seconda condizione (Regolarità):** $a \cdot f(n/b) \le k \cdot f(n)$.  

$$2 \cdot \left(\frac{n}{4}\right)^2 = 2 \cdot \left(\frac{n^2}{16}\right) = \frac{1}{8}n^2 \le k \cdot n^2$$  

La disuguaglianza è soddisfatta scegliendo una costante $k$ tale che $1/8 \le k < 1$.  

Entrambe le condizioni sono verificate. Si conclude che:  

$$T(n) = \Theta(f(n)) = \Theta(n^2)$$
