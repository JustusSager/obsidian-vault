# Grundbegriffe
## Steigung
### Steigung einer Geraden
![[steigung_gerade.png]]
$$\begin{align}
f(x) = m \cdot x + b \\
m = {y - y_0 \over x - x_0} = \tan(\beta)
\end{align}$$
### Steigung einer Kurve
![[steigung_kurve.png]]
Wenn sich der Punkt $Q$ immer näher an den Punkt $P$ annähert ($\Delta x \to 0$ und $\Delta y \to 0$), nähert sich auch die Sekante an die Tangente an. $m_{Sek.} = \tan(\beta) \to m_{Tan.} =  \tan(\alpha)$.
**Grenzwertbetrachtung:**
$$ \lim_{\Delta x \to 0} {\Delta y \over \Delta x} = \lim_{\Delta x \to 0} {f(x + \Delta x) - f(x) \over \Delta x} = {dy \over dx}$$
- Hier der rechtsseitiger Grenzwert, da $x_0 = x_P \lt x_Q = x_P + \Delta x$ mit $\Delta x \gt 0$ 
- Grenzwertbestimmung heißt auch [[#Ableitung|Ableiten]] oder Differenzieren der Funktion $f(x) = y$ 
## Ableitung
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
### Ableitungen elementarer Funktionen

| Funktion $y = f(x)$ | Ableitung $y' = f'(x)$                |
| ------------------- | ------------------------------------- |
| $$e^x$$             | $$e^x$$                               |
| $$a^x$$             | $$a^x \cdot \ln(a)$$                  |
| $$\ln(x)$$          | $$1 \over x$$                         |
| $$\log_a (x)$$      | $$a \over x \cdot \ln a$$             |
| $$\sin x$$          | $$\cos x$$                            |
| $$\cos x$$          | $$-\sin x$$                           |
| $$\tan x$$          | $${1 \over \cos^2 x} = 1 + \tan^2 x$$ |
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
