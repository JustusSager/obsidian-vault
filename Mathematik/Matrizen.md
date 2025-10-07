Voraussetzungen:
- [[Vektoren]]
#TODO Matrizenrechnung 

# Grundlagen und Grundbegriffe

$$\overline{\overline{A}}=\begin{pmatrix} a_{11} & a_{12} & ... & a_{1n} \\ a_{21} & a_{22} & & a_{2n}\\ ... & & ... & \\ a_{m1} & a_{m2} & & a_{mn}\end{pmatrix}$$
- Das Element $a_{ik}$ steht in der Matrix in der $i$-ten Zeile und in der $k$-ten Spalte.
- Die Anzahl der Zeilen $m$ und die Anzahl der Spalten $n$ kennzeichnen den **Typ der Matrix** $(m \times n)$ oder $(m, n)$.
	- wenn $m = n$ handelt es sich um eine **quadratische Matrix**.
- Eine Matrix, die aus einer einzigen Zeile bzw. Spalte besteht, heißt **Zeilenvektor** bzw. **Spaltenvektor**.
# Standardmatrizen
## Identitätsmatrix
Identitätsmatrix (oder auch Einheitsmatrix) ist eine quadratische Matrix mit "1" auf der Hauptdiagonalen und "0" überall sonst. 
$$ \mathbb{I}_n = \begin{pmatrix} 1 & 0 & \dots & 0 \\ 0 & 1 & \dots & 0 \\ \dots & & \dots & \\ 0 & 0 & & 1 \end{pmatrix} $$
# Operationen
## Matritzenmultiplikation
Es seien 2 Matrizen $A$ eine $(m,l)$-Matrix und $B$ eine $(l,n)$-Matrix. Das Produkt der Matrizen $C = A \cdot B$ ergibt eine $(m,n)$-Matrix mit: 
$$ c_{ik} = \sum_{j=1} ^l a_{ij} \cdot b_{jk} \quad \text{für} \left\{ \begin{array}{l} i = 1, 2, \dots, m \\ k = 1, 2, \dots, n \end{array} \right.$$
![[matritzenmultiplikation.png]]
**Hinweis:**
- nicht kommutativ
