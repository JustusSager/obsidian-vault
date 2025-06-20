Für die Verarbeitung der Inputs von Neuronen gibt es verschiedene "activation functions" 

# ReLu

$$
\begin{align}
  ReLu(x) = \left\{
    \begin{array}{l}
      x \quad \text{if $x \gt 0$}\\
      0 \quad \text{otherwise}
    \end{array}
  \right.
\end{align}
$$

## derivative
$$
\begin{align}
  ReLu_{derivative}(x) = \left\{
    \begin{array}{l}
      1 \quad \text{if $x \gt 0$}\\
      0 \quad \text{otherwise}
    \end{array}
  \right.
\end{align}
$$
## Python Beispiel
``` python
def relu(x):
	if x > 0:
		return x
	else:
		return 0
def relu_derivative(x):
	if x > 0:
		return 1
	else:
		return 0
```

# step function
$$
\begin{align}
  step(x) = \left\{
    \begin{array}{l}
      1 \quad \text{if $x \gt 0$}\\
      0 \quad \text{otherwise}
    \end{array}
  \right.
\end{align}
$$
