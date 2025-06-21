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
$$x_{out}=f(h)=f(\bar{x} \cdot \bar{w})=f(\sum_{i=0}^{n} (x_i \cdot w_i))$$
mit $w_0$ als Gewichtung für den konstanten Bias-Input $x_0$.
