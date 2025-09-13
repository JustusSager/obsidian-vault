In diesem Beispiel sollen 2 Arten von Fischen (Lachs und Barsch) automatisiert sortiert werden. Dazu wird eine Kamera verwendet.

## Physische Unterschiede
Wenn man diese beiden Fischarten vergleicht, lassen sich verschiedene physische Unterschiede feststellen, anhand von denen sie potenziell unterschieden werden können.
- Länge
- Breite
- Helligkeit der Schuppen
- Position des Mundes
- etc.
Diese Unterschiede nennt man Features
### Messfehler
Beim messen dieser Features eines Fisches können jedoch Fehler entstehen. Mögliche Fehlerquellen sind:
- Lichtveränderung
- Position des Fisches unter der Kamera
- etc.
Diese Fehler müssen so gut wie möglich ausgeschlossen werden.

## Erster Ansatz: Länge des Fisches
**Angenommen** man weiß, dass ein Barsch im Schnitt länger ist als ein Lachs
### Mögliche Klassifikation:
1. Es wird eine feste Länge festgelegt, die als `Decision Boundary` dient.
2. Es wird die Länge jedes Fisches gemessen
3. Wenn die Länge den `Threshold` überschreitet -> Barsch
	- Wenn nicht -> Lachs
### Threshold finden
- Möglichst viele Trainingsdaten sammeln
- Länge der (bereits klassifizierten) Fische messen und Messdaten inspizieren
![[bass_salmon_length.png|400]]
Es lässt sich ein Threshold definieren, bei dem der Großteil der Klassifikationen passt, jedoch gibt es immer noch falsche Klassifikationen.

## Zweiter Ansatz (Helligkeit des Schuppen)
Selbe Vorgehensweise wie bei der Länge des Fisches, diesmal wird jedoch die Helligkeit der Schuppen als Maß genutzt.
![[bass_salmon_lightness.png|400]]
Hier lässt sich ein besserer Threshold finden, jedoch gibt es immer noch fehlerhafte Klassifikationen.

### Threshold bei asymmetrischen Kosten
Eine Falschklassifikation kann akzeptabel sein, solange die daraus entstehenden Kosten gering bleiben. Jedoch sind diese Kosten nicht immer symmetrisch. Es kann z.B. vorkommen, dass:
- Kunden einen geringen Anteil an Lachs in ihrer Dose Barsch tolerieren,
	- Entspricht geringen Fehlerkosten
- Jedoch andersherum Barsch in ihrer Dose Lachs nicht toleriert wird.
	- Entspricht hohen Fehlerkosten
Entsprechend muss der Threshold für die Klassifikation von Barsch und Lachs anders definiert werden, als bei symmetrischen Fehlerkosten.

## Dritter Ansatz (beide Features kombinieren)
Um eine noch geringere Falschklassifikation zu erreichen, lassen sich auch mehrere Features des Fisches kombinieren. Diese Features lassen sich dann auch als Feature vector bezeichnen.
$\overline{x}=\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} Länge \\ Helligkeit \end{pmatrix}$

![[bass_salmon_lightness_width.png]]
Eine Klassifikation entspricht jetzt der Unterteilung des `feature space` in zwei Bereiche. Je nachdem auf welcher Seite des Graphen sich die Features des Fisches befinden, würde der Fisch als Barsch oder als Lachs klassifiziert werden.

### `Overfitting`
Die lineare Grenze in der oberen Graphik mit den Trainingsdaten immer noch Falschklassifikationen. Anhand der Trainingsdaten ließe sich eine Linie finden, welche die Trainingsdaten perfekt unterteilt. Diese Linie würde jedoch neue Daten, nicht zwingend besser Klassifizieren, da sie kein generelles Bild über die Features des Fisches beinhaltet, sondern lediglich auf die Trainingsdaten spezialisiert ist.
Das nennt man `Overfitting`. 
Besser wäre eine generelle (wenn auch nicht perfekte) Verallgemeinerung der Daten. Dies muss jedoch nicht zwingend eine Lineare Funktion sein.

## Zentrale Probleme der Mustererkennung
- Es müssen genügend Trainingsdaten vorhanden sein
- Es muss ein genaues Modeldesign existieren
- Es muss eine Verallgemeinerung von unbekannten Mustern stattfinden
- Störfaktoren müssen so gut wie möglich gefiltert werden
- Rechenzeit