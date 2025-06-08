In einem Neuronalen Netzwerk wird ein Netzwerk von Neuronen simuliert, angelehnt an dem biologischen Netzwerk von Neuronen, z.B. in einem Gehirn. 
Diese simulierten Neuronen haben eine vordefinierte Anzahl von Eingangswert und einen Ausgangswert. Innerhalb des Neurons werden die Eingangswerte verarbeitet und daraus ein Ausgangswert berechnet. Die Eingangswerte können von einer äußeren Quelle kommen (wie die in das Netzwerk gefütterten Werte) oder von anderen Neuronen. Dadurch entsteht ein Netzwerk von miteinander verknüpften Neuronen.

# Verwendungszweck
- Verständnis von biologischen Netzwerken
- Problemlösung mithilfe von selbstlernenden Algorithmen
	- Bilderkennung
	- Text-to-Speech, Speech-to-Text
	- Autonome Systeme
	- Industrieprozessoptimierung
	- Filtern, Klassifizieren von Daten
	- Datenanalyse

# Einführung anhand eines Beispiels
Quelle: `How to Create a Neural Network (and Train it to Identify Doodles)` von Sebastian Lague (https://www.youtube.com/watch?v=hfMk-kjRv4c)

Zwei scheinbar identische Früchte, eine ist giftig und eine nicht. Bei genauerer Betrachtung, lässt sich feststellen das es primär 2 Kriterien gibt, anhand von denen sich die Früchte unterscheiden.
![[neural_network_fruits.png|300]]
Die Größe der orangen Flecken und die Länge der Stacheln.
Diese Daten lassen sich nun auf einem Graphen darstellen.
#TODO Beispiel vervollständigen oder alternativ das Beispiel aus der Vorlesung.



# `Deep learning` vs Standard `machine learning`
Beim `machine learning` werden die zu Features eines Objekts anhand von denen Klassifiziert werden soll händisch definiert.
Beim `deep learning` entscheidet ein selbstlernender Algorithmus, welche Features welchen Einfluss auf das Endergebnis haben.

# Beispiel Fischklassifizierung
#TODO Beispiel Fischklassifizierung

# Neuronales Netzwerk aufgebaut in Schichten
In diesem Beispiel werden die Neuronen in Schichten aufgebaut. Das heißt das Neuronalen Netzwerk besteht aus einer festen Anzahl an Schichten, welche wiederum aus einer festen Anzahl an Neuronen bestehen. Die Neuronen der ersten Schicht sind jeweils alle Verbunden mit jedem einzelnen Neuron der nächsten Schicht.
![[neural_network.png]]

## Layer
### `Input layer`
In dem `input layer` werden die Werte die dem Neuronalen Netzwerk zur Verfügung stehen reingefüttert. 
Die Anzahl der Neuronen im `input layer` ist bestimmt durch die Anzahl der Werte die dem Neuronalen Netzwerk zur Verfügung stehen. Z.B. Bei einem Schwarz-Weiß-Bild mit 20x20 Pixeln beträgt die Anzahl der `input`-Neuronen $20 \cdot 20 = 400$, wobei jedes `input`-Neuron für einen Schwarz-Weiß-Wert eines Pixels steht.
Die Neuronen im `input layer` sind jedoch nicht zu Vergleichen mit den Neuronen in den anderen Layern, da hier keine Verarbeitung der Werte stattfindet, sondern diese nur als Zugriffspunkt für die Werte dienen.
 
### `Hidden layer`
Die `hidden layer` werden von dem Neuronalen Netzwerk für die Verarbeitung der Werte verwendet. Hier passiert die Mathematik / Magie eines Neuronalen Netzwerks.
Es kann mehrere hintereinander geschaltete `hidden layer` geben.

### `Output layer`
In dem `output layer` findet ein letztes mal eine Verarbeitung der Werte des letzten `hidden layers` statt. Danach werden die Ergebnisse ausgegeben. 
Typischerweise gibt es so viele Neuronen im `output layer` wie Möglichkeiten die Eingabe zu klassifizieren. Z.B. wenn die Eingabe ein Bild ist und entschieden werden soll, ob es sich um einen Hund oder eine Windmühle auf dem Bild handelt, gibt es zwei `output`-Neuronen, jeweils eine für die entsprechende Klassifizierung. 