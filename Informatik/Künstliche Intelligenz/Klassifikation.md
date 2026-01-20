Tags: #Informatik #KI 
# linear separierbar (Grundidee)
Ein erster Lösungsansatz ist sie anhand einer Geraden zu trennen. Am einfachsten vorzustellen, wenn es nur 2 Eigenschaften gibt und diese in einem Graphen dargestellt werden. Dort kann man sehr einfach verstehen, dass diese beiden Kategorien durch eine lineare Funktion separierbar sind.
$$ax_1+bx_2=c$$
$$P(x) = 
\begin{cases} 1 \quad \text{falls}\ ax_1+bx_2 > c \\
0 \quad \text{sonst}
\end{cases}$$
![[Pasted image 20251229125924.png]]
Diese Idee funktioniert auch mit mehr als zwei Dimensionen / Eigenschaften. Dann wird die lineare Funktion zu einer Hyperebene.
Sind die zwei Klassen durch eine lineare Funktion (oder eine Hyperebene) separierbar, nennt man sie **linear separabel**.
# Support Vektor Machine 