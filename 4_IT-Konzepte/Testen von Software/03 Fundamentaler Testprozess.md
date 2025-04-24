# Ablauf einer Softwareentwicklung
Eine strukturierte Softwareentwicklung folgt fest definierten Schritten. Verschiedene Vorgehensmodelle stellen den strukturierten Entwicklungsablauf dar.

## Beispiel Wasserfallmodell nach Royce (1970) ^18f604
- Entwicklungsprozess in 7 Stufen
- Jede Stufe hat nur eine Rückkoppelung zur Vorstufe
- Das Testen stellt hier nur eine Stufe im Prozess dar
	- es entspricht einer Produkt-Endabnahme
![[softwareentwicklungsprozess_wasserfallmodell.png|500]]

# Testen innerhalb des Softwareentwicklungsprozesses
- Abhängig von der Art des Vorgehensmodells wird das Testen zu verschiedenen Zeitpunkten der Softwareentwicklung durchgeführt.
- Das Testen selbst muss dabei ebenfalls als ein Prozess verstanden werden.
- Der Testprozess unterscheidet dabei die folgenden Phasen:
	![[Testprozess_nach_bs7925-2.png|250]]
### Testplanung:
- Start mit Beginn des Entwicklungsprozesses
- Planung der Ressourcen
	- Mitarbeiter
	- Umgebung und Hilfsmittel
- Festlegung einer Teststrategie
	- Setzen der Testprioritäten
	- Auswahl der Testfälle (z. B. nach Risiko)
	- Auswahl der Testmethoden
	- Festlegen der Testendekriterien
		- nach Überdeckung
		- nach Kundenanforderungen
	- Priorisierung der Tests
		- … muss erfolgen
		- … sollte erfolgen
		- … kann erfolgen
	- Werkzeugunterstützung ja/nein
	- Auswahl der Testumgebung
### Testspezifikation:
- Erzeugung von Testfällen
	- Anhand vorgegebener Methoden aus der Teststrategie
- Testdaten bereitstellen
	- häufig Anonymisierung von Daten erforderlich
- Rahmenbedingungen festlegen
- Vorgabe der Sollergebnisse für die Testfälle
	- Prüfung von Funktionen („Positivtest“)
	- Prüfung von Fehlersituationen („Negativtest“)
	- Prüfung von Fehleingaben (exception handling, „Falschtest“)
### Testdurchführung:
- Implementierung von:
	- Testtreibern
	- Testumgebung
- Aufsetzen von Monitoring-Tools
- Integration der Testdaten
- Ausführung der Testfälle bzw. Testszenarien unter gegebenen Rahmenbedingungen
### Testprotokollierung:
- Vollständige und exakte Protokollierung der Tests
- Transparenz der Tests für Dritte, die nicht direkt beteiligt sind
- Nachweis über die Umsetzung der Testplanung / Teststrategie
- Aufzeichnung von:
	- Testobjekt
	- Tester
	- Testdaten
	- Ergebnis
- Sicherstellen, dass Tests später erneut durchgeführt werden können
	- Rahmenbedingungen und Testdaten müssen archiviert werden
### Testauswertung:
- Auswertung der Fehlerwirkungen
	- Sind alle Fehlerwirkungen wirklich auf Fehler zurückzuführen?
	- Gefundene Fehler führen zu einem weiteren Testzyklus – beginnend mit der Testspezifikation
- Testendekriterien prüfen
	- Überdeckung erreicht?
	- Risikoabdeckung erreicht?
- Sind die Kriterien alle erfüllt, endet der Test mit der Auswertung
- Sind diese Kriterien nicht erfüllt,
	- ist ggf. erneut zu prüfen, ob sie überhaupt zu erfüllen wären
	- ist zu prüfen, ob die Testplanung angepasst werden sollte

# Testendekriterien
### Codeüberdeckung
- x % des Programmcodes müssen durchlaufen worden sein
### Risikoabdeckung
- Testfälle einer definierten Risikoklasse müssen fehlerfrei durchlaufen worden sein (z. B. die der obersten Priorität)
### Fehlerfindungsrate
- Anzahl neuer Fehler pro Stunde Testaufwand unterschreitet einen definierten Wert
- Test wird beendet, wenn sich pro Zeiteinheit weniger als n neue Fehler finden lässt
- Hier wird die Wirtschaftlichkeit von Tests berücksichtigt, die ab einer bestimmten Rate nicht mehr gegeben ist
### Testabbruch aus Zeit- oder Kostengründen
- z. B. in Folge unzureichender Ressourcenplanung
- verursacht i. d. R. durch später auftretende Fehler zusätzliche Kosten
