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
- Die additive Inverse wird auch als $-a$ geschrieben in Anlehnung an die gewohnte Schreibweise für reelle Zahlen.
- Zu jeder Zahl aus $\mathbb{Z}_m$ existiert eine additive Inverse
	- Berechnung durch $\begin{align} i_a = m -a \quad \text{für } a \ne 0 \\ i_a = 0 \quad \text{für } a = 0\end{align}$ 
# Beispiele
## ISBN-Nummer
Zehnstellige Internationale Standard-Buchnummer der Form `a-bcd-efghi-p`.
Jede Stelle kann eine Zahl $1,2,3, \dots , 10$ sein wobei die 10 mit dem Symbol $X$ geschrieben wird. `a` steht für das (ungefähre) Herkunftsland ($a=3$ steht für D, A, CH) und `bcd` für den Verlag. Die Prüfziffer `p` wird so gewählt, dass gilt:
$$10a+9b+8c+7d+6e+5f+4g+3h+2i+p = 0 \pmod{11}$$
#TODO Berechnungsverfahren von p
## Cäsar-Verschlüsselung
