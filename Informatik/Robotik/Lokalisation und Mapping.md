#Informatik #Robotik
Bei der Lokalisation soll der Roboter im Raum verortet werden.
# Ortungsverfahren
## Laterationsverfahren
Es wird die Entfernung zu zwei bekannten Landmarken gemessen. Dadurch entsteht ein Gleichungssystem. Eins der Ergebnisse des Gleichungssystems (Eins der beiden Schnittpunkte der Kreise) ist die Position des Roboters.
$(x_1-x_R)^2+(y_1-y_R)^2-d_1^2=0$ 
$(x_2-x_R)^2+(y_2-y_R)^2-d_2^2=0$ 
wobei $(x_R, y_R)$ die unbekannte Roboterposition ist und $(x_1, y_1)$, $(x_2,y_2)$ die bekannten Positionen der Landmarken.
Gleichungssystem lässt sich durch das [[Newton-Verfahren]] lösen
### Least-Square-Verfahren
Zur Verwendung bei einem überbestimmten Gleichungssystem, also mehr Messwerte zu Landmarken als Koordinatenachsen.
$(x_1-x_R)^2+(y_1-y_R)^2-d_1^2=0$
$(x_2-x_R)^2+(y_2-y_R)^2-d_2^2=0$
$(x_3-x_R)^2+(y_3-y_R)^2-d_3^2=0$
$\dots$
Meist gibt es durch Ungenauigkeiten in den Messwerten keine exakte Lösung. Daher wird versucht die Summe der Fehlerquadrate SSE zu minimieren:
$$ \text{SSE} = \sum_{i} [(x_i-x_R)^2+(y_i-y_R)^2-d_i^2]^2 $$
#### Problem
- Bei ungünstiger Geometrie (z.B. 2 Landmarken mit kleinem Schnittwinkel der Kreise) ist die Mehrdeutigkeit schwer auflösbar.
- 
## Koppelnavigation
Die neue Position wird anhand der alten Position und der zurückgelegten Strecke geschätzt. 
# SLAM-Verfahren
Synchrone Lokalisierung und Kartenerstellung
## Landmarkenbasiertes SLAM-Verfahren
**Problemstellung:**
- Roboter exploriert eine unbekannte Umgebung mit festen Landmarken
- Roboter wird durch Steuerdaten $u$ bewegt und es werden Sensordaten $z$ gesammelt
- Gesucht ist die Karte $m$ mit $n$ Landmarken
  $m = l_{1,x}, l_{1,y}, l_{2,x}, l_{2,y}, \dots , l_{n,x}, l_{n,y}$
  und Weg des Roboters
  $x_1, x_2, \dots , x_t$ 
**Schwierigkeit:**
- Sowohl Position der Landmarken als auch gefahrener Weg sind unbekannt
- Kartenfehler und Fehler im Roboterweg sind korreliert
- Die Zuordnung von Sensordaten zu Landmarken ist schwierig, es muss entschieden werden ob Sensordaten zu einer bekannten Landmarke gehören oder eine Neue bildet.
	- Verstärkt durch die Ungenauigkeit der Position der Roboters
**Vorgehensweise:**
Die Karte mit $n$ Landmarken wird durch einen $2n+3$-großen Zustandsvektor und einer Kovarianzmatrix dargestellt.
- Roboter Position: $(x, y, \theta)$ 
- $n$-Landmarken Positionen: $l_i = (x_i, y_i)$ für $1 \le i \le n$ 
- Es können mehrere hundert Landmarken behandelt werden.
$$x_k = \begin{pmatrix}
x \\ y \\ \theta \\ l_1 \\ l_2 \\ \dots \\ l_n
\end{pmatrix}
Kovarianzmatrix = \begin{pmatrix}
\sigma_{x}^2 & \sigma_{xy} & \sigma_{x \theta} & \sigma_{x l_1} & \sigma_{x l_2} & \dots & \sigma_{x l_n} \\ 
\sigma_{xy} & \sigma_{y}^2 \\ 
\sigma_{x \theta} && \sigma_{\theta}^2\\ 
\sigma_{x l_1} &&& \sigma_{l_1}^2 \\ 
\sigma_{x l_2} &&&& \sigma_{l_2}^2\\ 
\dots &&&&& \dots \\ 
\sigma_{x l_n} &&&&&& \sigma_{l_n}^2
\end{pmatrix}
$$
#TODO SLAM-Kovarianzmatrix vervollständigen
# Voronoi-Diagramm
![[voronoi_diagramm.png|300]]
## Vorgehensweise bei der Erstellung
Es kann ein rekursiver Algorithmus verwendet werden um ein Voronoi-Diagramm zu erstellen.
Startbedingung:
- Es existiert eine feste Menge an Punkten.
Vorgehensweise:
1. Bounding Box der Punkte berechnen.
2. Die Bounding Box in der sich die Punkte befinden wird in 2 ca. gleich große Teile geteilt.
3. Falls:
	1. in der Fläche mehr als 2 Punkte sind: 
	   Rekursiv Aufrufen (Start mit Schritt 2)
	2. Falls nur 2 Punkte enthalten sind: 
	    Teilen der Fläche an der Mittelsenkrechten der Verbindungslinie zwischen den 2 Punkten.
		1. Schnittpunkt der Mittelsenkrechten berechnen:
		   $M_x = {x_1 + x_2 \over 2}$ 
		   $M_y = {y_1 + y_2 \over 2}$ 
		2. Steigung der Mittelsenkrechten berechnen 
		   Steigung der Verbindungslinie: $m = {y_2 - y_1 \over x_2 - x_1}$ 
		   Steigung der Mittelsenkrechten: $M_m = -{1 \over m}$ 
		3. Funktionsformel der Mittelsenkrechten bestimmen
		   $M_y = M_m \cdot M_x + b$ nach b auflösen.
4. Verschmelzen der zurückbekommenen 2 Voronoi-Diagramme:
	1. Verbinden der nächsten Nachbarn entlang der Trennungslinie der 2 Flächen.
	2. Einzeichnen und abschneiden der Schnittpunkte der Mittelsenkrechten.
		1. Schnittpunkte zwischen den Mittelsenkrechten berechnen.
		2. Linien an den Schnittpunkten abschneiden.
5. Fertig.
