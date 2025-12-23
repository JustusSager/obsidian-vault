# Aussage
Ein Satz bei dem eindeutig gesagt werden kann, ob er wahr oder falsch ist. Aussagen können auch negiert oder miteinander verknüpft werden.
## Operatoren (von Aussagen)
### Negation
Verneinung einer [[#Aussage]].
$\bar{A}$ oder $\neg A$
### UND
Ist genau dann wahr wenn beide Aussagen A und B wahr sind.
$A \land B$ oder $A \cdot B$
### ODER
Ist dann wahr wenn einer der beiden (oder beide) Aussagen wahr sind.
$A \lor B$ oder $A + B$
### OHNE
Ist genau dann wahr, wenn A wahr und B falsch ist.
$A \setminus B$ 
### EX-ODER
Ist dann wahr wenn genau eine der beiden Aussagen wahr ist.
$\dots$ oder $A \oplus B$ (oder $A \operatorname{xor} B$)
### Subjunktion
Ist eine Aussage, deren Wahrheitswert von A und B abhängt. 
Ist nur dann falsch, wenn $A$ wahr ist und $B$ falsch.
Nicht zu verwechseln mit [[#Implikation]], wenn auch quasi das selbe, nur das es bei der Subjunktion um den Wert einer Aussage geht und nicht um den Zusammenhang zwischen zwei Aussagen.
$A \to B$ 
### Bijunktion
Ist eine Aussage, deren Wahrheitswert von A und B abhängt. 
Ist genau dann wahr, wenn $A$ und $B$ wahr sind, oder wenn $A$ und $B$ falsch sind (Beide gleich sind). 
Nicht zu verwechseln mit [[#Äquivalenz]], wenn auch quasi das selbe, nur das es bei der Bijunktion um den Wert einer Aussage geht und nicht um den Zusammenhang zwischen zwei Aussagen.
$A \operatorname{hier sollte ein doppelseitiger einfacher Pfeil sein, aber gibts nicht} B$ 
### Implikation
Relation zwischen zwei Aussagen, welche immer nur genau dann falsch ist, wenn $A$ wahr ist und $B$ falsch.
Wird fälschlicherweise häufig wie eine [[#Subjunktion]] verwendet. Entspricht einer [[#Subjunktion]] die immer wahr ist.
$A \implies B$ 
### Äquivalenz
Relation zwischen zwei Aussagen, welche immer genau dann wahr ist, wenn beide Aussagen ($A$ und $B$) wahr sind, oder beide Aussagen ($A$ und $B$) falsch sind.
Wird fälschlicherweise häufig wie eine [[#Bijunktion]] verwendet. Entspricht einer [[#Bijunktion]] die immer wahr ist.
$A \iff B$ bedeutet $A \implies B \land B \implies A$ 
### Wahrheitstabelle

| $A$ | $B$ | $A \land B$ | $A \lor B$ | $A \setminus B$ | $A \oplus B$ | $A \to B$ | $A \implies B$ | $A \iff B$ |
| --- | --- | ----------- | ---------- | --------------- | ------------ | --------- | -------------- | ---------- |
| f   | f   | f           | f          | f               | f            | w         | w              | w          |
| f   | w   | f           | w          | f               | w            | w         | w              | f          |
| w   | f   | f           | w          | w               | w            | f         | f              | f          |
| w   | w   | w           | w          | f               | f            | w         | w              | w          |

|                                          | Boolesche Algebra            | Mengenlehre              | Logik                     | Bedeutung                           |
| ---------------------------------------- | ---------------------------- | ------------------------ | ------------------------- | ----------------------------------- |
| Summe bzw. Vereinigung (Disjunktion)     | $A+B$ oder $A \lor B$        | $A \cup B$               | oder                      | A oder B oder beides                |
| Produkt bzw. Schnitt (Konjuktion)        | $A \cdot B$ oder $A \land B$ | $A \cap B$               | und                       | A und B gemeinsam                   |
| Differenz (Subtraktion)                  | $A \setminus B$              | $A \setminus B$          | ohne                      | A ohne die Elemente von B           |
| Symmetrische Differenz (Exklusives Oder) | $A \oplus B$                 | $A \operatorname{xor} B$ | entweder (...) oder (...) | Entweder (A ohne B) oder (B ohne A) |
## 1-Bit Adder

| X   | Y   | Übertrag C | Summe S |
| --- | --- | ---------- | ------- |
| 0   | 0   | 0          | 0       |
| 0   | 1   | 0          | 1       |
| 1   | 0   | 0          | 1       |
| 1   | 1   | 1          | 0       |
Summe S entspricht der logischen Verknüpfung $S=X \oplus Y$
Übertrag C entspricht der logischen Verknüpfung $C=X \cdot Y$
# Aussagenform
Eine Aussagenform $A(x)$ ist ähnlich zu einer [[#Aussage]], nur das sie eine Variable enthält. Sie können mit den selben [[#Operatoren (von Aussagen)|Operatoren]] wie Aussagen verwendet werden und zusätzlich noch mit weiteren.
## Operatoren (von Aussagenformen)
### All-Quantor
Für alle $x$ aus der Menge $M$ ist $A(x)$ wahr.
$\forall x \in M: A(x)$ 
### Existenz-Quantor
Es existiert ein $x$ in $M$, für das $A(x)$ wahr ist.
$\exists x \in M : A(x)$
# Rechenregeln
## Negation von All und Existenz Quantor
$\overline{\forall x \in M:A(x)} \iff \exists x \in M:\overline{A(x)}$ 
$\overline{\exists x \in M:A(x)} \iff \forall x \in M:\overline{A(x)}$ 
## De Morgansche Regeln
$\overline{A + B} \iff \bar A \cdot \bar B$ 
$\overline{A \cdot B} \iff \bar A + \bar B$ 
gilt auch für mehr als 2 Aussagen in Folge.
## idempotent
$A + A = A$
$A \cdot A = A$ 
## kommutativ
$A+B=B+A$
$A \cdot B=B \cdot A$
## assoziativ
$A+(B+C)=(A+B)+C$
$A \cdot (B \cdot C) = (A \cdot B) \cdot C$ 
## distributiv
$A \cdot (B + C) = (A \cdot B) + (A \cdot C)$ 
$A + (B \cdot C) = (A + B) \cdot (A + C)$ 
$+$ und $\cdot$ sind gleichberechtigt (also kein Punkt vor Strich), daher müssen immer Klammern gesetzt werden!
## weitere
$A \setminus B \iff A \cdot \bar B$ 
$A \oplus B \iff (A \setminus B) + (B \setminus A) \iff (A \cdot \bar B) + (B \cdot \bar A)$ 
$(A \implies B) \iff (\bar B \implies \bar A)$ 
$(A \implies B) \iff (\bar A \lor B)$ 
$\overline{(A \implies B)} \iff (A \land \bar B)$ 
# Beweise
Voraussetzung:
- [[Elementare Logik]]
In Beweisen soll anhand von der Gültigkeit bestimmter Aussagen (den Voraussetzungen) auf die Gültigkeit anderer Aussagen geschlossen werden.
## Direkter Beweis
Es wird anhand der Voraussetzung $A$ die Behauptung $B$ hergeleitet. Es wird also die Gültigkeit von $A \implies B$ gezeigt. 
### Vorgehensweise
Es gilt $A$, daraus $B$ folgern.
### Beispiel
Satz: Die Summe von drei aufeinander folgenden $\mathbb{N}$ Zahlen ist durch 3 teilbar.
Aussage A: 
	$a,b,c \in \mathbb{N} \text{ mit } b = a+1, c=a+2$ 
Aussage B: 
	$a,b,c \in \mathbb{N} \text{ ist durch 3 teilbar}$ 
Behauptung: 
	$A \implies B$ 
Vorgehensweise:
1) Voraussetzung: A wird erfüllt.
2) Damit folgt: $$a + b + c = a + (a+1) + (a+2) = a + a + a + 1 + 2 = 3 \cdot a + 3=3 \cdot (a + 1) \in \mathbb{N}$$
   Es ist durch 3 teilbar.
Also gilt: 
	$A \implies B$ 
## Indirekter Beweis durch Kontraposition
Dadurch dass $A \implies B$ logisch äquivalent ist zu $\bar B \implies \bar A$ lässt sich $A \implies B$ auch durch den indirekten Beweis $\bar B \implies \bar A$ beweisen. Dies ist häufig einfacher als der direkte Beweis $A \implies B$.
### Vorgehensweise
Es gilt $\bar B$, daraus $\bar A$ folgern.
### Beispiel
Satz: Für $m \in \mathbb{N}$ gilt: Ist $m²$ gerade, folgt daraus, dass $m$ gerade ist.
Aussage A:
	$m²$ ist gerade
Aussage B:
	$m$ ist gerade
Behauptung:
	$A \implies B$ 
zeige:
	$\bar B \implies \bar A$ 
Vorgehensweise:
1) Voraussetzung wird erfüllt, d.h. $\bar B$ soll wahr sein, also wähle ein ungerades $m \in \mathbb{N}$.
   Frage: Könnte $\bar A$ falsch sein? Also, könnte $A$ eintreten?
2) Annahme der Kontraposition: $\bar B$ ist wahr ($m$ ist ungerade), daher ist $\bar A$ ($m²$ ist ungerade) ebenfalls war
3) $m$ ungerade: $m = 2k+1$ mit $k \in \mathbb{N}$ 
   $m²$ ungerade: $m²=2n+1$ mit $n \in \mathbb{N}$ $$m² = m \cdot m = (2k+1)² = 4k²+4k+1 = 2 \cdot 2 \cdot k² + 2 \cdot 2 \cdot k + 1 = 2 \cdot (2k²+2k) + 1 = 2t + 1$$
   mit $t = 2k²+2k$ 
   Also ist $m² = 2t+1$ wahr und somit ungerade
Wenn $\bar B$ ($m$ ungerade) wahr ist, kann $A$ ($m²$ gerade) nicht wahr sein. D.h. $\bar B \implies \bar A \iff A \implies B$ 
## Indirekter Beweis durch Widerspruch 
Es gilt $(A \to B) \iff (\bar A \lor B)$ und für die Negation: $\overline{(A \to B)} \iff (A \land \bar B)$ 
### Vorgehensweise
$A$ und $\bar B$ können nicht gemeinsam eintreten, d.h. ein Widerspruch entsteht. 
Es wird gezeigt, dass $\overline{(A \to B)} \iff (A \land \bar B)$ nicht gilt, was bedeutet, dass $(A \to B) \iff (\bar A \lor B)$ gilt.
### Beispiel
Satz: Für $m \in \mathbb{N}$ gilt: Ist $m²$ gerade, folgt daraus, dass $m$ gerade ist.
Aussage A:
	$m²$ ist gerade
Aussage B:
	$m$ ist gerade
Behauptung:
	$A \implies B$ 
zeige:
	$\overline{A \land \bar B}$ 
Vorgehensweise:
1) Annahme des Gegenteils: Es gilt $A$ (m² ist gerade) und $\bar B$ ($m$ ist ungerade)
2) $m²$ gerade: $m² = 2n$ mit $n \in \mathbb{N}$ 
   $m$ ungerade: $m=2k+1$ mit $k \in \mathbb{N}$ $$m² = m \cdot m = (2k+1)² = 4k²+4k+1 = 2 \cdot 2 \cdot k² + 2 \cdot 2 \cdot k + 1 = 2 \cdot (2k²+2k) + 1 = 2t + 1$$
   mit $t = 2k²+2k$ 
   Es entsteht ein Widerspruch zur Annahme $A$ da $m² = 2t+1$ wahr und somit ungerade ist.
Da $A \land \bar B$ ein Widerspruch erzeugt ($\overline{A \land \bar B}$) muss die Aussage $A \implies B$ wahr sein.
## Vollständige Induktion
Es soll bewiesen werden, dass für alle $n \in \mathbb{N}$ (oder alle $n \in \mathbb{N}$ mit $n \ge n_0$, wobei $n_0$ die kleinste Zahl für die die Aussage besteht) etwas Gültig ist. 
### Vorgehensweise
1. Induktionsanfang:
   Beweis für das kleinste $n$, für das die Aussage gelten soll, auf [[#Direkter Beweis|direktem Weg]]. 
2. Induktionsbehauptung:
   Aussage gelte für ein festes, aber beliebiges $n$.
3. Induktionsschluss:
   Zeigen, dass wenn die Aussage für $n$ gilt, sie auch für $n+1$ gelten muss (Schluss von $n$ auf $n+1$)
### Beispiel
Satz: Für alle $n \in \mathbb{N}$ gilt: $$\sum_{k=1}^n k² = {1 \over 6} n \cdot (n + 1) \cdot (2n + 1)$$
1) Das kleinste $n$ für das die Aussage gelten soll ist $n_0 = 1$
   $\forall n \in \mathbb{N}:n \ge n_0$ wobei $n_0$ die kleinste Zahl ist. $$\sum_{k=1}^1 k^2 = 1^2 = 1 \iff {1 \over 6} \cdot 1 \cdot (1+1) \cdot (2 \cdot 1 + 1) = {1 \over 6} \cdot 6 = 1$$ d.h. Die Aussage ist für $n_0$ richtig.
2) Annahme: 
   Für ein beliebiges festes $n$ gilt: $$\sum_{k=1} ^n k^2 = {1 \over 6} n \cdot (n+1) \cdot (2n + 1)$$
3) Induktionsschritt: 
   Zeige, dass die Annahme auf für $m = n + 1$ gilt. $$ \sum_{k=1} ^m k^2 = \sum_{k=1} ^{n+1} k^2 = \sum_{k=1} ^{n} k^2 + (n+1)^2$$
   $\sum_{k=1} ^{n} k^2 + (n+1)^2 = {1 \over 6} n \cdot (n+1) \cdot (2n + 1) + (n+1)^2$
   $=(n+1) \cdot ({1 \over 6}n \cdot (2n+1) \cdot (n+1))$ 
   $= {1 \over 6}(n+1) \cdot (n \cdot (2n+1) \cdot 6(n+1))$ 
   $= {1 \over 6}(n+1) \cdot (2n^2+n+6n+6)$ 
   $= {1 \over 6}(n+1) \cdot (2n^2+7n+6)$ 
   $= {1 \over 6}(n+1) \cdot ((n+2)(2n+3))$ 
   $= {1 \over 6}(n+1) \cdot ((n+1+1)(2((n+1)+1))$ 
   $= {1 \over 6}m \cdot (m+1) \cdot (2m+1)$ 
Die Aussage ist richtig.
