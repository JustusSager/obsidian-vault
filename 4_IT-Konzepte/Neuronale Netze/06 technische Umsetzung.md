# Neuronen
Ein Neuronales Netzwerk besteht aus einer Menge an Neuronen. Diese Neuronen sind miteinander Verbunden, modelliert durch logische Kanäle, denen jeweils eine Gewichtung zugeordnet ist, welche als die "Stärke" der Verbindung verstanden werden kann (`synaptic efficacy`).
Ein Neuron kann mehrere Inputs $x_i$ haben, mit jeweils einer Gewichtung $w_i$.
- $w_i \gt 0$: `excitatory connection`
- $w_i \lt 0$ `inhibitory connection`
- $w_i = 0$: `no connection`
![[neuron.png]]
Der Ausgangswert $y$ des Neurons berechnet sich dann durch:
$$x_{out}=f(h)=f(\bar{x} \cdot \bar{w}-\theta)=f(\sum_{i=1}^{n} (x_i \cdot w_i) - \theta)$$
mit den Parametern:
- $\bar{x}$: input-Vektor
- $\bar{w}$: Gewichtungs-Vektor
- $\theta$: Bias / Threshold
- $f()$: [[Activation Functions|Activation function]]

Der Eingabevektor $\bar{x}$ kann sowohl von anderen Neuronen als auch direkt von den Eingabeparametern des Modells kommen. Die Ausgabe $y$ geht entweder zu einem anderen Neuron oder ist ein Ausgabeparameter des Modells.

## Bias / Threshold - Alternative Umsetzung
Der Bias kann auch über eine konstante Eingabe $x_0 = 1$ und einer dazugehörigen Gewichtung $w_0 = - \theta$ umgesetzt werden. Dadurch vereinfacht sich die obere Formel zu:
$$y=f(h)=f(\bar{x} \cdot \bar{w})=f(\sum_{i=0}^{n} (x_i \cdot w_i))$$
mit $w_0$ als Gewichtung für den konstanten Bias-Input $x_0$.

## Perceptron
Ein Perceptron ist eine Variante eines Neurons, bei der $y$ nur $0$ oder $1$ entspricht je nachdem ob:
$$
\begin{align}
  f(x) = \left\{
    \begin{array}{l}
      1 \quad \text{if $\sum_{i=1}^n w_i \cdot x_i \geq 0$}\\
      0 \quad \text{otherwise}
    \end{array}
  \right.
\end{align}
$$
Damit realisieren Perceptrons bool'sche Funktionen.

# single layer perceptron
## lineare Unterteilbarkeit
Zweit Mengen an Punkten sind Linear unterteilbar wenn es eine Menge an Gewichtungen $w_q, ... , w_n, \theta$ gibt, so dass
- $\sum_{i=1}^n w_i \cdot x_i \geq \theta$ für all Punkte in $(x_1, ... , x_n) \in A$
- $\sum_{i=1}^n w_i \cdot x_i \lt \theta$ für all Punkte in $(x_1, ... , x_n) \in B$
![[linear_seperable.png]]
geteilt durch die lineare Funktion
$$w_1 \cdot x_1 + w_2 \cdot x_2 = \theta$$
bzw.
$$x_2 = -\frac{w_1}{w_2} \cdot x_1 + \frac{\theta}{w_2}$$
### Im 3-Dimensionalen
Ähnlich funktioniert das auch bei einem 3-Dimensionalem Raum, hier ist es jedoch unterteilt durch eine Ebene statt einer Geraden.
$a \cdot x + b \cdot y + c \cdot z = d$
$w_1 \cdot x_1 + w_2 \cdot x_2 + w_3 \cdot x_3 = \theta$
