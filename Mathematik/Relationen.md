Voraussetzung:
- [[Elementare Logik]]
Eine Relation ist eine Beziehung zwischen den Elementen einer **Definitionsmenge** und den Elementen einer **Wertemenge**. 
- $(a,b) \in R \subseteq A\times B$ bedeutet, $a \in A$ steht in Relation $R$ zu $b \in B$.
- statt $(a,b) \in R$ wird auch $a R b$ geschrieben
- Falls $A = B$ sagt man auch $R$ ist eine Relation in $A$ (oder auf $A$).
# Grundbegriffe
## Tupel
Ein Tupel ist ein geordnetes Paar von Elementen. Dabei ist die Reihenfolge relevant. 
**Hinweis:**
- $(a,b) \ne (b,a)$
## Kartesisches Produkt
alle generierbaren Tupel $(a,b)$ von zwei (oder auch nur einer) Mengen.
$$ A \times B = \{ (a,b) | a \in A \land b \in B \}$$ Eine Relation $R$ ist immer eine Teilmenge von $A \times B$ (mit $A$ und $B$ Mengen), also $R \subseteq A \times B$. 
## inverse Relation
Die inverse Relation $R^{-1}$ zu der Relation $R \subseteq A\times B$ ist definiert durch:
$$ R^{-1} = \{ (b,a) \in B \times A | (a,b) \in R \} $$
# Matrizendarstellung
Relationen lassen sich auch als [[Matrizen]] darstellen. Jede Zeile der Matrix steht dabei für ein Element aus der Definitionsmenge und jede Spalte für ein Element aus der Wertemenge. Sie ist definiert durch:
$$ (R)_{A \times B} = \left\{ \begin{array}{l} 1 \quad \text{falls $(a,b) \in R$} \\ 0 \quad \text{falls $(a,b) \notin R$)} \end{array} \right.$$
Dabei steht das Element aus der $i$-ten Zeile in Relation zu dem Element aus der $k$-ten Spalte, wenn die Stelle $a_{ik} = 1$. Es besteht keine Relation zwischen den Elementen wenn $a_{ik} = 0$.
# Verkettung von Relationen
Zwei Relationen $R \subseteq A \times B$ und  $S \subseteq B \times C$ lassen sich verketten (verknüpfen) zu einer neuen Relation: 
$$ R \circ S = \{ (a,c) \in A \times C | \exists b \in B : (a,b) \in R \land (b,c) \in S \} $$
Die Verkettung lässt sich auch als [[Matrizen#Matritzenmultiplikation|Matritzenmultiplikation]] der Relationen in Matrizendarstellung umsetzen.
**Hinweis:**
- Die Verkettung ist (genauso wie die Matritzenmultiplikation) nicht kommutativ.
# Relationen in einer Menge
## Eigenschaften
Eine Relation $R$ in einer Menge $A$ heißt:
### reflexiv
$$ \forall a \in A : (a,a) \in R $$
Alle Elemente in der Menge stehen in Relation zu sich selbst.
- Verhindert:
	- irreflexiv
- Identitätsrelation ist immer in der Relation enthalten 
	- $\mathbb{I}_A \subseteq R$ 
	- $R \cup \mathbb{I}_A = R$ 
	- $R \cap \mathbb{I}_A = \mathbb{I}_A$ 
### irreflexiv
$$ \forall a \in A : (a,a) \notin R $$
Keines der Elemente in der Menge steht in Relation zu sich selbst.
Beispiel: Eine Mutter ist nie Mutter von sich selbst.
- Verhindert:
	- reflexiv
- Die Identitätsmatrix ist nie Teil der Relation
	- $R \cap \mathbb{I}_A = \{\}$ 
### transitiv
$$ \forall a,b,c \in A : (a,b) \in R \land  (b,c) \in R \implies (a,c) \in R $$
Wenn a in relation steht zu b und b in relation steht zu c, dann steht auch a in relation zu c.
### symmetrisch
$$ \forall a,b \in A : (a,b) \in R \iff (b,a) \in R $$
Wenn a in relation steht zu b, steht b auch in relation zu a.
Beispiel: Wenn a verheiratet ist mit b, dann ich b auch verheiratet mit a.
- Verhindert:
	- asymmetrisch
	- antisymmetrisch
- Die Inverse der Relation und die Relation sind identisch
	- $R \cup R^{-1} = R = R^{-1}$ 
### asymmetrisch
$$ \forall a,b \in A : (a,b) \in R \implies (b,a) \notin R $$
Wenn a in relation steht zu b, kann b nicht in relation stehen zu a.
- Verhindert:
	- symmetrisch
	- reflexiv
- Implizit auch:
	- antisymmetrisch
	- irreflexiv
- Die Relation ist disjunkt zu ihrer Inverse und beinhaltet nie die Identitätsrelation.
	- $R \cap R^{-1} = \{\}$ 
	- $R \cap \mathbb{I}_A = \{\}$ 
### antisymmetrisch
$$ \forall a,b \in A : (a,b) \in R \land (b,a) \in R \implies a = b $$
oder
$$ \forall a,b \in A | a \ne b : (a,b) \notin R \lor (b,a) \notin R) $$
Wie asymmetrisch, aber es darf auch reflexiv sein.
- Verhindert:
	- symmetrisch
### Identitätsrelation
$$ \mathbb{I}_A = \{ (a,a) | a \in A \} $$
Relation der Elemente in relation mit sich selbst. In Matrizendarstellung wäre es eine [[Matrizen#Identitätsmatrix|Identitätsmatrix]].
## Äquivalenzrelation
ist eine [[#reflexiv|reflexive]], [[#transitiv|transitive]] und [[#symmetrisch|symmetrische]] Relation. 
Beispiel: x wohnt auf der selben Insel wie y.
### Äquivalenzklasse
Eine Äquivalenzklasse ist eine Teilmenge der Menge $A$, deren Elemente $x$ äquivalent sind zu $a$
$$ [a] = \{ x,a \in A | (x,a) \in R \} $$
- Zwei Äquivalenzklassen sind entweder gleich oder disjunkt.
- Die Vereinigung aller Äquivalenzklassen ist $A$ 
## Ordnung
ist eine [[#reflexiv|reflexive]], [[#transitiv|transitive]] und [[#antisymmetrisch|antisymmetrische]] Relation $R$ in einer Menge $A$.
### strikte Ordnung
ist eine Verschärfung der [[#Ordnung]]. Sie ist eine [[#irreflexiv|irreflexive]], [[#transitiv|transitive]] und [[#asymmetrisch|asymmetrische]] Relation $R$ in einer Menge $A$.
**Hinweis:**
- Zu jeder Ordnung existiert auch eine zugehörige strikte Ordnung, indem man alle $(a,a) \in R$-Elemente entfernt.
- Umgekehrt gibt es auch zu jeder strikten Ordnung $S$ auch eine Ordnung $R$ die durch die Vereinigung der strikten Ordnung mit $\{ (a,a) | \text{es gibt ein } x \in A \text{ mit } (a,x) \in R \lor (x,a) \in R \}$.
### Totale Ordnung
Zwei Elemente heißen **vergleichbar** bezüglich der Ordnung $R$ wenn $(a,b) \in R \lor (b,a) \in R$ 
Sind bezüglich einer Ordnung $R$ alle Elemente einer Menge $A$ paarweise vergleichbar, heißt diese **Totale Ordnung**, andernfalls **Partielle Ordnung**.
**Hinweis:**
- Diese Begriffe sind auch für strikte Ordnungen definiert.
# Hüllen
## transitive Hülle
Die transitive Hülle einer Relation $R$ ist die kleinste transitive Relation, die $R$ enthält.
$$[R]^\text{trans} = R \cup R \circ R \cup R \circ R \cup \dots$$
## reflexive Hülle
Die reflexive Hülle einer Relation R ist die kleinste reflexive Relation, die R enthält.
$$ [R]^\text{reflex} = [R]^\text{ref} = R \cup \mathbb{I}_A $$
## symmetrische Hülle
Die symmetrische Hülle einer Relation R ist die kleinste symmetrische Relation, die R enthält.
$$ [R]^\text{sym} = R \cup R^{-1} $$
