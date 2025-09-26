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

# Indirekter Beweis durch Widerspruch
Es gilt $(A \to B) \iff (\bar A \lor B)$ und für die Negation: $\overline{(A \to B)} \iff (A \land \bar B)$ 
## Vorgehensweise
$A$ und $\bar B$ können nicht gemeinsam eintreten, d.h. ein Widerspruch entsteht. 
Es wird gezeigt, dass $\overline{(A \to B)} \iff (A \land \bar B)$ nicht gilt, was bedeutet, dass $(A \to B) \iff (\bar A \lor B)$ gilt.
# Vollständige Induktion
Es soll bewiesen werden, dass für alle $n \in \mathbb{N}$ (oder alle $n \in \mathbb{N}$ mit $n \ge n_0$, wobei $n_0$ die kleinste Zahl für die die Aussage besteht) etwas Gültig ist. 
## Vorgehensweise
1. Induktionsanfang:
   Beweis für das kleinste $n$, für das die Aussage gelten soll, auf [[#Direkter Beweis|direktem Weg]]. 
2. Induktionsbehauptung:
   Aussage gelte für ein festes, aber beliebiges $n$.
3. Induktionsschluss:
   Zeigen, dass wenn die Aussage für $n$ gilt, sie auch für $n+1$ gelten muss (Schluss von $n$ auf $n+1$)
