Eine ist eine Menge an geordneten Zahlen. Diese gehorchen häufig einem bestimmten Bildungsgesetz.
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
# Grenzwert einer Folge
Der Grenzwert einer Folge ist der Wert den sich die Folge im unendlichen annähert. 
Wenn eine Zahlenfolge einen Grenzwert $g$ besitzt, nennt man sie **konvergent**, andernfalls **divergent**.
$$\lim_{n \to \infty } a_n = g$$ 
## Rechenregeln
$$\lim_{n \to \infty} (a_n \pm C) = \lim_{n \to \infty} a_n \pm$\lim_{n \to \infty} C = a \pm C$$
$$ \lim_{n \to \infty} C \cdot a_n = C \cdot \lim_{n \to \infty} a_n = C \cdot a $$
$$ \lim_{n \to \infty} (a_n \pm b_n) = \lim_{n \to \infty} a_n \pm  \lim_{n \to \infty} b_n = a \pm b $$
$$ \lim_{n \to \infty} (a_n \cdot b_n) = \lim_{n \to \infty} a_n \cdot \lim_{n \to \infty} b_n = a \cdot b$$
$$ \lim_{n \to \infty} \left( {a_n \over b_n } \right) = {\lim_{n \to \infty} a_n \over \lim_{n \to \infty} b_n} = {a \over b} (\text{ falls } b \ne 0)$$
