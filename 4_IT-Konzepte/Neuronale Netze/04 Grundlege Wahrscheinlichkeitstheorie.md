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

### Varianz
[[31-1 Numerische Maßzahlen#^651312|Siehe Varianz]]
$Var[x]= \sigma^2 = E[(x-\mu)^2]=\sum_{x \in X} (x-\mu)^2 \cdot P(x)$
- $Var[x]$: Varianz
- $\sigma^2$: Standardabweichung $\sigma$
