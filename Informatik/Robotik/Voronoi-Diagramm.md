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
