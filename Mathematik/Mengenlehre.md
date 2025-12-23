# Grundlegende Mengenoperatoren
## Schnittmenge
die Elemente, die in `A und B` enthalten sind. Siehe auch [[Elementare Logik#UND|UND aus der boolschen Algebra]].
$$A \cap B$$
![[mengenlehre_schnittmenge.png|200]]
## Vereinigung
Die Elemente, die in `A oder B` enthalten sind. Siehe auch [[Elementare Logik#ODER|ODER aus der boolschen Algebra]].
$$A \cup B$$
![[mengenlehre_vereinigung.png|200]]
## Differenz
$A$ ohne $B$. Siehe auch [[Elementare Logik#OHNE|OHNE aus der boolschen Algebra]].
$$A \setminus B$$
![[mengenlehre_differenz.png|200]]
## Symmetrische Differenz
Siehe auch [[Elementare Logik#EX-ODER|EX-ODER aus der boolschen Algebra]].
$$A \Delta B \quad \text{oder} \quad A \operatorname{xor} B$$
![[mengenlehre_symm_differenz.png|200]]
# Relationen
Voraussetzung:
- [[Elementare Logik]]
Eine Relation ist eine Beziehung zwischen den Elementen einer **Definitionsmenge** und den Elementen einer **Wertemenge**. 
- $(a,b) \in R \subseteq A\times B$ bedeutet, $a \in A$ steht in Relation $R$ zu $b \in B$.
- statt $(a,b) \in R$ wird auch $a R b$ geschrieben
- Falls $A = B$ sagt man auch $R$ ist eine Relation in $A$ (oder auf $A$).
## Grundbegriffe
### Tupel
Ein Tupel ist ein geordnetes Paar von Elementen. Dabei ist die Reihenfolge relevant. 
**Hinweis:**
- $(a,b) \ne (b,a)$
### Kartesisches Produkt
alle generierbaren Tupel $(a,b)$ von zwei (oder auch nur einer) Mengen.
$$ A \times B = \{ (a,b) | a \in A \land b \in B \}$$ Eine Relation $R$ ist immer eine Teilmenge von $A \times B$ (mit $A$ und $B$ Mengen), also $R \subseteq A \times B$. 
### inverse Relation
Die inverse Relation $R^{-1}$ zu der Relation $R \subseteq A\times B$ ist definiert durch:
$$ R^{-1} = \{ (b,a) \in B \times A | (a,b) \in R \} $$
## Matrizendarstellung
Relationen lassen sich auch als [[Vektoren, Matrizen#Matrizen TODO|Matrizen]] darstellen. Jede Zeile der Matrix steht dabei für ein Element aus der Definitionsmenge und jede Spalte für ein Element aus der Wertemenge. Sie ist definiert durch:
$$ (R)_{A \times B} = \left\{ \begin{array}{l} 1 \quad \text{falls $(a,b) \in R$} \\ 0 \quad \text{falls $(a,b) \notin R$)} \end{array} \right.$$
Dabei steht das Element aus der $i$-ten Zeile in Relation zu dem Element aus der $k$-ten Spalte, wenn die Stelle $a_{ik} = 1$. Es besteht keine Relation zwischen den Elementen wenn $a_{ik} = 0$.
## Verkettung von Relationen
Zwei Relationen $R \subseteq A \times B$ und  $S \subseteq B \times C$ lassen sich verketten (verknüpfen) zu einer neuen Relation: 
$$ R \circ S = \{ (a,c) \in A \times C | \exists b \in B : (a,b) \in R \land (b,c) \in S \} $$
Die Verkettung lässt sich auch als [[Vektoren, Matrizen#Matrizenmultiplikation|Matritzenmultiplikation]] der Relationen in Matrizendarstellung umsetzen.
**Hinweis:**
- Die Verkettung ist (genauso wie die Matritzenmultiplikation) nicht kommutativ.
## Eigenschaften von Relationen in einer Menge
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
## Identitätsrelation
$$ \mathbb{I}_A = \{ (a,a) | a \in A \} $$
Relation der Elemente in relation mit sich selbst. In Matrizendarstellung wäre es eine [[Vektoren, Matrizen#Identitätsmatrix|Identitätsmatrix]].
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
## Hüllen
### transitive Hülle
Die transitive Hülle einer Relation $R$ ist die kleinste transitive Relation, die $R$ enthält.
$$[R]^\text{trans} = R \cup R \circ R \cup R \circ R \cup \dots$$
### reflexive Hülle
Die reflexive Hülle einer Relation R ist die kleinste reflexive Relation, die R enthält.
$$ [R]^\text{reflex} = [R]^\text{ref} = R \cup \mathbb{I}_A $$
### symmetrische Hülle
Die symmetrische Hülle einer Relation R ist die kleinste symmetrische Relation, die R enthält.
$$ [R]^\text{sym} = R \cup R^{-1} $$
# Gruppen, Ringe, Körper
## Grundbegriffe
### Verknüpfung
Gegeben ist eine Menge $M$. Eine **Verknüpfung** ordnet je zwei beliebige Elemente $a,b \in M$ genau einem Element $a \circ b \in M$ zu.
$$ (M, \circ) $$
**Beispiel:**
Die Addition in der Menge der ganzen Zahlen $(\mathbb{Z}, +)$ 
**Hinweis:**
- Gibt es in der Menge $M$ eine Verknüpfung, sagt man die Menge $M$ ist **abgeschlossen** bezüglich der Verknüpfung.
### neutrales Element
Das neutrale Element $n \in M$ bezüglich einer Verknüpfung, kann mit allen Elementen der Menge verknüpft werden, ohne Dieses zu verändern.
$$ \forall a \in M : a \circ n = a = n \circ a = $$
**Beispiel:**
In $(\mathbb{Z},+)$ ist das neutrale Element $n = 0$:
	$\forall k \in \mathbb{Z} : k + 0 = k = 0 + k$ 
In $(\mathbb{Z}, \cdot)$ ist das neutrale Element $n = 1$:
	$\forall k \in \mathbb{Z} : k \cdot 1 = k = 1 \cdot k$ 
### Inverse
Zu einer beliebigen Zahl $a \in M$ ist die Invers bezüglich der Verknüpfung eine Zahl $i_a \in M$ für die gilt:
Die Verknüpfung von $a$ und ihrer Inversen $i_a$ ergibt das neutrale Element $n$.
$$ a \cdot i_a = n = i_a \cdot a $$
**Beispiel:**
In $(\mathbb{Q}, +)$ ist für jede Zahl $a \in \mathbb{Q}$ die additive Inverse $i_a = -a$
	$a + i_a = a - a = 0$ wobei $n = 0$ das neutrale Element der Addition.
In $(\mathbb{Q}, \cdot)$ ist für jede Zahl $b \in \mathbb{Q}$ die multiplikative Inverse $i_b = b^{-q}$
	$b \cdot i_b = b \cdot b^{-1} = 1$ wobei $n=1$ das neutrale Element der Multiplikation.
## Gruppe
Eine Menge mit einer Verknüpfung $(G,\circ)$ heißt **Gruppe**, wenn alles folgende gilt:
- das Assoziativgesetz
  Für alle $a,b,c \in G$ gilt: $a \circ (b \circ c) = (a \circ b) \circ c$ 
- es existiert ein neutrales Element $n \in G$
  Es existiert ein $n \in G$, sodass für alle $a \in G$ gilt: $n\circ a = a = a \circ n$ 
- zu jedem $a \in G$ existiert eine Inverse $i_a \in G$
  für alle $a \in G$ existiert ein $i_a \in G$, sodass $a \circ i_a = n = i_a \circ a$ 
### kommutative Gruppe
Gilt zusätzlich das Kommutativgesetz heißt sie **kommutative Gruppe** (oder auch **abelsche Gruppe**).
Für alle $a,b \in G$ gilt: $a \circ b = b \circ a$
## Ring
Eine Menge mit zwei Verknüpfungen $(R, \oplus, \circ)$ heißt **Ring**, wenn alles folgende gilt:
- $(R,\oplus)$ ist eine [[#kommutative Gruppe]]
- In $(R, \circ)$ gilt das Assoziativgesetz
  Für alle $a,b,c \in R$ gilt: $a \circ (b \circ c) = (a \circ b) \circ c$ 
- Das Distributivgesetz gilt
  Für alle $a,b,c \ in R$ gilt: $a \circ (b \oplus c) = (a \circ b) \oplus (a \circ c)$ 
### kommutativer Ring
Gilt zusätzlich noch die Kommutativität in $(R, \circ)$, so heißt $(R, \oplus, \circ)$ **kommutativer Ring**.
Für alle $a,b \in R$ gilt: $a \circ b = b \circ a$ 
### Ring mit Eins
Gibt es zusätzlich noch ein neutrales Element in $(R, \circ)$, so heißt $(R, \oplus, \circ)$ **Ring mit Eins**.
Es gibt ein $n_\circ \in R$ sodass für alle $a \in R$ gilt: $a \circ n_\circ = a$ 
### kommutativer Ring mit Eins
Es gilt die Kommutativität in $(R, \circ)$ (wie bei [[#kommutativer Ring]]) und es gibt ein neutrales Element in $(R, \circ)$ (wie in [[#Ring mit Eins]]) 
Für alle $a,b \in R$ gilt: $a \circ b = b \circ a$ 
Es gibt ein $n_\circ \in R$ sodass für alle $a \in R$ gilt: $a \circ n_\circ = a$ 
## Körper
Eine Menge mit zwei Verknüpfungen $(K, \oplus, \circ)$ heißt **Körper**, wenn alles folgende gilt:
- $(K, \oplus)$ ist eine [[#kommutative Gruppe]] mit neutralem Element $n$
- $(K \setminus \{ n_\oplus \}, \circ)$ ist eine [[#kommutative Gruppe]] mit neutralem Element $n$
- Das Distributivgesetz gilt
  Für alle $a,b,c \in K$ gilt: $a \circ (b \oplus c) = (a \circ b) \oplus (a \circ c)$ 
**Hinweis:**
- hat in einem [[#kommutativer Ring mit Eins|kommutativen Ring mit Eins]] jedes Element $a \in R \setminus \{0\}$ eine multiplikative Inverse, ist der Ring ein Körper.
**Beispiel:**
$(R, +, \cdot)$ ist ein Körper.
