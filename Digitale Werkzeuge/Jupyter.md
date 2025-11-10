# Jupyter
Jupyter ist eine Notizenformat welches die Integration von Programmcode in die Notizen unterstützt. 
- Die Notizen basieren dabei auf dem Markdown-Format. 
- Jupyter unterstützt mehr als 40 Programmiersprachen, unter anderem Python. 
- Es ist Dateiorientiert, alles wird in die eine quelloffene Datei geschrieben.
- Der Kernel von Jupyter kann über verschiedene Interfaces aufgerufen werden. Siehe [[#JupyterLab]] und [[#JupyterNotebook]].
# JupyterLab
Das browserbasierte Interface für Jupyter Notizbücher.
# JupyterNotebook
Eine installierbare Software als Interface, mit der Jupyter Notizbücher offline erstellt und bearbeitet werden können.
- Der Kernel muss dabei nicht zwingend auf dem selben Gerät installiert sein. Man kann auch einen Jupyter Kernel übers Web einrichten.
# JupyterNotebook in PyCharm
JupyterNotebook lässt sich auch in PyCharm integrieren.
## **1. Was ist ein Jupyter Notebook in PyCharm?**

- Interaktive Python-Datei mit **Code-, Text- und Visualisierungszellen**
- Direkt **in PyCharm geöffnet und ausgeführt**
- Speichert Dateien im `.ipynb` Format
- Vorteil: keine externe Browseroberfläche nötig

---

## **2. Was kann Jupyter in PyCharm?**

- Python-Code direkt ausführen, **Zellweise oder komplett**
- Markdown-Zellen für **Dokumentation** und **Mathematikformeln**
- Diagramme und Grafiken direkt in der IDE anzeigen (`matplotlib`, `seaborn`)
- Nutzung von PyCharm-Features: **Debugger, Git, Virtual Environments**
- **Variablen-Explorer**: Werte von Variablen direkt einsehen
    

---

## **3. Wie erleichtert uns PyCharm Jupyter Notebooks?**

- Kein Browser, alles in **einer IDE**
- **Autocomplete, Syntaxprüfung und Refactoring** für Python-Code
- **Projektintegration**: Zugriff auf Dateien, Libraries und Git-Repositories
- Einfacher Wechsel zwischen Code, Notizen und Ergebnissen

---

## **4. Wie und wo bekomme ich Jupyter in PyCharm?**

- **PyCharm Professional Edition**: Jupyter-Unterstützung integriert
- **Setup in PyCharm**:
    1. Neue `.ipynb` Datei erstellen
    2. Kernel auswählen (z. B. Python 3)
    3. Code ausführen direkt in PyCharm
- **Community Edition**: Notebooks anzeigen, aber **nicht interaktiv ausführen**
- **Extern:** Jupyter über `pip install jupyterlab` und im Browser starten
    

---

## **5. Wie verwende ich Jupyter in PyCharm?**

1. Projekt öffnen → **Datei → Neu → Jupyter Notebook (.ipynb)**
2. **Codezelle erstellen** → schreiben → `Shift+Enter` ausführen
3. **Markdownzelle** für Text und Formeln einfügen
4. **Diagramme und Visualisierungen** direkt unter der Zelle anzeigen lassen
5. **Variablen und Ergebnisse** über den PyCharm-Explorer überprüfen

## 6. Beispiele

###  Beispiel 1: Datenanalyse:

```python
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv("daten.csv")
plt.plot(data["Zeit"], data["Temperatur"])
plt.title("Temperaturverlauf")
plt.show()


```
### Beispiel 2: Mathematische Berechnung

```python
import math
r = 5
fläche = math.pi * r**2
fläche

```

### Beispiel 3: Markdown + Formel

```python
### Kreisfläche
Formel: \( A = \pi \cdot r^2 \)

```
## **7. Vorteile von Jupyter in PyCharm**

-  Alles in einer IDE, **kein Browser nötig**  
- Zugriff auf **Debugger, Git, Libraries**  
-  **Interaktive Entwicklung**: sofortiges Feedback zu Code  
-  **Variableninspektion** direkt in der IDE

---
