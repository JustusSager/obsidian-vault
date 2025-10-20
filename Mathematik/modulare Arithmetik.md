Voraussetzung:
- [[Elementare Logik]]
# Modulo Rechnung
Modulo Rechnung ist eine Division mit Rest, bei der der Rest das Ergebnis der Rechnung ist.
Zwei Zahlen 
Zu zwei Zahlen $a \in \mathbb{Z}$ und $m \in \mathbb{N}$ gibt es ganze Zahlen $q,r \in \mathbb{Z}$ mit $a = q \cdot m + r$. Dann heißt $m$ das **Modul**, $r$ der **Rest** modulo $m$ und $q$ der **Divisor** modulo $m$.
$$ r = a \pmod m \quad \text{ und } \quad q = a (\operatorname{div}m)$$
## kongruent
Zwei zahlen $a, b$ heißen **kongruent**, wenn sie bei einer Division durch das Modul $m$ den gleichen Rest $r$ haben. Schreibweise: 
$$ a = b \pmod m $$
D.h., wenn die Differenz ein Vielfaches $k \in \mathbb{Z}$ des Moduls  ist:
$$ a - b = k \cdot m $$
**Hinweis:**
- kongruent modulo $m$ ist eine [[Relationen#Äquivalenzrelation|Äquivalenzrelation]] und damit:
	- [[Relationen#reflexiv|reflexiv]]: $a = a \pmod m$ 
	- [[Relationen#transitiv|transitiv]]: $a=b \pmod m \land b=c \pmod m \implies a=c \pmod m$ 
	- [[Relationen#symmetrisch|symmetrisch]]: $a=b \pmod m \implies b=a \pmod m$ 
## Restklasse
Enthält alle Zahlen die zu einander kongruent modulo $m$ sind. Zu dem Modul $m$ erhält man $m$ verschiedene Restklassen. 
Alle Zahlen innerhalb einer Restklasse verhalten sich bei Addition (bzw. Multiplikation) gleich:
Für alle Zahlen $a,b,c,d \in \mathbb{Z}$ mit $a=b \pmod m$ und $c=d \pmod m$ gilt:
$$ \begin{align} a + c = b + d \pmod m &\implies a + z = b + z \pmod m  \\ a \cdot c = b \cdot d \pmod m &\implies a \cdot z = b \cdot z \pmod m \implies (a)^k = (b)^k \pmod m \end{align}$$
**Beispiel:**
Zu dem Modul $m=5$ existieren 5 Restklassen: 
#TODO Das folgende hier ist evtl. nicht ganz richtig:
- Rest $r=0$: $\mathbb{Z}_0 = \{ 0, 5, 10, 15, 20, 25, \dots \}$ 
- Rest $r=1$: $\mathbb{Z}_1 = \{ 1, 6, 11, 16, 21, 26, \dots \}$ 
- Rest $r=2$: $\mathbb{Z}_2= \{ 2, 7, 12, 17, 22, 27, \dots \}$ 
- Rest $r=3$: $\mathbb{Z}_3 = \{ 3, 8, 13, 18, 23, 28, \dots \}$ 
- Rest $r=4$: $\mathbb{Z}_4 = \{ 4, 9, 14, 19, 24, 29, \dots \}$  
**Hinweis:**
- Restklassen sind [[Relationen#Äquivalenzklasse|Äquivalenzklassen]] 
- In Summen und Produkten darf jede Zahl durch irgendeinen Vertreter aus ihrer Restklasse ersetzt werden, sofern man nur am Ergebnis modulo $m$ interessiert ist.
	- Insbesondere kann jede Zahl durch den kleinsten Vertreter der Restklasse (der Rest modulo $m$) ersetzt werden.
- Auf beiden Seiten der Kongruenzgleichung kann eine ganze Zahl $z$ addiert (bzw. multipliziert) werden
	- Achtung: Kürzen ist nicht erlaubt! $8 = 2 \pmod 6 \not\!\!\!\implies 4 = 1 \pmod 6$ 
## Additive Inverse
Basierend auf der [[Gruppen, Ringe, Körper#Inverse|Inverse von Gruppen]] lässt sich für die modulare Arithmetik die additive Inverse definieren als:
$$ a + i_a = 0 \pmod m $$
**Hinweis:**
- Die add. Inverse wird auch als $-a$ geschrieben in Anlehnung an die gewohnte Schreibweise für reelle Zahlen.
- Zu jeder Zahl aus $\mathbb{Z}_m$ existiert eine additive Inverse
	- Berechnung durch $\begin{align} i_a = m -a \quad \text{für } a \ne 0 \\ i_a = 0 \quad \text{für } a = 0\end{align}$ 
**Beispiel:**
Additive Inverse in $\mathbb{Z}_5$
$$\begin{align} 
a = 0 &\implies i_a = 0 \quad 
\text{Probe: } a + i_a = 0 + 0 = 0 \pmod 5 \\ 
a = 1 &\implies i_a = 4 \quad 
\text{Probe: } a + i_a = 1 + 4 = 0 \pmod 5 \\
a = 2 &\implies i_a = 3 \quad 
\text{Probe: } a + i_a = 2 + 3 = 0 \pmod 5 \\ 
a = 3 &\implies i_a = 2 \quad 
\text{Probe: } a + i_a = 3 + 2 = 0 \pmod 5 \\
a = 4 &\implies i_a = 1 \quad 
\text{Probe: } a + i_a = 4 + 1 = 0 \pmod 5 \\
\end{align}$$
## Multiplikative Inverse
Basierend auf der [[Gruppen, Ringe, Körper#Inverse|Inverse von Gruppen]] lässt sich für die modulare Arithmetik die multiplikative Inverse definieren als:
$$ e \cdot i_e = 1 \pmod m $$
**Hinweis:**
- Die mult. Inverse wird auch als $e^{-1}$ oder ${1 \over e}$ geschrieben in Anlehnung an die gewohnte Schreibweise für reelle Zahlen.
- Nicht zu allen Zahlen in $\mathbb{Z}_m$ existiert eine mult. Inverse.
	- Zu $0$ gibt es nie eine mult. Inverse, zu $1$ gibt es immer eine in $\mathbb{Z}_m$ 
	- Zu $e \ne 0$ in $\mathbb{Z}_m$ existiert genau eine mult. Inverse wenn $e$ und $m$ teilerfremd sind.
- Berechnung mit erweitertem Euklidischen Algorithmus.
### mult. Inverse bestimmen (durch probieren)
$$ \begin{align}
e \cdot i_e = k \cdot m + 1 \pmod m \\
\implies i_e = {k \cdot m + 1 \over e}
\end{align} $$
Jetzt kann $k \in \mathbb{Z}$ durchprobiert werden, bis für $i_e$ eine ganze Zahl herauskommt.
### mult. Inverse bestimmen (erweiterter Euklidischer Algorithmus)
- mit dem Euklid Algorithmus lassen sich diophantische Gleichungen lösen, also Gleichungen der Form: $ax+by=c$ 

| k       | r     | q   | x     | y     |
| ------- | ----- | --- | ----- | ----- |
| 0       | a / b |     | 1 / 0 | 0 / 1 |
| 1       | b/ a  |     | 0 / 1 | 1 / 0 |
| 2       |       |     |       |       |
| $\dots$ |       |     |       |       |
**Vorbereitung:**
1. $k$ wird von 0 an durchnummeriert
2. $r_0 = \begin{cases} a & a > b \\ b & b > a \end{cases}$ , $x_0 = \begin{cases} 1 & a > b \\ 0 & b > a \end{cases}$ , $y_0 = \begin{cases} 1 & a < b \\ 0 & b < a \end{cases}$
	- $r_0$ ist der größere der beiden Vorfaktoren, $1$ bei der x,y-Spalte, vor dem der größere Vorfaktor steht.
3.  $r_1 = \begin{cases} a & a < b \\ b & b < a \end{cases}$ , $x_1 = \begin{cases} 1 & a < b \\ 0 & b < a \end{cases}$ , $y_1 = \begin{cases} 1 & a > b \\ 0 & b > a \end{cases}$ 
	-  $r_1$ ist der kleinere der beiden Vorfaktoren, $1$ bei der x,y-Spalte, vor dem der kleinere Vorfaktor steht.
**Durchgang:**
4. $r_k = r_{k-2} \operatorname{\%} r_{k-1}$  Rest der Division
5. $q_k = r_{k-2} \div r_{k-1}$ Ganzzahliger Quotient
6. $x_k=x_{k-2}-(q_k \cdot x_{k-1})$ 
7. wiederholen bis $r_k=0$ 
**Auswertung:**
- Über dem $r_k=0$ steht der $r_{k-1} = ggT(r_0, r_1) = ggT(a, b)$ 
	- Für die multiplikative Inverse muss der $ggT(a, b) = 1$ sein. Ansonsten existiert keine Inverse.
- Die Inverse steht in $x_{asdcd}$ 
# Rechenregeln

## additive Gleichungen
Für alle Zahlen $x,z \in \mathbb{Z}$ und $a, i_a \in \mathbb{Z}_m$ wobei $i_a$ die add. Inverse zu $a$ ist, gilt:
$$ \begin{align}
&x + a = z \pmod m \\
&\implies x + a + i_a = z + i_a \pmod m \\
&\implies x = z + i_a \pmod m
\end{align} $$
**Hinweis:**
- $a+x=b \pmod m$ besitzt immer eine eindeutige Lösung $x=-a+b \pmod m$ in $\mathbb{Z}_m$ 
## multiplikative Gleichungen
Für alle Zahlen $x,z \in \mathbb{Z}$ und $e, i_e \in \mathbb{Z}_m$ wobei $i_e$ die mult. Inverse zu $e$ ist, gilt:
$$ \begin{align}
&e \cdot x = z \pmod m \\
&\implies i_e \cdot e \cdot x = i_e \cdot z \pmod m \\
&\implies x = i_e \cdot z \pmod m
\end{align} $$
**Hinweis:**
- $a \cdot x = b \pmod m$ besitzt genau dann eine eindeutige Lösung $x=a^{-1}b \pmod m$ in $\mathbb{Z}$ wenn $a$ und $m$ teilerfremd sind.
- $a \cdot x = b \pmod m$ besitzt genau dann $t$ eindeutige Lösungen in $\mathbb{Z}_m$ , wobei $t=ggT(a,m) \gt 1$, also wenn $a$ und $m$ nicht teilerfremd sind, und wenn $t$ auch $b$ teilt; ansonsten existiert keine Lösung.
# Beispiele
## Erkennung von Fehlern mit Prüfziffern
Hiermit sollen die häufigsten Eingabefehler vermieden werden, indem hinter die eigentliche Kennnummer noch eine Prüfziffer gehangen wird, welche bestimmten Prüfvorschriften folgt.
Ein allgemeiner Ansatz dafür wäre:
$$ P(x_1, x_2, \dots , x_n) = \sum_{j=1} ^n g_j \cdot x_j = 0 \pmod m \quad \text{mit } g_j,x_j \in \{0,1,2,\dots,m-1\} \in \mathbb{Z}_m $$
d.h. das Modul $m$ legt den Wertebereich für die Ziffern $x_j$ , der Prüfnummer $P(\dots)$ und den Faktoren $g_j$ fest.
### ISBN-Nummer
Zehnstellige Internationale Standard-Buchnummer der Form `a-bcd-efghi-p`.
Jede Stelle kann eine Zahl $1,2,3, \dots , 10$ sein wobei die 10 mit dem Symbol $X$ geschrieben wird. `a` steht für das (ungefähre) Herkunftsland ($a=3$ steht für D, A, CH) und `bcd` für den Verlag. Die Prüfziffer `p` wird so gewählt, dass gilt:
$$10a+9b+8c+7d+6e+5f+4g+3h+2i+p = 0 \pmod{11}$$
#TODO Berechnungsverfahren von p
## Verschlüsselungen
### Cäsar-Verschlüsselung
Klartext: `HALLO`
Codiert: $x = 7, 0, 11, 11, 14$ 
**Verschlüsselung:**
mit Schlüssel $e = 3$ und Modul $m = 26$ 
$$ \begin{align} 
y = x + e \pmod{m} \\
y = x + 3 \pmod{26}
\end{align} $$
Verschlüsselt: $y = 10, 3, 14, 14, 17$ 
**Entschlüsselung:**
additive Inverse zu $e = 3 \implies i_e = 23$ zu Modul $m=26$ 
$$ \begin{align}
y &= x + e \pmod{m} \quad \text{| erweitern um $i_e$}\\
y + i_e &= x + e + i_e \pmod{m} \quad \text{| $e + i_e = 0$} \\
y + i_e &= x \pmod{m} \\
x &= y + 23 \pmod{26}
\end{align} $$
entschlüsselt: $x = 7, 0, 11, 11, 14$ 
### multiplikative Verschlüsselung
Klartext: `GABEL`
Codiert: $x = 6, 0, 1, 4, 11$
**Verschlüsselung:**
mit Schlüssel $e=9$ und Modul $m=26$
$$\begin{align}
y = e \cdot x \pmod m \\
y = 9 \cdot x \pmod{26}
\end{align}$$
Verschlüsselt: $y=2, 0, 9, 10, 21$
**Entschlüsselung:**
mult. Inverse zu $e=9$:
$$\begin{align} 
&i_e={k \cdot m + 1 \over e} = {k \cdot 26 + 1 \over 9}\\
&\text{mit $k = 1$} \implies i_e = {1 \cdot 26 + 1 \over 9} = {27 \over 9} = 3
\end{align}$$
dann ist:
$$\begin{align}
y &= e \cdot x \pmod m \quad \text{| erweitert um } i_e\\
i_e \cdot y &= i_e \cdot e \cdot x \pmod m \quad \text{| }i_e \cdot e = 1 \\
i_e \cdot y &= x \pmod m \\
x &= 3 \cdot y \pmod{26}
\end{align}$$
Entschlüsselt: $x = 6, 0, 1, 4, 11$ 
### RSA-Verschlüsselung
ist eine [[asymmetrische Verschlüsselung]] bei der es einen öffentlich zugänglichen public key gibt und einen geheim zu haltenden private key.
**Schlüssel generieren:**
Man wählt zwei Primzahlen $p, q$ und bildet $n = p \cdot q$ und $m=(p-1) \cdot (q-1)$.
$$\begin{align}
p = 31, q = 37 &\implies n = 31 \cdot 37 = 1147 \\
&\implies m = (31-1) \cdot (37-1) = 1080
\end{align}$$
Jetzt muss $e$ gewählt werden, sodass $ggT(e,m)=1$ und es wird die multiplikative Inverse $i_e$ zu $e$ modulo $m$ (also $e \cdot i_e=1 \pmod m$).
$e = 29$, überprüfen ob $ggT(29, 1080) = 1$ ist mit [[#mult. Inverse bestimmen (erweiterter Euklidischer Algorithmus)|erweitertem Euklid Algorithmus]].
diophantische Gleichung: $ex+my=1 \iff 29x + 1080y = 1$ 

| k   | r     | q   | x       | y   |
| --- | ----- | --- | ------- | --- |
| 0   | 1080  |     | 0       | 1   |
| 1   | 29    |     | 1       | 0   |
| 2   | 7     | 37  | -37     | 1   |
| 3   | **1** | 4   | **149** | -4  |
| 4   | 0     | 7   |         |     |
$ggT(29, 1080) = 1$ ist wahr.
multiplikative Inverse zu $e=29 \pmod{1080}$ ist $i_e=149$ 
public key: $(e,n) = (29,1147)$
private key: $(i_e,n)=(149,1147)$ 
$(p,y,m)$ bleiben geheim und werden nicht mehr benötigt.
**Verschlüsselung:**
`MATHEISTSUPER`
eine Nachricht $x$ verschlüsseln
$x = 12,0,19,7,4,8,18,19,18,20,15,4,17$ 
$$\begin{align}
y &= x^e \pmod n \\
&= x^{29} \pmod{1147}
\end{align}$$
$y = 292, 0, 979, 567, 152, 97, 205, 979, 205, 1068, 277, 132, 42$
**Entschlüsseln:**
eines Chiffretextes $y$ 
$$\begin{align}
x &= y^{i_e} \pmod n \\
&= y^{149} \pmod{1147}
\end{align}$$
$x = 12,0,19,7,4,8,18,19,18,20,15,4,17$ 
**Hinweis:**
- In der Praxis: $n \approx 2046 \text{ bit}$ lang, d.h. z.B. $e = 2^{16}+1=65537$ 
- Sicherheit: Angreifer müsste privaten Schlüssel aus öffentlichem Schlüssel berechnen, also Lösung der Gleichung $e \cdot i_e = 1 \pmod m$, dafür ist aber die Kenntnis von $m$ erforderlich. Es müssten die unbekannten Primzahlen $p,q$ ermittelt werden anhand von $n$ wofür es jedoch kein effektives Verfahren gibt.