#Mathematik
# Organisation von Daten
- Zuordnung von Zahlen zu einem Ergebnis oder einer Eigenschaft
- Unterscheidung von qualitativen und quantitativen Merkmalen
- Unterscheidung von stetigen und diskreten Merkmalen
- Unterscheidung von 4 unterschiedlichen Skalentypen
	- Nominal-, Ordinal-, Intervall-, Verhältnisskala
- Bestimmung der zulässigen (mathematischen) Transformationen durch das Skalenniveau 

## Statistische Eigenschaften von Merkmalen
### Qualitative Merkmale
Mit qualitativen Merkmalen kann nicht "gerechnet" werden.
- Merkmale deren Ausprägung (Kategorien) z.B. Namen, Etikettierungen, Bezeichnungen, Eigenschaften, Zahlen sind.
- Merkmale **ohne** rechnerische Operationen anwendbar
- Merkmale können beliebig umgeordnet werden
### Quantitative Merkmale
Mit quantitativen Merkmalen kann gerechnet werden.
- Merkmale, deren Ausprägung reelle Zahlen sind
- Neben einer Ordnungsrelation ist ein fester Abstandsbegriff vorgegeben (Metrik).
### diskrete Merkmale
- Merkmale die nur eindeutige Werte haben, es existieren keine Werte "dazwischen".
**Beispiel:**
- natürliche Zahlen
### stetige Merkmale
- fließende Übergänge von Zahlen.
**Beispiel:**
- reelle Zahlen
## Skalentypen von Merkmalen
![[mathe_skalentypen.png]]
- Das Skalenniveau bestimmt die Möglichkeiten statistischer Verfahren, d.h. je höher das Skalenniveau desto höher der Informationsgehalt.
- Transformation der Daten ist nur auf ein niedrigeres Niveau möglich
- Nominal- und ordinalskalierte Merkmale müssen vor einer Auswertung codiert werden
- Intervall- und Verhältnisskala werden auch als metrische Skalen bezeichnet
### Nominalskala
- geeignet nur für diskrete qualitative Merkmale
- Aussagen über Gleichheit / Verschiedenheit von Merkmalsausprägungen
- Willkürliche Zuordnung der Antworten mit Zahlen (Codierung)
**Beispiel:**
- Geschlecht
- Haarfarbe
- Automarke
### Ordinalskala (Rangskala)
- Geeignet nur für diskrete qualitative Merkmale
- Zusätzlich Größer-Kleiner-Aussagen, damit Ausdruck einer Reihenfolge (Rangordnung) möglich
- Ungleiche Abstände zwischen Merkmalsausprägungen möglich
**Beispiel:**
- Wettkampf-Platzierung
- Schulnoten
### Intervallskala
- Geeignet für diskrete oder stetige quantitative Merkmale
- Wichtigste und häufigste verwendete Skala
- Gleichgroße Intervalle / Abstände zwischen der Codierung
- Abstand zwischen Merkmalsausprägung ist messbar
- Intervallskala hat **keinen** natürlichen Nullpunkt
**Beispiel:**
- Jahreszahlen
- Datumsangaben
- Temperaturangabe in Celsius
### Verhältnisskala (Ratioskala) 
- Geeignet für stetige quantitative Merkmale
- Zusätzliche Existenz eines natürlichen Nullpunktes, lokalisiert, wo die Variable aufhört zu existieren
- Verhältnisse sind (rational) interpretierbar (z.B. 10 cm ist doppelt so lang wie 5 cm)
**Beispiel:**
- Einkommen
- Gewicht
- Reaktionszeit
- Temperaturangaben in Kelvin
# Darstellung von Daten
## Kreuztabellen (Kontingenztabellen)

**absolute Häufigkeit von Kombinationen bestimmter Merkmalsausprägungen:**

|                   | E      | INF    | Wing   | WI     | Sonstige | Summe   |
| ----------------- | ------ | ------ | ------ | ------ | -------- | ------- |
| **3. Semester**   | 35     | 56     | 28     | 34     | 16       | **169** |
| **5. Semseter**   | 18     | 21     | 7      | 9      | 2        | **57**  |
| **> 5. Semester** | 4      | 1      | 3      | 6      | 0        | **14**  |
| **Summe**         | **57** | **78** | **38** | **49** | **18**   | **240** |
Die Tabelle kann auch die **relativen Häufigkeiten** beinhalten.

## Histogramm (Häufigkeitsverteilung):
![[histogramm.png]]
## Kreisdiagramm
![[kreisdiagramm.png]]
## Einteilung in Klassen
#TODO hier weitermachen mit Statistik 1
# Numerische Maßzahlen
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
