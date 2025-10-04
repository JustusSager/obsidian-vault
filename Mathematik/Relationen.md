Voraussetzung:
- [[Elementare Logik]]
Eine Relation ist eine Beziehung zwischen den Elementen einer **Definitionsmenge** und den Elementen einer **Wertemenge**. 
- $(a,b) \in \mathit{R} \subseteq A\times B$ bedeutet, $a \in A$ steht in Relation $\mathit{R}$ zu $b \in B$.
- statt $(a,b) \in \mathit{R}$ wird auch $a \mathit{R} b$ geschrieben
- Falls $A = B$ sagt man auch $\mathit{R}$ ist eine Relation in $A$ (oder auf $A$).
# Grundbegriffe
## Tupel
Ein Tupel ist ein geordnetes Paar von Elementen. Dabei ist die Reihenfolge relevant. 
- $(a,b) \ne (b,a)$
## Kartesisches Produkt
alle generierbaren Tupel $(a,b)$ von zwei (oder auch nur einer) Mengen.
$$ A \times B = \{ (a,b) | a \in A \land b \in B \}$$ Eine Relation $\mathit{R}$ ist immer eine Teilmenge von $A \times B$ (mit $A$ und $B$ Mengen), also $\mathit{R} \subseteq A \times B$. 
## inverse Relation
Die inverse Relation $\mathit{R}^{-1}$ zu der Relation $\mathit{R} \subseteq A\times B$ ist definiert durch:
$$ \mathit{R}^{-1} = \{ (b,a) \in B \times A | (a,b) \in \mathit{R} \} $$
# Matrizendarstellung
Relationen lassen sich auch als [[Matrizen]] darstellen. Jede Zeile der Matrix steht dabei für ein Element aus der Definitionsmenge und jede Spalte für ein Element aus der Wertemenge. Sie ist definiert durch:
$$ (\mathit{R})_{A \times B} = \left\{ \begin{array}{l} 1 \quad \text{falls $(a,b) \in \mathit{R}$} \\ 0 \quad \text{falls $(a,b) \notin \mathit{R}$)} \end{array} \right.$$
Dabei steht das Element aus der $i$-ten Zeile in Relation zu dem Element aus der $k$-ten Spalte, wenn die Stelle $a_{ik} = 1$. Es besteht keine Relation zwischen den Elementen wenn $a_{ik} = 0$.
