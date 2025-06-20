## Merkmalsausprägungen
Es lässt sich annehmen, dass eine zufälliges Merkmal $x$ eine bestimmte begrenzte Menge an Werten hat, die Es annehmen kann.
$X=\{v_1, v_2, ... , v_m\}$

## Wahrscheinlichkeit
Die Wahrscheinlichkeit, dass das Merkmal $x$ einen bestimmten Wert aus der Menge $X$ annimmt.
$p_i=Pr(x=v_i), i=1, ... , m$
**Voraussetzung:**
- $p_i\geq 0$
- $\sum_{i=1}^m p_i = 1$

# Diskrete Verteilung
Bei der diskreten Verteilung lässt sich die Menge der Wahrscheinlichkeiten $\{p_1, p_2, ... , p_m\}$ ausdrücken als `probability mass funktion` $P(x)$
**Voraussetzung:**
- $P(x) \geq 0$
- $\sum_{x \in X} P(x) = 1$
- $\sum_{x \notin X} P(x) = 0$

### Support $S_x$
Die Sammlung aller Merkmale, die eine Wahrscheinlichkeit größer 0 haben ($P(x) \gt 0$) nennt man `support` $S_x$. 

### relative Häufigkeit / empirische Wahrscheinlichkeit $h_n(A)$
Die Wahrscheinlichkeit, welche jedoch nicht bekannt ist, sondern durch Versuche / Experimente ermittelt wurde.
$h_n(A)=\frac{H_n(A)}{n}$
- $A$: Merkmal
- $h$: relative Häufigkeit
- $H$: absolute Häufigkeit
- $n$: Anzahl der durchgeführten Experimente

### Erwartungswert (Mittelwert)
[[31-1 Numerische Maßzahlen#^310b8e|Siehe Arithmetischer Mittelwert]]
$E[x]=\mu=\sum_{x \in X} x \cdot P(x) = \sum_{i=1}^m v_i \cdot p_i$
#### Bei zwei Variablen
$\mu_x=E[x]=sum_{x \in X} sum_{y \in Y} x \cdot P(x,y)$
$\mu_y=E[y]=sum_{x \in X} sum_{y \in Y} y \cdot P(x,y)$

### Varianz
[[31-1 Numerische Maßzahlen#^651312|Siehe Varianz]]
$Var[x]= \sigma^2 = E[(x-\mu)^2]=\sum_{x \in X} (x-\mu)^2 \cdot P(x)$
- $Var[x]$: Varianz
- $\sigma^2$: Standardabweichung $\sigma$
#### Bei zwei Variablen
$\sigma_x²=E[(x-\mu_x)²]=\sum_{x \in X} \sum_{y \in Y} (x- \mu_x)² \cdot P(x,y)$
$\sigma_y²=E[(y-\mu_y)²]=\sum_{x \in X} \sum_{y \in Y} (y- \mu_y)² \cdot P(x,y)$

## Statistische Unabhängigkeit
$P(x,y)=P(x) \cdot P(y)$
Der Wert von $x$ gibt keine Rückschlüsse auf den Wert von $y$.

## Shanon information content
- Deterministische Ergebnisse enthalten keine Informationen
	- $P(x)=1 \rightarrow h(x)=\log_2 \frac{1}{P(x)}=\log_2 1=0$
- Informationsgehalt steigt mit sinkender Wahrscheinlichkeit
- Informationsgehalt ist additiv für statistisch unabhängige zufällige Variablen
	- $h(x,y)=h(x)+h(y)$
- 
### diskrete zufällige Variablen
$h(x)=\log_2 (\frac{1}{P(x)})=-\log_2 (P(x))=-ld (P(x))$
### stetige zufällige Variablen
$h(x)=\log_e (\frac{1}{P(x)})=-\log_e (P(x))=-\ln (P(x))$

### Shanon Entropy
Misst wie verteilt die möglichen Resultate sind für eine zufällige Variable
$H(x)=- \sum_{x \in X} P(x) \cdot \log_2 P(x)$
