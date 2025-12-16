Das Grundproblem, dass mithilfe der Integration zu lösen ist, ist das Flächenproblem. D.h. die Berechnung der Fläche unter einer Kurve.
![[ansatz_integration.png]]
Ansatz ist, dass man unendliche schmal werdende Rechtecke unter der Kurve betrachtet. Also eine Grenzwertbetrachtung mit $\lim_{\Delta x \to 0}$. 
Dies lässt sich darstellen als:
$$A=\int_a^b f(x) = \lim_{n \to \infty} \left(\Delta x \cdot \sum_{i=0}^{n-1} f(x_i) \right) \quad \text{wobei: } b = a + n \cdot \Delta x$$
Streben Ober- und Untersumme für $n \to \infty$ gegen den gleichen Grenzwert, so heißt dieser bestimmtes Integral der Funktion $f(x)$ in den Grenzen von $a$ bis $b$.
Eine einfachere Rechnung als über den limes ist über die Bildung der **Stammfunktion**. 
$$I = \int_a^b f(x) dx = \int_a^b F'(x) = [ F(x) ]_a^b = F(b) - F(a)$$
**Hinweis:**
- Bei unbestimmten Integralen wird $F(x)$ noch mit einer Konstanten $C$  addiert. 
- f(x) muss stetig sein
- Verläuft die Kurve unterhalb der x-Achse, ist das Ergebnis des Integrals negativ. 
	- Die Fläche wäre der Betrag des zugehörigen Integrals
	- Liegt die Fläche teils über, teils unter der x-Achse, müssen die Teilflächen gesondert berechnet werden, um die echte Fläche zu bekommen.
- 
# Grundrechenregeln
**Faktorregel:** 
$$\int C \cdot f(x) dx = C \cdot \int f(x) dx$$
**Vertauschungsregel:** 
$$\int_a^b f(x) = -\int_b^a f(x)$$
**Summenregel:**
$$\int (f(x) + g(x)) = \int f(x) + \int g(x)$$
**Gleichheit von oberer und unterer Grenze:**
$$\int_a^a f(x) = 0$$
**Intervallregel:**
$$\int_a^c f(x) = \int_a^b f(x) + \int_b^c f(x)$$
**Potenzregel:**
$$\int x^n dx = {x^{n+1} \over n+1}, \quad n \ne 0$$

# Erweiterte Rechenregeln
## Integration durch Substitution
Entsprechend der [[Differenzialrechnung#Kettenregel|Kettenregel bei der Differenzierung]] kann beim Integrieren substituiert werden. 
$$\int f(g(x)) \cdot g'(x) dx = F(g(x)) + C \quad \text{wobei $f$ Ableitung von $F$ ist}$$
**Vorgehensweise:**
1. Neue Variable einführen (Substitution): $$u = g(x)$$
2. Ableitung bilden: $${du \over dx} = g'(x) \implies du = g'(x) dx$$
3. Integral umschreiben: 
   ggf. muss hier ein Vorfaktor angepasst werden, sodass man die passende Form erhält. $$\int f(g(x)) \cdot g'(x) dx = \int f(u) du$$
4. Stammfunktion bestimmen: $$\int f(u) du = F(u) + C$$
5. Rücksubstituieren: $$F(u) + C = F(g(x)) + C$$
## Partielle Integration
Entsprechend der [[Differenzialrechnung#Produktregel|Produktregel der Differentialrechnung]] kann beim Integrieren ein partielle Integration durchgeführt werden.
$$\begin{align}
\int u'(x) + v(x) dx &= u(x) + v(x) - \int u(x) + v'(x) dx \\
&\text{oder} \\
\int u(x) + v'(x) dx &= u(x) + v(x) - \int u'(x) + v(x) dx
\end{align}$$
### DI-Methode/Tanzalin-Methode
Die Partielle Integration kann auch wiederholt durchgeführt werden, indem ein Teil differenziert wird bis er stark vereinfacht ist, der andere wird genauso häufig integriert. Danach können die Teile zusammengesetzt werden.
$$\int f(x) \cdot g(x)=\sum_{k=0}^{n-1} \left( (-1)^k \cdot f^{(k)}(x) \cdot g^{(-1-k)}(x) \right) + (-1)^n \cdot \int f^{(n)}(x) \cdot g^{-n}(x) dx$$
Dabei können folgende 3 Fälle als Endfälle für die Differenzierung / Integration der Terme genutzt werden:
**1. Fall:**
Der zu differenzierende Teil wird 0, wodurch der Integralteil am Ende wegfällt und zu $C$ wird.
**2. Fall:**
In einer Zeile entsteht ein als Produkt einfach zu integrierender Term. Das Ergebnis ist die Summe der einzelnen Integrationsschritte + die Integration des einfach zu integrierenden Terms.
- Nicht die Konstante $C$ als Summand vergessen.
**3. Fall:**
Bis auf einen Vorfaktor entsteht wieder der ursprüngliche zu integrierende Term. Das Ergebnis lässt sich als Summe der einzelnen partiellen Integrationsschritte aufschreiben, wobei der letzte Summand dann das Vielfache von I ist. 
- $I = \int f(x) \cdot g(x)$ also das ursprüngliche Integral
- Nicht die Konstante $C$ als Summand vergessen.
## Partialbruchzerlegung
#TODO Partialbruchzerlegung
