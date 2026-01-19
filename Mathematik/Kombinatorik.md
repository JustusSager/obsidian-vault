#Mathematik
# Permutation
- Anordnung von allen $n$ Elementen in einer bestimmten Reihenfolge
## Alle Elemente sind verschieden
- Anzahl der Permutationen von $n$ <b>verschiedenen</b> Elementen
$$P_n=n!=1 \cdot 2 \cdot 3 \cdot (...) \cdot n$$

### Beispiel
Wie viele Möglichkeiten gibt es 6 verschiedene Ziffern in einer Reihe anzuordnen?
$$P_6=6!=1 \cdot 2 \cdot 3 \cdot 4 \cdot 5 \cdot 6=720$$ 

## Es existieren gleiche Elemente
- Von den $n$ Elementen sind $n_1$, $n_2$, $n_3$, ... Elemente gleich.
$$P_n^{(n_1, n_2, ..., n_k)}={n! \over n_1! \cdot n_2! \cdot (...) \cdot n_k!}$$

### Beispiel
Wir haben die Elemente $a$, $b$, $b$, $c$, $c$, $c$. Also 6 Elemente, unter denen einmal 2 Gleiche und einmal 3 Gleiche sind.
$$P_6^{(2, 3)}={6! \over 2! \cdot 3!}=60$$
# Variation
- Es werden $k$ Elemente aus einer Grundmenge von $n$ Elementen rausgegriffen.
- Die Reihenfolge wird berücksichtigt, d.h. $ba \neq ab$.

## Variation mit Wiederholung
- Elemente $k$ werden zurückgelegt / können beliebig oft vorkommen.
- In diesem Fall kann $k>n$ sein.
$$V_n^k=n \cdot n \cdot (...) \cdot n=n^k$$ 
## Variation ohne Wiederholung
- Die Elemente können nur einmal auftreten.
- In diesem Fall muss $k \leq n$ sein.
$$V_n^k=n \cdot (n-1) \cdot (n-2) \cdot (...) \cdot (n-(k-1))={n! \over (n-k)!}$$

# Kombination
- Es werden $k$ Elemente aus einer Grundmenge von $n$ Elementen herausgegriffen.
- Die Reihenfolge wird nicht berücksichtigt, d.h. $ab = ba$.

## Kombination ohne Wiederholung
- Die Elemente können nur einmal auftreten.
- In diesem Fall muss $k \leq n$ sein.
$$C_n^k={1 \over k!} \cdot V_n^k={n! \over (n-k)! \cdot k!}={n \cdot (n-1) \cdot (n-2) \cdot (...) \cdot (n-(k-1)) \over 1 \cdot 2 \cdot 3 \cdot (...) \cdot k}=\begin{pmatrix} n \\ k \end{pmatrix}$$
$$\begin{pmatrix} n \\ k \end{pmatrix} \overset{\wedge}{=} Binomialkoeffizient$$

## Kombination mit Wiederholung
- Elemente $k$ werden zurückgelegt / können beliebig oft vorkommen.
- In diesem Fall kann $k>n$ sein.
$$C_n^k=\begin{pmatrix} m \\ k \end{pmatrix}={m! \over (m-k)! \cdot k!)}={(n+k-1) \cdot (n+k-2) \cdot (...) \cdot (n+1) \cdot n \over 1 \cdot 2 \cdot 3 \cdot (...) \cdot k}=\begin{pmatrix} n+k-1 \\ k \end{pmatrix}$$
$$m=n+k-1$$
