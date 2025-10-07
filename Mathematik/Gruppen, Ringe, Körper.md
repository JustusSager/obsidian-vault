Voraussetzung:
- [[Elementare Logik]]
# Grundbegriffe
## Verknüpfung
Gegeben ist eine Menge $M$. Eine **Verknüpfung** ordnet je zwei beliebige Elemente $a,b \in M$ genau einem Element $a \circ b \in M$ zu.
$$ (M, \circ) $$
**Beispiel:**
Die Addition in der Menge der ganzen Zahlen $(\mathbb{Z}, +)$ 
**Hinweis:**
- Gibt es in der Menge $M$ eine Verknüpfung, sagt man die Menge $M$ ist **abgeschlossen** bezüglich der Verknüpfung.
## neutrales Element
Das neutrale Element $n \in M$ bezüglich einer Verknüpfung, kann mit allen Elementen der Menge verknüpft werden, ohne Dieses zu verändern.
$$ \forall a \in M : a \circ n = a = n \circ a = $$
**Beispiel:**
In $(\mathbb{Z},+)$ ist das neutrale Element $n = 0$:
	$\forall k \in \mathbb{Z} : k + 0 = k = 0 + k$ 
In $(\mathbb{Z}, \cdot)$ ist das neutrale Element $n = 1$:
	$\forall k \in \mathbb{Z} : k \cdot 1 = k = 1 \cdot k$ 
## Inverse
Zu einer beliebigen Zahl $a \in M$ ist die Invers bezüglich der Verknüpfung eine Zahl $i_a \in M$ für die gilt:
Die Verknüpfung von $a$ und ihrer Inversen $i_a$ ergibt das neutrale Element $n$.
$$ a \cdot i_a = n = i_a \cdot a $$
**Beispiel:**
In $(\mathbb{Q}, +)$ ist für jede Zahl $a \in \mathbb{Q}$ die additive Inverse $i_a = -a$
	$a + i_a = a - a = 0$ wobei $n = 0$ das neutrale Element der Addition.
In $(\mathbb{Q}, \cdot)$ ist für jede Zahl $b \in \mathbb{Q}$ die multiplikative Inverse $i_b = b^{-q}$
	$b \cdot i_b = b \cdot b^{-1} = 1$ wobei $n=1$ das neutrale Element der Multiplikation.
# Gruppe
Eine Menge mit einer Verknüpfung $(G,\circ)$ heißt **Gruppe**, wenn alles folgende gilt:
- das Assoziativgesetz
  Für alle $a,b,c \in G$ gilt: $a \circ (b \circ c) = (a \circ b) \circ c$ 
- es existiert ein neutrales Element $n \in G$
  Es existiert ein $n \in G$, sodass für alle $a \in G$ gilt: $n\circ a = a = a \circ n$ 
- zu jedem $a \in G$ existiert eine Inverse $i_a \in G$
  für alle $a \in G$ existiert ein $i_a \in G$, sodass $a \circ i_a = n = i_a \circ a$ 
## kommutative Gruppe
Gilt zusätzlich das Kommutativgesetz heißt sie **kommutative Gruppe** (oder auch **abelsche Gruppe**).
Für alle $a,b \in G$ gilt: $a \circ b = b \circ a$
# Ring
Eine Menge mit zwei Verknüpfungen $(R, \oplus, \circ)$ heißt **Ring**, wenn alles folgende gilt:
- $(R,\oplus)$ ist eine [[#kommutative Gruppe]]
- In $(R, \circ)$ gilt das Assoziativgesetz
  Für alle $a,b,c \in R$ gilt: $a \circ (b \circ c) = (a \circ b) \circ c$ 
- Das Distributivgesetz gilt
  Für alle $a,b,c \ in R$ gilt: $a \circ (b \oplus c) = (a \circ b) \oplus (a \circ c)$ 
## kommutativer Ring
Gilt zusätzlich noch die Kommutativität in $(R, \circ)$, so heißt $(R, \oplus, \circ)$ **kommutativer Ring**.
Für alle $a,b \in R$ gilt: $a \circ b = b \circ a$ 
## Ring mit Eins
Gibt es zusätzlich noch ein neutrales Element in $(R, \circ)$, so heißt $(R, \oplus, \circ)$ **Ring mit Eins**.
Es gibt ein $n_\circ \in R$ sodass für alle $a \in R$ gilt: $a \circ n_\circ = a$ 
## kommutativer Ring mit Eins
Es gilt die Kommutativität in $(R, \circ)$ (wie bei [[#kommutativer Ring]]) und es gibt ein neutrales Element in $(R, \circ)$ (wie in [[#Ring mit Eins]]) 
Für alle $a,b \in R$ gilt: $a \circ b = b \circ a$ 
Es gibt ein $n_\circ \in R$ sodass für alle $a \in R$ gilt: $a \circ n_\circ = a$ 
# Körper
Eine Menge mit zwei Verknüpfungen $(K, \oplus, \circ)$ heißt **Körper**, wenn alles folgende gilt:
- $(K, \oplus)$ ist eine [[#kommutative Gruppe]] mit neutralem Element $n = 0$
- $(K \setminus \{ n_\oplus \}, \circ)$ ist eine [[#kommutative Gruppe]] mit neutralem Element $n = 1$
- Das Distributivgesetz gilt
  Für alle $a,b,c \in K$ gilt: $a \circ (b \oplus c) = (a \circ b) \oplus (a \circ c)$ 
**Hinweis:**
- hat in einem [[#kommutativer Ring mit Eins|kommutativen Ring mit Eins]] jedes Element $a \in R \setminus \{0\}$ eine multiplikative Inverse, ist der Ring ein Körper.
**Beispiel:**
$(R, +, \cdot)$ ist ein Körper.