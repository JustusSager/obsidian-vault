Beim maschinellen Lernen sollen Computer aus Erfahrung lernen.
# Kategorien
## supervised
Das Vorhersagenmodell wird anhand der input- und der output-Daten entwickelt. Es wird auf ein bestimmtes "target" hintrainiert, welches bekannt ist.
**Beispiel:**
- Bilder klassifizieren, trainiert anhand von bereits klassifizierten Bildern
## unsupervised
Gruppierung und Interpretation der Daten basiert nur auf den input-Daten. Der ML-Algorithmus lernt eigenständig die nützlichen Eigenschaften des Datensatzes, ohne Hilfe von Außerhalb.
**Beispiel:**
- Lerne Wahrscheinlichkeiten/Verteilung mit dem ein Datensatz entstanden ist
- `Clustering`: Gruppierung eines Datensatzes in verschiedene Gruppen mit ähnlichen Eigenschaften
## semi-supervised
Es wird mit einer Mischung von den beiden Oberen Varianten gearbeitet, also der Datensatz, mit dem der ML-Algorithmus trainiert wird, besteht aus bereits klassifizierten und nicht klassifizierten Daten.
## reinforcement learning
Der Algorithmus interagiert aktiv mit einer Umgebung, welches Feedback für die Aktionen liefert.
**Beispiel:**
- Ein Computerspiel beibringen, ohne vorher die Regeln zu erklären

# Typische Aufgaben
## Klassifikation
Es wird ein $n$-Dimensionaler Input-Vektor gegeben und dieser soll einem von $k$ Klassen zugeordnet werden.
$f:\mathbb{R}^n \rightarrow \{1,2,...,K\}$ 
**Beispiel:**
- Bilder klassifizieren
## Regression
Eine Zahl vorhersehen anhand eines $n$-Dimensionalen Input-Vektors
$f: \mathbb{R}^n \rightarrow \mathbb{R}$
**Beispiel:**
- Vorhersage von Aktienpreis
## Transkription
Eine unstrukturierte Darstellung in diskrete Textform umwandeln
**Beispiel:**
- Spracherkennung
## Maschinelle Übersetzung
Eine Folge von Zeichen in einer Sprache in eine Folge von Zeichen einer anderen Sprache übersetzen
## Und viele Weitere#
- "anomaly detection"
- "synthesis"
- "denoising"

# Performance Messung
Um die Fähigkeiten eines Machine Learning Algorithmus zu messen ist eine quantitative Messung von dessen Performance nötig.
## Theoretische Fehlerberechnung
**Mittlerer Fehler**
$P(error)=\int_{-\infty}^\infty P(error,x) dx=\int_{-\infty}^\infty P(error|x) \cdot p(x) dx$
## Empirische Fehlermessung
$\text{(empirical) error rate}=\frac{\text{number of recognition errors}}{\text{number of recognition tests}}$

## Hinweise
- Eine saubere Trennung zwischen Trainings- und Testdaten ist zwingend notwendig
- Wiederholtes Testen mit den selben Daten kann falsche Funktionsfähigkeit vorspielen, da sich das System evtl. speziell auf die Testdaten optimiert hat.
- Wissenschaftliche Objektivität benötigt einen Test mit vorher ungenutzten Testdaten.
- Begrenzung der Menge an Daten -> Cross-Validation
# Overfitting, Underfitting
Ein Algorithmus soll nicht nur mit den Daten gut funktionieren, anhand von denen er trainiert wurde, sondern auch mit Daten die er vorher noch nie gesehen hat. Die Fähigkeit des Algorithmus mit vorher ungesehenen Daten umzugehen nennt man "Generalisierung".
Dafür wird anhand eines Trainingssets der ML-Algorithmus trainiert und anhand des `training errors` optimiert. Zur Überprüfung der Generalisierung wird dann der `test error` anhand von vorher ungesehenen Daten gebildet. 
Ziel ist ein minimaler `generalization error` (bzw. `test error`).
Der `test error` ist dabei im Anschluss größerer oder gleich dem `training error`.

Faktoren, welche die bestimmen wie gut der ML-Algorithmus abschneiden wird, sind dessen Fähigkeiten,
- den `training error` so klein wie möglich zu machen.
- den Abstand zwischen `training error` und `test error` so gering wie möglich zu halten.
### Underfitting
Das Modell ist nicht in der Lage die Fehlerrate klein genug zu bekommen, mit dem genutzten Trainingsset. Das Modell hat Schwierigkeiten Parameter zu finden, die zu geringen Fehlerraten führen.
### Overfitting
Das Modell klassifiziert zwar die Trainingsdaten sehr gut, jedoch ist der Abstand zwischen dem `training error` und dem `test error` sehr groß. D.h. das Modell ist zu sehr auf die Trainingsdaten spezialisiert und nicht gut generalisiert. Es "merkt" sich Trainings-Parameter welche ihn negativ beim Test beeinflussen.
## Cross-Validation
In jeder Iteration wird ein Teil der Daten der Trainingsphase vorenthalten. Danach können diese Daten zum Testzwecken verwendet werden.
![[cross_validation.png]]

# Hyperparameter
Sie werden verwendet um das Verhalten des ML-Algorithmus zu steuern. Diese werden meist nicht von dem Lern-Algorithmus bestimmt. 

# Typischer Ablauf
## 1. Daten sammeln
- Es werden die nötigen Trainings- und Testdaten gesammelt
- Desto mehr desto besser
- Wichtig und teuer
## 2. Features auswählen
- Entscheident für die Performance des Systems
- Optimale Features sind:
	- einfach zu extrahieren
	- resistent gegen nicht relevante Informationen
	- nützlich für die Kategorisierung
- Traditionell basierend auf Vorerfahrung
	- auf Basis von Beispielen oder Expertenwissen
- Heutzutage eher: Erlernen anhand der Daten
	- "end to end" learning
	- integration vom erlernen der Features und der Systemoptimierung
## 3. Modell wählen
Das Modell ist die (mathematische) Beschreibung der zu verwendenden Features
- Beispiel:
	- parametrisierte oder nicht-parametrisierte Technik?
	- MAP-Klassifizierung mit Gauß'scher Verteilung
	- "single or multi-modal?" #TODO was das?
	- Architektur des Neuronalen Netzwerks
- Erfordert viel Erfahrung des System Designers
- In der Praxis häufig: "trial and error"
## 4. Trainingsphase
- Das Modell wird anhand der Daten trainiert, bzw. Die Parameter des Modells werden anhand der Daten bestimmt
## 5. Evaluation
- Die System-Performance wird gemessen
- Evaluation der:
	- bekannten Trainingsdaten
	- unbekannten Testdaten
- Bei der Evaluation sollen Schwachstellen der Modell-Komponenten festgestellt werden