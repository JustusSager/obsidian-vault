$$P(x) = \sum_{n=0}^\infty a_n \cdot (x-x_0)^n$$
Kann vereinfacht werden, wenn $x_0 = 0$, zu:
$$P(x) = \sum_{n=0} ^\infty a_n \cdot x^n$$
- $x_0$ ist der **Entwicklungspunkt** (oder das **Entwicklungszentrum**).
# Konvergenz
Eine Potenzreihe ist **konvergent**, wenn:
$$r \gt |x-x_0|$$
**Hinweis:**
- Wenn $r \lt |x-x_0|$ ist die Potenzreihe **divergent**. 
- In den Randpunkten, wenn $r = |x|$, ist **keine allgemeingültige Aussage** möglich. Hier ist eine gesonderte Untersuchung nötig.
- Wenn $r = \infty$, dann ist die Potenzreihe **beständig konvergent**.
## Berechnung des Konvergenzradius zur Potenzreihe P(x):
nach dem Quotientenkriterium:
$$r = \lim_{n \to \infty} \left| {a_n \over a_{n+1}} \right|$$
nach dem Wurzelkriterium:
$$r = {1 \over \overline{ \lim_{n \to \infty} } \sqrt[n]{|a_n|}}$$
### Randpunkte überprüfen
Um den Konvergenzbereich zu bestimmen, die Ungleichung nach $x$ lösen:
$$|x-x_0| < r$$
Am Rand dieses Konvergenzbereiches gibt es immer einen rechten und Linken Grenzpunkt($r_l$ und $r_r$. 
$$\begin{align}
r_l = x_0 - r\\
r_r = x_0 + r
\end{align}$$
Die Grenzpunkte $r_l$ und $r_r$ in die Formel der Potenzreihe für $x$ einsetzten, um zu prüfen, ob es an den Punkten konvergiert oder divergiert:
$$\begin{align}
R_l = \sum_{n=0}^\infty a_n \cdot r_l^n \\
R_r = \sum_{n=0}^\infty a_n \cdot r_r^n
\end{align}$$

