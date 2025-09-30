Voraussetzung:
- [[Elementare Logik]]
In Beweisen soll anhand von der Gültigkeit bestimmter Aussagen (den Voraussetzungen) auf die Gültigkeit anderer Aussagen geschlossen werden.
# Direkter Beweis
Es wird anhand der Voraussetzung $A$ die Behauptung $B$ hergeleitet. Es wird also die Gültigkeit von $A \implies B$ gezeigt. 
## Vorgehensweise
Es gilt $A$, daraus $B$ folgern.
## Beispiel
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
# Indirekter Beweis durch Kontraposition
Dadurch dass $A \implies B$ logisch äquivalent ist zu $\bar B \implies \bar A$ lässt sich $A \implies B$ auch durch den indirekten Beweis $\bar B \implies \bar A$ beweisen. Dies ist häufig einfacher als der direkte Beweis $A \implies B$.
## Vorgehensweise
Es gilt $\bar B$, daraus $\bar A$ folgern.
## Beispiel
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
# Indirekter Beweis durch Widerspruch 
Es gilt $(A \to B) \iff (\bar A \lor B)$ und für die Negation: $\overline{(A \to B)} \iff (A \land \bar B)$ 
## Vorgehensweise
$A$ und $\bar B$ können nicht gemeinsam eintreten, d.h. ein Widerspruch entsteht. 
Es wird gezeigt, dass $\overline{(A \to B)} \iff (A \land \bar B)$ nicht gilt, was bedeutet, dass $(A \to B) \iff (\bar A \lor B)$ gilt.
## Beispiel
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
# Vollständige Induktion
Es soll bewiesen werden, dass für alle $n \in \mathbb{N}$ (oder alle $n \in \mathbb{N}$ mit $n \ge n_0$, wobei $n_0$ die kleinste Zahl für die die Aussage besteht) etwas Gültig ist. 
## Vorgehensweise
1. Induktionsanfang:
   Beweis für das kleinste $n$, für das die Aussage gelten soll, auf [[#Direkter Beweis|direktem Weg]]. 
2. Induktionsbehauptung:
   Aussage gelte für ein festes, aber beliebiges $n$.
3. Induktionsschluss:
   Zeigen, dass wenn die Aussage für $n$ gilt, sie auch für $n+1$ gelten muss (Schluss von $n$ auf $n+1$)
## Beispiel
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
