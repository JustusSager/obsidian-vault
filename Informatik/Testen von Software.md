---
erstellt am:
  - "19.05.2026 13:09"
tags:
Deckblatt:
---
# Warum wird getestet
- Eine Software (und auch kein anderes Produkt) ist niemals vollständig fehlerfrei.
- Auch Tests können nicht die Fehlerfreiheit eines Programms nicht sicherstellen.
- In der Praxis ist ein "Volltest" kaum möglich.
Aber:
- Je nach Einsatzzweck der Software und der Art des Fehlers können erhebliche Schäden entstehen.
	- deshalb sind "alle" Funktionen einer Software systematisch auf Fehler zu testen
	- ein Test kann in einem gewissen Sinne als destruktiv bezeichnet werden und muss immer darauf abzielen, neue Fehler zu finden!
- Fehlerbehebung während der Entwicklung
	- verbessert das Produkt
	- senkt die Kosten einer späteren Fehlerbeseitigung

# Allgemeine Probleme des Testens
## Umfang der Tests
- Keine komplexe Software kann vollständig getestet werden
- Die Durchführung von Tests verschlingt Ressourcen ohne garantierte direkte Gegenleistung.
- Ein "Volltest" ist technisch quasi nicht umsetzbar, da es voraussetzt alle möglichen verschiedenen Rahmenbedingungen vorherzusehen.
- Der Umfang der Tests wird also in Abhängigkeit zur Priorität und zum Risiko reduziert unter Anwendung systematischer Vorgehensweisen.
	- Ein hoher Testaufwand für die Beseitigung „kleinerer“ Fehler ist nicht gerechtfertigt.
	- Ein Programm in den Einsatz zu bringen, ohne auch die entscheidenden Eigenschaften auf Fehler getestet zu haben, ist wenig sinnvoll.
	- In der Praxis wird somit stichprobenartig getestet.
	- Allerdings wird diese Stichprobe i. d. R. analytisch bestimmt.
## Kosten
- Testen verursacht hohe Kosten innerhalb der Softwareentwicklung
	- Insbesondere in großen IT-Projekten kann der Aufwand für das Testen den größten Anteil am Gesamtaufwand einnehmen.
	- Frühzeitiges Testen trägt zur Verbesserung des Entwicklungsprozesses bei und reduziert damit Kosten (u. a. durch die Verringerung der Fehlerentdeckung in späten Phasen der Softwareentwicklung, denn dann ist die Fehlerentdeckung und -behebung deutlich aufwändiger).
- Fehler, die nicht bei Tests gefunden wurden, verursachen ebenfalls Kosten (Fehlerkosten)
	- Imageverluste, Aufwand für Korrekturen und Schadenersatz drohen dem Hersteller
	- Datenfehler oder Datenverluste und Ausfallzeiten sind die Folgen für den Kunden
- Bemerkung: 
  Testkosten sollten geringer sein als mögliche Fehlerkosten!

# Sollwerte und Testorakel
Zum Testen benötigt man Werte gegen die man die Ergebnisse testen kann.
### Sollwerte
- Fehlerwirkung:
  Abweichung zwischen Soll- und Ist-Ergebnis
- Dem Tester muss ein eindeutiges Sollergebnis vorliegen, um es mit dem Testergebnis vergleichen zu können!
- Die verschiedenen Quellen, die ein Tester während der Spezifikation seiner Testfälle befragen kann, um an Angaben zu den erwarteten Sollergebnissen zu gelangen, werden auch unter dem Begriff Orakel bzw. Testorakel zusammengefasst.

### mögliche Testorakel
- Ableitung der Sollergebnisse
	- Übliche Vorgehensweise, bei der die Sollwerte aus den Spezifikationen oder der Anforderungsdefinition abgeleitet werden
	- Zur Generierung der Sollergebnisse wird evtl. zusätzliches Fachwissen benötigt
- Prototypen
	- Liegen Spezifikationen vor, können für die Bestimmung der Sollergebnisse vorab Prototypen des Testobjektes entwickelt werden
- Back-to-Back“-Test
	- Anforderungen werden von mehreren Entwicklern parallel umgesetzt.
	- „Back-to-Back“-Tests werden in allen Umsetzungen durchgeführt.
	- Ergebnisse werden anschließend verglichen.
	- Weicht ein Ergebnis von den anderen ab, liegt ein Fehler vor.
	- „Back-to-Back“-Tests sind sehr aufwendig und mit hohen Kosten verbunden.
- Benutzerhandbücher, Dokumentationen
	- Liegen umfassende Angaben anhand von Handbüchern oder Dokumentationen vor, können diese ebenfalls als Testorakel herangezogen werden.
- Testobjekt
	- Gibt es keine anderen Testorakel, dann muss das Testobjekt selbst herangezogen werden.
	- Dazu wird das Testobjekt an unterschiedlichen Stellen von verschiedenen Personen ausgeführt.
	- Alle Daten werden gesammelt und ausgewertet.

# Begriffserklärung
## Fehlerbegriffe
### Fehler
- Abweichung zwischen Ist- und Soll-Wert.
- Nichterfüllung einer festgelegten Anforderung
### Mangel
- festgelegte Anforderung wird nicht angemessen erfüllt
### Fehlerwirkung / äußerer Fehler
- Sichtbarwerden eines Fehlers
### Fehlerzustand (Defekt, innerer Fehler)
- Ursache für das Auftreten einer Fehlerwirkung
### Fehlermaskierung
- Mehrere Fehlzustände kompensieren sich gegenseitig
- Es tritt keine Fehlwirkung auf
### Fehlhandlung
- Ursache für einen Defekt oder Fehlerzustand
- stellt eine menschliche Handlung dar, 
	- z. B. Fehlprogrammierung etc.

## Testen und Testfall
### Debugging
- Lokalisieren und Beheben von inneren Fehlern
### Testen
- gezielte und systematische Suche nach Fehlerwirkungen, um Defekte nachzuweisen
### Testen von Software
- jede Ausführung eines Testobjektes, die zu dessen Überprüfung dient
- i. d. R. erfolgt dies stichprobenartig
### Testfall
- Zusammenführung von Test und festgelegten Rahmenbedingungen
- z. B. Ausführungsvoraussetzungen, feste Eingabewerte in Verbindung mit erwarteten Ein-/Ausgabewerten oder dem erwarteten Verhalten des Testobjektes
### Testfallexplosion
- meint, dass durch die vielfältigen Kombinationsmöglichkeiten bspw. von Eingabewerten die Anzahl möglicher Testfälle sehr schnell ansteigt und leicht einen Umfang von hunderten oder tausenden Testfällen erreichen kann

## Softwarequalität
Definition nach ISO / IEC 9126
- Softwarequalität ist die Gesamtheit der Merkmale und Merkmalswerte eines Software-Produktes, die sich auf dessen Eignung beziehen, festgelegte oder vorausgesetzte Erfordernisse zu erfüllen.
Bemerkung: Softwarequalität bezieht sich in dieser Definition auf das Produkt, nicht auf den Prozess, der zu der Entstehung des Produkts führt.

### Kriterien zur Qualität von Software
nach ISO / IEC 25010
#### Funktionale Eignung
- Funktionen mit festgelegten Eigenschaften / Fähigkeiten vorhanden sind.
- dass diese Funktionen die definierten Anforderungen erfüllen ([[Anforderungsdefinition#^065da4|funktionale Anforderungen]])
- Merkmale nach ISO / IEC 9126
	- Angemessenheit
	- Richtigkeit
	- Interoperabilität
	- Ordnungsmäßigkeit
	- Sicherheit
#### Effizienz
- bedeutet einen möglichst geringen Verbrauch an Ressourcen (z. B. CPU-Zeit), der für die Erfüllung einer Aufgabe erforderlich ist.
#### Kompatibilität

#### Benutzbarkeit
- Je geringer der Aufwand für die Benutzung der Software, desto höher ist die Benutzbarkeit einzustufen.
- Merkmale
	- Erlernbarkeit
	- Verständlichkeit
	- Bedienbarkeit
#### Zuverlässigkeit
- eine Software / ein System kann fest vorgegebenen Bedingungen seine Leistung / Funktion über einen definierten Zeitraum aufrechterhalten
#### Sicherheit

#### Wartbarkeit (Änderbarkeit)
- zielt ab auf den Aufwand, der zur Durchführung vorgegebener Änderungen notwendig ist.
#### Übertragbarkeit
- Möglichkeiten zur Übertragung der Software in eine andere Umgebung, d. h.:
	- Hardware-Umgebung
	- Software-Umgebung
	- organisatorische Umgebung

## Qualitätssicherung
### konstruktive Maßnahmen der Fehlervermeidung
z.B. durch geeignete Methoden des Software-Engineering
- technische Maßnahmen
	- Methoden
	- Werkzeuge
- Organisatorische Maßnahmen
	- Richtlinien
	- Standards
	- Checklisten
### analytische Maßnahmen der Fehlerfindung
z. B. durch Testen, da es durch das Finden von Fehlerwirkungen dazu dient, Defekte zu beseitigen und damit die Softwarequalität zu erhöhen

## Begriffe der Softwarequalität
### Korrektheit
- Korrektheit als „Grad der Übereinstimmung zwischen Spezifikation und Programm“ (ANSI 72983)
- Korrektheit bedeutet Abwesenheit von Fehlern
- Software ist korrekt, wenn sie genau das in der Spezifikation festgelegte funktionale Verhalten zeigt
	- also nicht: Wartbarkeit, Effizienz, Funktionalität, …
	- als Qualitätsmaß schlecht geeignet
- Bemerkung: Üblicherweise sind verschiedene korrekte Implementierungen einer Spezifikation möglich 
- 
### Sicherheit
- Sicher: „Zustand, in dem das Risiko eines Personen- oder Sachschadens auf einen annehmbaren Wert begrenzt ist“ (ISO 8402)
- Ein System heißt sicherheitskritisch, wenn es beim Ausfall großen Schaden verursachen kann
	- „großer Schaden“: Der Ausfallverlust übersteigt die regulären Betriebsgewinne um ein Vielfaches
- Siehe auch [[Glossar#Funktionssicherheit|Funktionssicherheit]] und [[Glossar#Informationssicherheit|Informationssicherheit]]

### Zuverlässigkeit
- Zuverlässigkeit (Reliability) ist ein Maß für die Fähigkeit des Systems, funktionstüchtig zu bleiben; Wahrscheinlichkeit, dass das System während einer bestimmten Zeitdauer t nicht versagt
- Grad der Vertrauenswürdigkeit in die vom System erbrachte Leistung
- MTTF: mean time to failure
- Überlebenswahrscheinlichkeit R(t):
  Wahrscheinlichkeit, dass das System nach t Zeiteinheiten noch nicht ausgefallen ist
### Verlässlichkeit
- Verlässlichkeit (Dependability) wird oft synonym oder als Erweiterung für Zuverlässigkeit verwendet
- DIN 40041: Zuverlässigkeit ist die Beschaffenheit bezüglich der Eignung, während oder nach vorgegebenen Zeitspannen bei vorgegebenen Arbeitsbedingungen die Zuverlässigkeits-Anforderungen zu erfüllen.
- Teile: Verfügbarkeit, Funktionsfähigkeit, Sicherheit
- Vertraulichkeit ist Teil der [[Glossar#Informationssicherheit|Informationssicherheit]] 
### Verfügbarkeit
- MTBF: mean time between failures; MTTR: mean time to repair
- Verfügbarkeit (availability) misst die Wahrscheinlichkeit, mit der ein reparierbares System zu einem beliebigen Zeitpunkt funktioniert:
  MTBF / (MTBF + MTTR)
### Robustheit
- Eigenschaft des Systems, auch in ungewöhnlichen (unspezifizierten) Situationen bestmögliche Funktionalität zu erbringen
### Fehlertoleranz
- Eigenschaft des Systems, auch beim Auftreten von bestimmten Fehlern (Fehlzuständen) die geforderte Funktionalität zu erbringen

# 