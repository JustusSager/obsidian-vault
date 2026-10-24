Es gibt eine Norm für Elektrische Systeme auf kleinen Wasserfahrzeugen:
- EN ISO 13297:2021 + A1:2022 + A11:2023
# Was / Wie / Wo Kabel
## Welche Kabel können verwendet werden? 
- Immer nur **flexible Leitungen**, da starre Leitungen unter Vibration und Bewegung schneller brechen.
- Bei Kabeln mit **kleinem Querschnitt** ($\le 16 \text{mm}^2$) sollte die **Isolierung aus PVC sein**, da diese schwer entflammbar und selbstlöschend ist.
	- Mantel aus `PVC (Polyvinylchlorid)`
	- `H07V-K` 
- Bei **großem Querschnitt** ($\gt 16 \text{mm}^2$) empfiehlt sich ein **Kabel mit erhöhter Litzendichte** für mehr Flexibilität.
	- `H01N2` mit Gummiummantelung vom Typ `EM5`
- Bei Kabeln **im Außenbereich** sollte das Kabel einen besonders UV-beständigen Mantel haben und besonders wasserresistent sein. Es empfiehlt sich **Kabel mit verzinnten Litzen**
	- Mantel aus `PUR (Polyurethan)` 
## Farbcodes der Kabel
### 12V
Es sollten auf jeden Fall nicht die Farben der 230V Wechselstrom-Kabel verwendet werden. Das schließt folgende Farben aus:
- Blau, Braun, Grün-Gelb
Ansonsten gibt es eigentlich keine Einschränkungen, es hat sich jedoch häufig ein gewisser Standard etabliert. Es kann z.B. folgendes Farbschema verwendet werden:

| Nutzung          | Farbe                |
| ---------------- | -------------------- |
| 12V Minus        | Schwarz              |
| 12V Plus         | Rot                  |
| Analoge Signale  | Gelb                 |
| Digitale Signale | Irgendwelche anderen |
Zusätzlich sollten alle Kabelenden beschriftet werden mit ihrem Zweck.
### 230V
Sollte man nicht selber machen, aber falls doch:
Die Kabelfarben sind Festgelegt:

| Nutzung      | Farbe     |
| ------------ | --------- |
| L1           | Braun     |
| Neutral      | Blau      |
| Schutzleiter | Grün-Gelb |
Dieser Standard hat sich 1970, 1980 und 2005 geändert, daher **Vorsicht** bei alten Leitungen!
## Kabelenden
Es können verschiedene Terminals am Ende eines Kabels 

# Einen LiFePo4-Akku mit der Lichtmaschine laden
**Ausgangssituation:**
Es existiert ein Motor mit einer normalen Lichtmaschine für Blei-Säure-Akkus, welche direkt an die Starterbatterie des Motors angeschlossen ist. Außerdem existiert ein LiFePo4-Akku welcher als Verbraucherakku verwendet wird.
**Ziel** ist es, dass die Lichtmaschine zusätzlich zur Starterbatterie auch die LiFePo4-Verbraucherbatterie auflädt. Dies soll automatisch und ausschließlich bei laufendem Motor geschehen. Die Starterbatterie darf dabei nicht entladen werden.

**Problem:**
1. Ein LiFePo4-Akku hat im Vergleich zu einer normalen Starterbatterie einen sehr geringen internen Wiederstand. Dadurch würde (bei direktem Anschluss) eine normale Lichtmaschine durchbrennen, da diese den Innenwiederstand des Akkus als Strombegrenzung benutzt.
2. LiFePo4-Akkus und Blei-Säure-Akkus haben eine unterschiedliche Ladespannung und Kurve.


# Quellen
- https://www.blauwasser.de/bootselektrik-anleitung-erneuern-planen