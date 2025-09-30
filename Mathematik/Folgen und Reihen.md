# Folgen
Eine ist eine Menge an geordneten Zahlen (Gliedern). Diese gehorchen häufig einem bestimmten Bildungsgesetz.
$$\{a_n\}=a_1, a_2, \dots a_n \text{ mit } (n \in \mathbb{N})$$
Bildungsgesetze können z.B. so aussehen:
- über Funktionsgleichungen
	- $a_n={1 \over n}$ beschreibt die Folge $\{ a_1, a_2, a_3, \dots \} = \left\{ 1, {1 \over 2}, {1 \over 3}, {1 \over 4} \right\}$ 
	- $a_n = (-1)^{n} = \begin{cases} 1 & \text{falls } n \text{ gerade} \\ -1 & \text{falls } n \text{ ungerade} \end{cases}$ beschreibt die Folge $\{-1, +1, -1, +1, \dots\}$
	- $a_n = {1 \over 4} \cdot (-1)^n \cdot \left( {1 \over 3} \right) ^{n-1}$ beschreibt die Folge $\left\{ -{1\over 4}, +{1 \over 12}, -{1 \over 36}, \dots \right\}$ 
- über Rekursionsformel
	- $a_n = a_{n-1} + a_{n-2} \text{ für } n \ge 2 \text{ und }a_1 = 1, a_2 = 1$ beschreibt die Fibonacci-Folge $\{a_n\} = \left\{ 1, 1, 2, 3, 5, 8, 13, 21, \dots \right\}$ 
- durch Messung erfasst 
	- z.B. Tagestemperaturen, Wechselkursnotierungen, etc.
## Grenzwert einer Folge
Der Grenzwert einer Folge ist der Wert den sich die Folge im unendlichen annähert. 
Wenn eine Zahlenfolge einen Grenzwert $g$ besitzt, nennt man sie **konvergent**, andernfalls **divergent**.
$$\lim_{n \to \infty } a_n = g$$ 
### Rechenregeln
$$\lim_{n \to \infty} (a_n \pm C) = \lim_{n \to \infty} a_n \pm$\lim_{n \to \infty} C = a \pm C$$
$$ \lim_{n \to \infty} C \cdot a_n = C \cdot \lim_{n \to \infty} a_n = C \cdot a $$
$$ \lim_{n \to \infty} (a_n \pm b_n) = \lim_{n \to \infty} a_n \pm  \lim_{n \to \infty} b_n = a \pm b $$
$$ \lim_{n \to \infty} (a_n \cdot b_n) = \lim_{n \to \infty} a_n \cdot \lim_{n \to \infty} b_n = a \cdot b$$
$$ \lim_{n \to \infty} \left( {a_n \over b_n } \right) = {\lim_{n \to \infty} a_n \over \lim_{n \to \infty} b_n} = {a \over b} (\text{ falls } b \ne 0)$$
## Arithmetische Folge
Es existiert eine Konstante $d  \in \mathbb{R}$, so dass für jedes $n \in \mathbb{N}$ gilt: 
$$a_{n+1} - a_n = d \iff a_{n+1} = a_n + d$$(Die Differenz von zwei aufeinander folgenden Glieder ist immer Gleich)
z.B. $\{1, 6, 11, 16, 21, \dots\} \text{ mit } d = 5$ 
## Geometrische Folge
Es existiert eine Konstante $q \in \mathbb{R}$, so dass für jeder $n \in \mathbb{N}$ gilt:
$$ {a_{n+1} \over a_n} = q \iff a_{n+1} = q \cdot a_n$$ (Quotient zweier aufeinander folgenden Glieder ist immer gleich)
z.B. $\{1, 2, 4, 8, 16, 32, \dots\} \text{ mit } a = 2$ 
# Reihen
Eine Reihe ist die Partialsumme einer Folge.
## Grundbegriffe 
### Partialsumme
Die Summe der ersten $n$ Glieder ist die **Partialsumme** $s_n$.
$$s_n = \sum_{k=1} ^n a_k = s_1 + s_2 + \dots + s_n$$
### (un)endliche Reihe
Die Folge der Partialsummen heißt **endliche Reihe** $\{s_n\}$.
Falls $n \to \infty$ heißt sie **unendliche Reihe**.
**Grenzwert** einer endlichen Reihe ist das letzte Folgenglied der Partialsummenfolge.
### harmonische Reihe $H$
$$ H = \sum_{k=1} ^{\infty} {1 \over k} = 1 + {1 \over 2} + {1 \over 3} + {1 \over 4} + \dots + {1 \over n} + \dots$$
