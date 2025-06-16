numpy wird hauptsächlich zur Berechnung von/mit Vektoren und Matrizen verwendet. Siehe hierzu den Mathematischen Ansatz unter [[Vektoren]] und [[Matrizen]].
# Basics
``` python
import numpy as np

# Array erstellen
arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([  # beliebig viele dimensionen möglich
	[1, 2, 3, 4],
	[5, 6, 7, 8]
])

# Daten zum array ausgeben
print(arr1)  # Array ausgeben
print(arr1[0])  # nulltest Element des Arrays ausgeben
print(arr2[0][0])  # bei mehreren Dimensionen so
print(arr2[0, 0])  # oder so

print(arr2.ndim)  # Dimension des arrays, hier 2
print(arr2.shape)  # From des Arrays ausgeben, hier (2, 4)
```

# Platzhalter Arrays/Matrizen
``` python
import numpy as np

array_shape = (3, 2)  # From der Matrix
arr1 = np.zeros(array_shape)  # Matrix mit 0 gefüllt
arr2 = np.ones(array_shape)  # Matrix mit 1 gefüllt
arr3 = np.full(array_shape, 5)  # Matrix mit 5 gefüllt

arr4 = np.eye(3)  # Identitätsmatrix Größe 3

# gleichmäßig steigende Werte im Array (in Abhängigkeit zur Größe des Arrays)
number_of_samples = 10
start_value = 0
end_value = 2
arr5 = np.linspace(start_value, end_value, number_of_samples) 

# gleichmäßig steigende Werte im Array (in Abhängigkeit zur Schrittgröße)
step_size = 0.25
start_value = 0
end_value = 2
arr6 = np.arange(start_value, end_value, step_size) # Endwert ist nicht enthalten im Array

# zufällige Werte im Array / in der Matrix (Gauss Verteilung)
standard_deviation = 0.2
arr7 = np.random.normal(scale=standard_deviation, size=array_shape)

# zufällige Werte im Array / in der Matrix (Normal Verteilung)
arr8 = np.random.randn(*array_shape)
	# durch '*' wird die array_shape entpackt in ihre einzelnen Werte

# Optional: den seed für die zufälligen Berechnungen setzen
seed_value = 2 # selber seed führt zu selber "zufälliger" Zahl
np.random.seed(seed_value)
```

# Rechnen mit Arrays / Matrizen
``` python
import numpy as np

arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.array([6, 7, 8, 9, 10])

# Summe (Arrays müssen gleiche Form haben)
arr3 = arr1 + arr2
arr3 = np.sum(arr1, arr2)

# Subtraktion (Arrays müssen gleiche Form haben)
arr4 = arr1 - arr2
arr4 = np.subtract(arr1, arr2)

# Multiplikation (Arrays müssen gleiche Form haben)
arr5 = arr1 * arr2
arr5 = np.multiply(arr1, arr2)

# Division (Arrays müssen gleiche Form haben)
arr6 = arr1 / arr2
arr6 = np.divide(arr1, arr2)

# Kreuzprodukt (Arrays müssen gleiche Form haben)
arr7 = np.dot(arr1, arr2)
```

## Aggregation
``` python
import numpy as np

arr1 = np.array([1, 2, 3, 4, 5])
i = arr1.sum()  # Summe der Elemente
```

# Elementweise Funktionen ausführen
``` python
import numpy as np  
  
# Define a simple function  
def square(x):  
    return x ** 2  
  
# Create a NumPy array  
arr = np.array([1, 2, 3, 4, 5])  
  
# Apply the function using numpy.vectorize  
vectorized_square = np.vectorize(square)  
result = vectorized_square(arr)  
  
print("Original Array:", arr)  
print("Squared Array:", result)
```
