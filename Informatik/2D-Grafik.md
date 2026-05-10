---
erstellt am:
tags:
  - Informatik
  - Computergraphik
Deckblatt: "[[bild_als_raster.png]]"
---


#Informatik #Computergraphik
# Farben

## Frequenzen und Farbspektrum
Licht ist eine elektromagnetische Welle (oder Teilchen) welches sich ohne Übertragungsmedium übertragen kann. Diese Welle kommt in unterschiedlichen Frequenzen. Ein kleiner Teil des gesamten Spektrums kann als Licht in unterschiedlichen Farben wahrgenommen werden.
![[elektromagnetisches_spektrum.png]]
	Quelle Bild: Von Horst Frank / Phrood / Anony - Horst Frank, Jailbird and Phrood, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=3726606
**Frequenzbereiche der Farben:**
- Blau: 400nm - 500nm
- Grün: 450nm - 630nm
- Rot: 500nm - 700nm
**Licht kann auf verschiedene Weise entstehen:**
- Durch Wärmestrahlung (Sonne, Glühbirne, Lichtbogen)
	- Alles was über 0° Kelvin gibt Strahlung ab
- Durch Umwandlung (Leuchtstoffröhre)
- Durch Halbleitervorgänge (LED)
**Farben werden vom Auge unterschiedlich stark wahrgenommen:**
![[farbwahrnehmung.png]]
	Quelle Bild: Vorlesungsskript des Moduls Computergraphik (Quelle 1)
Stärkste Wahrnehmung bei:
- Maximum S-Zapfen 420nm (violett getöntes blau)
- Maximum M-Zapfen 534nm (türkis getöntes grün)
- Maximum L-Zapfen 564nm (grün getöntes gelb)

## CIE-xy Farbraum
Es sollte die Farbwahrnehmung simulieren. Es wurde durch Spektralzerlegung ein Testlicht erzeugt. Dann wurden rote grüne und blaue Referenzlichter erzeugt und überlagert, wobei die Testperson die Intensität einstellen konnte. 
Relevant, wenn ein Display konstruiert wird oder man die Wiedergabemöglichkeiten verstehen möchte.
![[farbraum_cie-xy.png|300]]
	Quelle Bild: https://de.wikipedia.org/wiki/CIE-Normvalenzsystem 

## Metamerie
Zwei verschiedene Farbspektren können bei einem Menschen den gleichen Farbreiz (Farbvalenz) auslösen, z.B. das weiße Licht einer Leuchtstoffröhre hat ein anderes Farbspektrum als das weiße Licht einer LED. Die blauen, grünen und roten Zapfen im Auge werden jedoch gleichermaßen angeregt.

## Farben digitalisieren

### RGB-Farbsystem
Hierbei wird die Farbe als die 3 Farbkomponenten Rot, Grün und Blau gespeichert. Bei einem Bild werden dabei für jedes Pixel des Bildes diese 3 Komponenten gespeichert.
![[rgb_farbraum.png]]
	Quelle Bild: Vorlesungsskript des Moduls Computergraphik (Quelle 1)

| Rot | Grün | Blau | Farbe   |
| --- | ---- | ---- | ------- |
| 255 | 255  | 0    | Gelb    |
| 0   | 255  | 255  | Cyan    |
| 255 | 0    | 255  | Magenta |
| 255 | 255  | 255  | Weiß    |
Bei einer [[#Farbtiefe]] von 8 Bit pro Farbkanal reichen die Werte von 0 bis 255. Dadurch lassen sich z.B. die oberen Farben (die Eckpunkte des Farbraums) kombinieren. 
Beim RGB-Farbsystem handelt es sich um ein additives Farbsystem, siehe [[#Additive vs. Subtraktive Farbsysteme]]. 
#### Farbtiefe
Die Farbtiefe ist, wie viele Bits für jeden Farbkanal bereitgestellt wird. Je mehr Bits pro Farbkanal zur Verfügung stehen, desto feiner sind die möglichen Abstufungen in den Farben.
Bei zu kleiner Farbtiefe kann ein sog. Banding-Effekt auftreten, ein Bildfehler, bei dem weiche Farb- oder Helligkeitsverläufe als harte, stufenartige Streifen dargestellt werden.

| Name                                | Bittiefe      | Anzahl der Farben            |
| ----------------------------------- | ------------- | ---------------------------- |
| Monochrom (schwarz/weiß)            | 1 Bit         | 2                            |
| Graustufen                          | 8 Bit         | 255                          |
| Next-Workstations                   | 3 x 4 Bit     | 4096                         |
| High Color                          | 5, 6, 5 Bit   | 65.536                       |
| True Color (evtl. zus. Alpha-Kanal) | 3 x 8 Bit     | ca. 16,8 Mio.                |
| Deep Color                          | 3 x 10-16 Bit | Milliarden bis 281 Billionen |
### HSV-Farbsystem
Das Hue-Saturation-Value-Farbsystem erlaubt eine bessere Unterscheidung der Farben. 
- Die Farbe wird hierbei nur durch den Hue angegeben, von 0° bis 360°.
- Saturation gibt die Sättigung (also die Entfernung zu Grau) der Farbe an, von 0% bis 100%.
- Value gibt die Helligkeit der Farbe an, von 0% bis 100%.
![[hsv-farbraum.png| 300]]
	Quelle Bild: https://de.wikipedia.org/wiki/HSV-Farbraum 

### Additive vs. Subtraktive Farbsysteme
![[additive_subtraktive_farbsysteme.png]]
Quelle Bilder : Wikipedia Quark57 und ToBeFree
Die Mischung von Farben kann in weiß oder in schwarz enden. 
Bei Additiven Farbsystemen sorgt eine maximale Aussteuerung jeder Farbe für Weiß. Ein echtes Beispiel dafür wären Scheinwerfer. Das [[#RGB-Farbsystem]] ist z.B. ein additives Farbsystem.
Bei subtraktiven Farbsystemen kommt bei einer maximalen Aussteuerung jeder Farbe Schwarz heraus. Ein echtes Bespiel dafür wären Wasserfarben. Das [[#CMY(K)-Farbsystem]] ist z.B. ein subtraktives Farbsystem

### CMY(K)-Farbsystem
Dieses Farbsystem ist ähnlich dem [[#RGB-Farbsystem]], jedoch aufgeteilt in Cyan, Magenta und Gelb. Diese Farben sind quasi das Gegenteil der RGB-Komponenten. Eine Aussteuerung einer der Komponenten, schwächt die Wahrnehmung des entsprechend gegenüberliegenden Zapfens. Eine Aussteuerung von Magenta, z.B. (dem Anti-Grün, weil alles außer Grün) schwächt die Wahrnehmung des Grün-Zapfens im Auge. 
Die K-Komponente kann dabei ggf. genutzt werden um eine zusätzliche Schwarz-Komponente hinzuzufügen.
Eine Analogie dafür wäre ein Drucker. Hier wird mit einem weißen Blatt gestartet und es können Farbkomponenten hinzugefügt werden, bis man am Ende bei Schwarz ankommt (oder direkt die Schwarzkomponente aufgetragen werden).

# Bilder im Speicher
![[bild_als_raster.png|400]]
Die einfachste Form ein Bild digital zu speichern ist, die Farbwerte als ein 2-dimensionales Raster/Array zu speichern. Für jeden Farb-Kanal (z.B. bei Graustufe nur einer) kann dabei pro Pixel z.B. ein Byte verwendet werden. 
Diese Farbkanäle werden typischerweise als Vektor3 oder Vektor4 gespeichert. Der vierte Wert ist dabei der Alpha-Kanal, z.B. für die Transparenz. Die Reihenfolgen welche Farbe an welcher Stelle des Vektors steht, ist dabei nicht standardisiert, es kommt jede Form mal vor.

Aus effizienzgründen kann statt einem 2-dimensionalen Array auch ein 1-dimensonales Array verwendet werden. Dann wird zusätzlich noch die Information über die Breite des Bildes benötigt.
Um das Kopieren im Speicher zu erleichtern wird nach Bedarf das Bild erweitert
![[padding_eines_bildarrays.png|500]]

Ein Bild im Speicher ist also ein Array an Bytes, welches erst durch weitere zusätzliche Informationen Sinn ergibt. Es wird die
- Höhe und Breite
- Zeilenbreite (stride)
- Format, also z.B. RGB, BGR, BGRA, (...)
benötigt um das Array an Bytes als ein sinnvolles Bild auf dem Bildschirm auszugeben.

#### Code
#TODO 

## Farbpaletten
Statt für jedes Pixel den RGB-Wert zu speichern, kann auch zum Zwecke der Bildkompression eine Farbpalette verwendet werden. Hierfür wird ein Array an möglichen verwendbaren Farben definiert und das Pixel enthält nur noch einen Verweis auf eine bestimmte Stelle in dem Farbpaletten-Array. Diese Farbpalette wird damit als LookupTable (LUT) realisiert.
Der Vorteil hierbei, im Vergleich zu einer geringeren [[#Farbtiefe]] zur Kompression ist, dass hier bestimmte Farben trotzdem eine sehr hohe Auflösung haben können und nur bei bestimmten Farbtönen Speicherplatz gespart wird.
![[farbpalette.png]]

#### Code
``` CS
// Eine Liste mit allen Farben
List<Color> colors = new List<Color>();
// Alle Rottöne zur Liste hinzufügen
for (int i = 0; i < 256; i++) {
	colors.Add(Color.fromArgb(255, (byte) i, 255, 255))
}
// Bitmap Palette anhand der Liste an Farben erstellen
BitmapPalette plt = new BitmapPalette(colors);

// Die Palette wird der Bitmap mit übergeben und der Typ der Pixel wird als Index angegeben
WriteableBitmap wb = new WritableBitmap(width, height, 0, 0, PixelFormats.Indexed8, plt);
```

# Von Aufnahme zu Wiedergabe
![[bilder_von_aufnahme_zu_wiedergabe.png]]
Innerhalb dieser Verarbeitungskette gibt es viele Parameter die die Zwischenergebnisse und das Endergebnis stark beeinflussen.

## Darstellung auf ein OLED-Display
Auf einem OLED-Display besteht jeder Pixel aus 3 bis 4 LEDs, eine Rote , Grüne, Blaue. Ggf. gibt es eine Weiße oder weitere Grüne LED.
Hier unterm Mikroskop:
![[oled_unterm_mikroskop.png]]
Es wird als das [[#Additive vs. Subtraktive Farbsysteme|additive]] [[#RGB-Farbsystem]] verwendet um jede mögliche Farbe darzustellen.
## Bilder drucken
Beim Drucken eines Bildes werden kleine Farbpunkte so dich nebeneinander gesetzt, dass sie ohne Mikroskop aussehen wie eine Farbmischung. 
![[druck_unterm_mikroskop.png]]
Hierbei handelt es sich um ein [[#Additive vs. Subtraktive Farbsysteme|subtraktives Farbsystem]] wie dem [[#CMY(K)-Farbsystem]]. 

## Dynamikumfang eines Bildes
Der Dynamikumfang ist das Verhältnis zwischen Hell und Dunkel eines Bildes. Je nach Wiedergabemedium kann dieser sehr unterschiedliche Ausfallen.
- Normaler Bildschirm 700:1 (bei OLED deutlich mehr)
- Kinoprojektor 2000:1
- Papierdruck 100:1
Das menschliche Auge hat durch die Irisblende jedoch einen deutlich höheren Dynamikumfang von 1.000.000:1.
Der dynamische Umfang muss also an das Medium angepasst werden. Dies kann z.B. über die [[#Gamma-Korrektur]] erreicht werden.

## Luminanz und Luma
Da die Helligkeitswahrnehmung je nach Farbe unterschiedlich stark ausfällt, kann beim konvertieren der Farbe in ein Graustufen-Bild nicht einfach der Mittelwert der drei Farbkanäle verwendet werden. Hierfür wird die Empfindlichkeit der Zapfen im Auge für die unterschiedlichen Farben berücksichtigt. Für die Berechnung eines Pixels kann folgende Formel verwendet werden:
$$𝑌 = 0,2126 ∗ R + 0,7152 ∗ G + 0,0722 ∗ B$$
- $Y$ ist der resultierenden Helligkeitswert.
- $R$ ist die rote Ausprägung des Pixels
- $G$ ist die grüne Ausprägung des Pixels
- $B$ ist die blaue Ausprägung des Pixels

| Original             | Graustufen anhand des Mittelwerts          | Graustufen anhand der korrigierten Helligkeit          |
| -------------------- | ------------------------------------------ | ------------------------------------------------------ |
| ![[Campus.png\|300]] | ![[campus_mittelwert_graustufen.png\|300]] | ![[campus_helligkeitskorrigierte_graustufen.png\|300]] |
Hier ist der Unterschied schwierig zu erkennen, doch die Helligkeitswahrnehmung des dritten Bildes entspricht eher dem Original als dem in der Mitte.

#### Code
Graustufen anhand des Mittelwerts:
``` CS
render_pixels[(x + (y * width))] = (byte) ((
    pixels[(x + (y * width)) * 3 + 0] + 
    pixels[(x + (y * width)) * 3 + 1] + 
    pixels[(x + (y * width)) * 3 + 2]
) / 3);
```
Graustufen anhand der korrigierten Helligkeit:
``` CS
render_pixels[(x + (y * width))] = (byte) (
    0.2126 * pixels[(x + (y * width)) * 3 + 0] + 
    0.7152 * pixels[(x + (y * width)) * 3 + 1] + 
    0.0722 * pixels[(x + (y * width)) * 3 + 2]
);
```

## Gamma-Korrektur
Die Gamma-Korrektur kann verwendet werden, um den scheinbaren Dynamikumfang des Bildes künstlich zu erhöhen. Damit lässt sich die nicht-lineare Lichtwahrnehmung des Auges besser aufgreifen in der Darstellung des Bildes. Das lässt sich mithilfe einer Potenzfunktion realisieren.
$$I_{Ausgabe} = I_{Eingabe}^Y \quad \text{mit} \quad 0 \le I_{Ausgabe} \le 1$$
Oder der Umkehrfunktion:
$$I_{Ausgabe} = I_{Eingabe}^{1 \over Y} \quad \text{mit} \quad 0 \le I_{Ausgabe} \le 1$$
#### Code
``` CS
// render_pixels[i] = I
// gamma_value = Y
// Korrektur wird auf jeden Farbkanal in jedem Pixel angewendet
for (int i = 0; i < render_pixels.Length; i++)
{
    render_pixels[i] = (byte) (Math.Pow((render_pixels[i] / 255.0), gamma_value) * 255);
}
```

## Schwellwertoperation
Es kann auch ein reines Schwarz/Weiß Bild erstellt werden, indem anhand der Helligkeit ein Pixel entweder ganz Schwarz oder ganz Weiß gesetzt wird. Dies kann dann folgendermaßen aussehen:

| Original             | Schwellwertoperation                      |
| -------------------- | ----------------------------------------- |
| ![[Campus.png\|300]] | ![[campus_schwellwertoperation.png\|300]] |
#### Code
``` CS
for (int i = 0; i < render_pixels.Length; i++)
{
    if (render_pixels[i] > schwellwert_value) render_pixels[i] = (byte)(255);
    else render_pixels[i] = (byte)(0);
}
```

# Glossar
### Auflösung
Auflösung kann je nach Kontext etwas anderes bedeuten und ist nicht klar definiert. 
Es kann
- ... die Breite und Höhe des Monitors in Pixeln sein
- ... die Gesamtanzahl der Pixel auf dem Bildschirm oder in einer Kameralinse sein (Megapixel) (steigt quadratisch)
- ... die Anzahl der Pixel pro Fläche (oder Länge) sein (dpi = dips per inch)
	- z.B. ca. 100 dpi eines normalen Monitors
	- z.B. ca. 600 dpi eines normalen Druckers
- ... bei einer Farbe sein, wie viele mögliche Farben dargestellt werden können.

# Quelle
1. Modul Computergraphik der HAW Kiel von Prof. Dr. Wolfram Acker 
   (Wintersemester 2025/26)
2. 