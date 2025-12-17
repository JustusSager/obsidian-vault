Hier kommt alles rund um Analysis und Kurvendiskussion rein.
**Hinweis:**
- Teil der Analysis wäre auch das Rechnen mit Vektoren und Matrizen, dies ist jedoch ausgelagert in [[Vektoren]], [[Matrizen]].
# Steigung einer Funktion
## Steigung einer Geraden
![[steigung_gerade.png]]
$$\begin{align}
f(x) = m \cdot x + b \\
m = {y - y_0 \over x - x_0} = \tan(\beta)
\end{align}$$
## Steigung einer Kurve
![[steigung_kurve.png]]
Wenn sich der Punkt $Q$ immer näher an den Punkt $P$ annähert ($\Delta x \to 0$ und $\Delta y \to 0$), nähert sich auch die Sekante an die Tangente an. $m_{Sek.} = \tan(\beta) \to m_{Tan.} =  \tan(\alpha)$.
**Grenzwertbetrachtung:**
$$ \lim_{\Delta x \to 0} {\Delta y \over \Delta x} = \lim_{\Delta x \to 0} {f(x + \Delta x) - f(x) \over \Delta x} = {dy \over dx}$$
- Hier der rechtsseitiger Grenzwert, da $x_0 = x_P \lt x_Q = x_P + \Delta x$ mit $\Delta x \gt 0$ 
- Grenzwertbestimmung heißt auch [[#Differenzialrechnung|ableiten]] oder Differenzieren der Funktion $f(x) = y$ 
# Differenzialrechnung
Das Grundproblem, welches mit der Differentialrechnung gelöst werden soll, ist die Ermittlung der Steigung an einer bestimmten Stelle einer Kurve. Dafür kann die Ableitung einer Funktion gebildet werden
**Ableitung von Funktionen in der Form $y = f(x)$.**
Eine Funktion heißt differenzierbar, wenn der rechtseitige und der linksseitige Grenzwert  existieren und übereinstimmen.
$$\lim_{\Delta x \to 0} {\Delta y \over \Delta x} = \lim_{\Delta x \to 0} {f(x_0 + \Delta x) - f(x_0) \over \Delta x} = f'(x_0)$$
Dieser Grenzwert heißt auch **1. Ableitung** der Funktion $y = f(x)$ an der Stelle $x_0$.
**Hinweise:**
- Findet man zu jedem x einen beidseitig bestimmten Grenzwert, so heißt die Funktion Ableitungsfunktion $f'(x)$ 
- Andere Schreibweisen: ${dy \over dx} = {d \over dx} (f(x)) = f'(x) = y'(x)$ 
- Nur stetige Funktionen sind Differenzierbar (notwendig, aber nicht ausreichende Bedingung)
**Beispiel:**
$$\begin{align}
y &= x^2 \\
y' &= 2x
\end{align}$$
## Grundlegende Ableitungsregeln
### Potenzregel
Eine Potenzfunktion lässt sich einfach ableiten mit:
$$\begin{align}
y &= x^n \\
y' &= n \cdot x^{n-1}
\end{align}$$
### Konstantenregel
Ein Konstanter Faktor bleibt erhalten
$$\begin{align}
y &= C \cdot f(x) \\
y' &= C \cdot f'(x)
\end{align}$$
### Summenregel
eine endliche Reihe von Summanden wird gliedweise differenziert
$$\begin{align}
y &= f(x) + g(x) + h(x) + \dots\\
y' &= f'(x) + g'(x) + h'(x) + \dots
\end{align}$$
### Produktregel
$$\begin{align}
y &= u(x) \cdot v(x) \\
y' &= u'(x) \cdot v(x) + u(x) \cdot v'(x)
\end{align}$$
### Quotientenregel
$$\begin{align}
y &= {u(x) \over v(x)} \\
y' &= {u'(x) \cdot v(x) - u(x) \cdot v'(x) \over v^2(x)} \text{ mit } v(x) \ne 0
\end{align}$$
### Kettenregel
Ableitung von ineinander verschachtelten Funktionen
$$\begin{align}
y &= {f(u(x))} \\
y' &= f'(u(x)) \cdot u'(x)
\end{align}$$
### Ableitungen elementarer Funktionen:

| Funktion $y = f(x)$ | Ableitung $y' = f'(x)$                |
| ------------------- | ------------------------------------- |
| $$e^x$$             | $$e^x$$                               |
| $$a^x$$             | $$a^x \cdot \ln(a)$$                  |
| $$\ln(x)$$          | $$1 \over x$$                         |
| $$\log_a (x)$$      | $$a \over x \cdot \ln a$$             |
| $$\sin x$$          | $$\cos x$$                            |
| $$\cos x$$          | $$-\sin x$$                           |
| $$\tan x$$          | $${1 \over \cos^2 x} = 1 + \tan^2 x$$ |
## Ableitung spezieller Funktionen
### Ableitung impliziter Funktionen
**Ableitung von Funktionen in der Form $F(x,y)=0$** z.B. $x \cdot y^2 - y^3 - 4x = 0$ 
Es wird hierbei Gliedweise nach $x$ abgeleitet. Jeder Term, der $y$ enthält wird dabei als eine von $x$ abhängige Funktion mithilfe der Kettenregel abgeleitet. Anschließend wird nach $y'$ aufgelöst.
**Hinweis:**
- $y'$ kann dabei die Variablen $x$ und $y$ enthalten.
- $y^n$ wird zu $n\cdot y^{n-1}{dy \over dx}$ abgeleitet.
**Beispiel:**
$x \cdot y^2 - y^3 - 4x = 0$
1. Alle Glieder einzeln ableiten:
$$\begin{align}
x \cdot y^2 - y^3 - 4x = 0 \\
y^2 + 2xy{dy \over dx} - 3y^2{dy \over dx} - 4 = 0
\end{align}$$
		Hilfsrechnung $x \cdot y^2$ ableiten mithilfe der [[#Produktregel]] 
$$\begin{align}
x \cdot y^2 = u(x) \cdot v(x) &= (x)(y^2)\\
(u(x) \cdot v(x))' &= u'(x) \cdot v(x) + u(x) \cdot v'(x) \\
&= (x)' \cdot (y^2) + (x) \cdot (y^2)' \\
&= 1 \cdot y^2 + x \cdot 2y{dy \over dx} \\
&= y^2 + 2xy{dy \over dx}
\end{align}$$
2. Nach $dy \over dx$ auflösen
$$\begin{align}
y^2 + 2xy{dy \over dx} - 3y^2{dy \over dx} - 4 &= 0 \\
y^2 - 4 &= 3y^2{dy \over dx} - 2xy{dy \over dx} \\
y^2 - 4 &= {dy \over dx} \cdot (3y^2 - 2xy) \\
{y^2 - 4 \over 3y^2 - 2xy}&= {dy \over dx} \\
\end{align}$$
# Integralrechnung
Das Grundproblem, dass mithilfe der Integration zu lösen ist, ist das Flächenproblem. D.h. die Berechnung der Fläche unter einer Kurve.
![[ansatz_integration.png]]
Ansatz ist, dass man unendliche schmal werdende Rechtecke unter der Kurve betrachtet. Also eine Grenzwertbetrachtung mit $\lim_{\Delta x \to 0}$. 
Dies lässt sich darstellen als:
$$A=\int_a^b f(x) = \lim_{n \to \infty} \left(\Delta x \cdot \sum_{i=0}^{n-1} f(x_i) \right) \quad \text{wobei: } b = a + n \cdot \Delta x$$
Streben Ober- und Untersumme für $n \to \infty$ gegen den gleichen Grenzwert, so heißt dieser bestimmtes Integral der Funktion $f(x)$ in den Grenzen von $a$ bis $b$.
Eine einfachere Rechnung als über den limes ist über die Bildung der **Stammfunktion**. 
$$I = \int_a^b f(x) \ dx = \int_a^b F'(x) = [ F(x) ]_a^b = F(b) - F(a)$$
**Hinweis:**
- Bei unbestimmten Integralen wird $F(x)$ noch mit einer Konstanten $C$  addiert. 
- f(x) muss stetig sein
- Verläuft die Kurve unterhalb der x-Achse, ist das Ergebnis des Integrals negativ. 
	- Die Fläche wäre der Betrag des zugehörigen Integrals
	- Liegt die Fläche teils über, teils unter der x-Achse, müssen die Teilflächen gesondert berechnet werden, um die echte Fläche zu bekommen.
- 
## Grundrechenregeln
### Faktorregel
$$\int C \cdot f(x) \ dx = C \cdot \int f(x) \ dx$$
### Vertauschungsregel
$$\int_a^b f(x) \ dx = -\int_b^a f(x) \ dx$$
### Summenregel
$$\int (f(x) + g(x)) \ dx = \int f(x) \ dx + \int g(x) \ dx$$
### Gleichheit von oberer und unterer Grenze
$$\int_a^a f(x) \ dx = 0$$
### Intervallregel
$$\int_a^c f(x) \ dx = \int_a^b f(x) \ dx + \int_b^c f(x)\ dx $$
### Potenzregel
$$\int x^n \ dx = {x^{n+1} \over n+1}, \quad n \ne 0$$

## Erweiterte Rechenregeln
### Integration durch Substitution
Entsprechend der [[#Kettenregel|Kettenregel bei der Differenzierung]] kann beim Integrieren substituiert werden. 
$$\int f(g(x)) \cdot g'(x) \ dx = F(g(x)) + C \quad \text{wobei $f$ Ableitung von $F$ ist}$$
**Vorgehensweise:**
1. Neue Variable einführen (Substitution): $$u = g(x)$$
2. Ableitung bilden: $${du \over dx} = g'(x) \implies du = g'(x) \ dx$$
3. Integral umschreiben: 
   ggf. muss hier ein Vorfaktor angepasst werden, sodass man die passende Form erhält. $$\int f(g(x)) \cdot g'(x) \ dx = \int f(u) \ du$$
4. Stammfunktion bestimmen: $$\int f(u) \ du = F(u) + C$$
5. Rücksubstituieren: $$F(u) + C = F(g(x)) + C$$
### Partielle Integration
Entsprechend der [[#Produktregel|Produktregel der Differentialrechnung]] kann beim Integrieren ein partielle Integration durchgeführt werden.
$$\begin{align}
\int u'(x) + v(x) \ dx &= u(x) + v(x) - \int u(x) + v'(x) \ dx \\
&\text{oder} \\
\int u(x) + v'(x) \ dx &= u(x) + v(x) - \int u'(x) + v(x) \ dx
\end{align}$$
### DI-Methode/Tanzalin-Methode
Die Partielle Integration kann auch wiederholt durchgeführt werden, indem ein Teil differenziert wird bis er stark vereinfacht ist, der andere wird genauso häufig integriert. Danach können die Teile zusammengesetzt werden.
$$\int f(x) \cdot g(x) \ dx = \sum_{k=0}^{n-1} \left( (-1)^k \cdot f^{(k)}(x) \cdot g^{(-1-k)}(x) \right) + (-1)^n \cdot \int f^{(n)}(x) \cdot g^{-n}(x) \ dx$$
Dabei können folgende 3 Fälle als Endfälle für die Differenzierung / Integration der Terme genutzt werden:
**1. Fall:**
Der zu differenzierende Teil wird 0, wodurch der Integralteil am Ende wegfällt und zu $C$ wird.
**2. Fall:**
In einer Zeile entsteht ein als Produkt einfach zu integrierender Term. Das Ergebnis ist die Summe der einzelnen Integrationsschritte + die Integration des einfach zu integrierenden Terms.
- Nicht die Konstante $C$ als Summand vergessen.
**3. Fall:**
Bis auf einen Vorfaktor entsteht wieder der ursprüngliche zu integrierende Term. Das Ergebnis lässt sich als Summe der einzelnen partiellen Integrationsschritte aufschreiben, wobei der letzte Summand dann das Vielfache von I ist. 
- $I = \int f(x) \cdot g(x)\ dx$ also das ursprüngliche Integral
- Nicht die Konstante $C$ als Summand vergessen.
### Partialbruchzerlegung #TODO
### Integrale mit einem unendlichen Grenzwert #TODO
## Verschiedenste Anwendungsfälle
### Bogenlänge einer ebenen Kurve #TODO
### Fläche zwischen ebenen Kurven #TODO
### Volumina von Rotationskörpern #TODO
### Flächenschwerpunkte
$$\begin{align}
x_s = {1 \over A} \cdot \int_a^b x \cdot y \ dx \\
y_s = {1 \over 2A} \cdot \int_a^b y^2 \ dx
\end{align}$$
- für $y$ wird entsprechend die Funktion der eingrenzenden Kurve eingefügt.
### Linearer Mittelwert
Der lineare Mittelwert einer Funktion $y = f(x)$ im Intervall $a \le x \le b$ ist die Größe:
$$\bar y_{lin} = {1 \over b - a} \int_a^b f(x) \ dx $$
![[integral_linearer_mittelwert.png|300]]
### Volumen eines Rotationskörpers
#### Rotation um x-Achse
![[integral_volumen_rotationskoerper.png|300]]
$$V_x = \lim_{\Delta x \to 0} \sum_{i=1}^n \pi \cdot (f(x_i))^2 \cdot \Delta x = \int_a^b \pi \cdot (f(x))^2 \ dx = \int_a^b \pi \cdot y^2$$

# Quellen
- https://de.wikipedia.org/wiki/Analysis
- `Mathe 1 für Informatiker (WiSe25/26)` Modul der HAW Kiel
- `Mathe 2 für Informatiker (SoSe25)` Modul der HAW Kiel