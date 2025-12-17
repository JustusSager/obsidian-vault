# Vektoren #TODO
## Grundlagen und Grundbegriffe (Vektoren)
Ein Vektor:
$\overline{v}=\begin{pmatrix} v_1 \\ v_2 \\ ... \\ v_n \end{pmatrix}$
mit $n$ Werten. Die Anzahl der Werte nennt man #TODO
## Rechenoperationen (Vektoren)
### Länge eines Vektors

$|\overline{v}|=|\begin{pmatrix} v_1 \\ v_2 \\ ... \\ v_n\end{pmatrix}|=\sqrt{v_1^2 + v_2^2+...+v_n}$
### Summe von 2 Vektoren

$\overline{v}+\overline{w}=\begin{pmatrix} v_1 \\ v_2 \\ ... \\ v_n \end{pmatrix}+\begin{pmatrix} w_1 \\ w_2 \\ ... \\ w_n \end{pmatrix}=\begin{pmatrix} v_1 + w_1 \\ v_2 + w_2 \\ ... \\ v_n + w_n\end{pmatrix}$
**Voraussetzungen:**
- Die Vektoren sind gleich groß. 
### Skalarmultiplikation
$s \cdot \overline{v}= s \cdot \begin{pmatrix} v_1 \\ v_2 \\ ... \\ v_n \end{pmatrix} =\begin{pmatrix} s \cdot v_1 \\ s \cdot v_2 \\ ... \\ s \cdot v_n \end{pmatrix}$
Graphisch gesehen ist dies eine "Streckung / Verkürzung / Umkehrung" des Vektors
### Vektor zwischen zwei Punkten berechnen
$\overrightarrow{PQ} = Q - P = \begin{pmatrix} Q_1 \\ Q_2 \\ ... \\ Q_n \end{pmatrix} - \begin{pmatrix} P_1 \\ P_2 \\ ... \\ P_n \end{pmatrix} = \begin{pmatrix} Q_1 - P_1 \\ Q_2 - P_2 \\ ... \\ Q_n - P_n \end{pmatrix}$

**Voraussetzungen:**
- Die beiden Punkte haben die selbe Anzahl an Dimensionen
# Matrizen #TODO 

## Grundlagen und Grundbegriffe (Matrizen)

$$\overline{\overline{A}}=\begin{pmatrix} a_{11} & a_{12} & ... & a_{1n} \\ a_{21} & a_{22} & & a_{2n}\\ ... & & ... & \\ a_{m1} & a_{m2} & & a_{mn}\end{pmatrix}$$
- Das Element $a_{ik}$ steht in der Matrix in der $i$-ten Zeile und in der $k$-ten Spalte.
- Die Anzahl der Zeilen $m$ und die Anzahl der Spalten $n$ kennzeichnen den **Typ der Matrix** $(m \times n)$ oder $(m, n)$.
	- wenn $m = n$ handelt es sich um eine **quadratische Matrix**.
- Eine Matrix, die aus einer einzigen Zeile bzw. Spalte besteht, heißt **Zeilenvektor** bzw. **Spaltenvektor**.
## Standardmatrizen
### Identitätsmatrix
Identitätsmatrix (oder auch Einheitsmatrix) ist eine quadratische Matrix mit "1" auf der Hauptdiagonalen und "0" überall sonst. 
$$ \mathbb{I}_n = \begin{pmatrix} 1 & 0 & \dots & 0 \\ 0 & 1 & \dots & 0 \\ \dots & & \dots & \\ 0 & 0 & & 1 \end{pmatrix} $$
## Rechenoperationen (Matrizen)
### Matrizenmultiplikation
Es seien 2 Matrizen $A$ eine $(m,l)$-Matrix und $B$ eine $(l,n)$-Matrix. Das Produkt der Matrizen $C = A \cdot B$ ergibt eine $(m,n)$-Matrix mit: 
$$ c_{ik} = \sum_{j=1} ^l a_{ij} \cdot b_{jk} \quad \text{für} \left\{ \begin{array}{l} i = 1, 2, \dots, m \\ k = 1, 2, \dots, n \end{array} \right.$$
![[matritzenmultiplikation.png]]
**Hinweis:**
- nicht kommutativ
