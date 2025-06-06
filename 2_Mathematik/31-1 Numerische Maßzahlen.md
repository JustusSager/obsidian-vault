## Modalwert (Modus)
Der Wert, der in der Diskreten Verteilung am Häufigsten vorkommt.

## Arithmetischer Mittelwert
Bei einer Stichprobe $x_1, x_2, x_3, ... , x_n$ von $n$ Werten:
$$\bar{x} = \frac{1}{n}\sum_{i=1}^n x_i =\frac{x_1+x_2+...+x_n}{n}$$

### gewichteter arithmetischer Mittelwert
Treten die Daten (Werte) $x_k$ mehrfach auf, kann dies durch eine Häufigkeitsverteilung $f(x_k)$ beschrieben werden (z.B. beim Zusammenfassen von Daten in Klassen).
$$\bar{x} = \frac{1}{n}\sum_{k=1}^m (x_k \cdot n_k)=\sum_{k=1}^m (x_k \cdot f(x_k))$$

## geometrischer Mittelwert
$$\bar{x}_{geo}=(\prod_{i=1}^n x_i)^{\frac{1}{n}} = \sqrt[n]{x_1 \cdot x_2 \cdot ... \cdot x_n}$$

## harmonischer Mittelwert
Der harmonische Mittelwert wird bei verhältnisbeschreibenden Problemstellungen (z.B. Durchschnittsgeschwindigkeiten km/h ) verwendet.
$$\bar{x}_{harm}=\frac{\sum_{i=1}^n n_i}{\sum_{i=1}^n (\frac{n_i}{x_i})}$$

## Median (Zentralwert)
Der in der Mitte stehende Wert in einer der Größe nach geordneten Liste.
- Wird bei Problemstellungen mit einzelnen stark abweichenden Datenwerten verwendet.
- Bei einer geraden Anzahl an Daten wird das arithmetische Mittel der beiden Mittleren Datenwerte als Median angenommen.

## Varianz
$$s²=\frac{1}{n-1} \sum_{i=1}^n (x_i-\bar{x})²$$
- wird auch als Streuung bezeichnet
### Varianz der beschreibenden Statistik
$$s²=\frac{1}{n} \sum_{i=1}^n (x_i-\bar{x})²$$

## Standardabweichung
$$s=\sqrt{s²}=\sqrt{\frac{1}{n} \sum_{i=1}^n (x_i-\bar{x})²}$$
- spielt eine zentrale Rolle in der schließenden Statistik.
## mittlerer Fehler des Mittelwerts
$$s_{\bar{x}}=\frac{s}{\sqrt{n}}=\sqrt{\frac{1}{n \cdot (n-1)} \sum_{i=1}^n (x_i-\bar{x})²}$$
- findet in der beschreibenden Statistik seine Anwendung
## Variationskoeffizient
$$V_x=\frac{s}{\bar{x}}$$
- entspricht einer Normierung der Standardabweichung
