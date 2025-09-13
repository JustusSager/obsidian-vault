# Warum muss priorisiert werden?
### "Schwachstelle" Zeit
- Das Testen steht am Ende des Softwareentwicklungsprozesses – wird in den vorhergehenden Stufen zusätzliche Zeit verbraucht, fehlt diese am Ende, um die geplanten Tests durchzuführen.
- Auch wenn ausreichend Zeit für den Test geplant wurde, kann es bedingt durch hohe Fehlerzahlen zu einer Ausweitung der Tests kommen.
- Oft wird das Testen vernachlässigt und erhält in der Projektplanung nur wenig Ressourcen.
### Risiko
- Knappe Ressourcen lassen einen Volltest i. d. R. nicht zu.
- Gleichverteilung der Ressourcen über alle Testbereiche bedeutet i. d. R. Verschwendung, da keine Gewichtung nach Risiken vorgenommen wird.
- Aufteilung des Testobjektes in kritische und unkritische Bereiche!
- Systematische Aufteilung der Testfälle in Risikoklassen ist sinnvoll.

# Nach welchen Kriterien erfolgt die Priorisierung?
### Eintrittswahrscheinlichkeit eines Fehlers
- Fehler in Funktionen, die sehr häufig Verwendung finden, werden als Fehlerwirkung eher sichtbar als Fehler in Funktionen, die sehr selten zum Einsatz kommen.
- Es kann also eine Priorisierung nach der Verwendungshäufigkeit erfolgen.
### Fehlerschwere
- Höhe des durch den Fehler verursachten möglichen Schadens wird betrachtet
- Schaden bezogen auf die Fehlerkosten (z. B. Schadenersatz etc.)
- Klassifikation nach zusätzlichen Kriterien ebenfalls sinnvoll (z. B. Imageschäden)

### Fehlerrisiko
- Fehlerrisiko = Eintrittswahrscheinlichkeit x Fehlerschwere
- Getestet wird vor allem dort, wo mit hoher Wahrscheinlichkeit ein großer Schaden erwartet wird
### Wahrnehmung des Fehlers
- Ist ein Fehler bzw. dessen Fehlerwirkung für den Anwender (Kunden) zu erkennen?
- Ein Fehler in der GUI fällt dem Anwender z. B. sofort auf und stellt u.U. die Funktionsfähigkeit des übrigen Programms in Frage.
### Anforderungsdefinition
- Eine mögliche Gewichtung kann auf Basis der Anforderungsdefinition erfolgen.
- Sind dort einige Funktionen wichtiger als andere, werden diese stärker getestet.
- Es wird getestet, was der Kunde benötigt.
### Softwarequalitätsanforderungen
- Werden bestimmte Merkmale der Softwarequalität höher gewichtet, können diese auch intensiver getestet werden
### Fehlerwirkungen
- Unterscheidung der Fehlerwirkungen zwecks Priorisierung
	- Führt der Fehler zu einem Systemabsturz oder zu einer Fehldarstellung in der GUI?
### Komplexität
- Komplexe Programmteile sind oftmals fehlerträchtiger als einfache, wobei sich die Frage nach der Definition von Komplexität stellt.
- Unter Beachtung von Metriken für die Komplexität sollten solche Programmteile intensiv getestet werden.
Bemerkung: Unter einer Metrik versteht man eine Größe zur Messung einer bestimmten Eigenschaft eines Programms oder eines Programmsegments.
### Ressourcen-Risiko
- Welche Auswirkungen hat der Fehler auf die Projekt-Ressourcen?
- Es wird dort intensiv getestet, wo ein Fehler zu größeren Änderungen und somit zu großem Aufwand führen würde.
	- Eventuell notwendige Veränderungen in der Programmierung, die in einer der unteren Stufen des Softwareentwicklungsprozesses durchgeführt werden müssen

# Auf welche Besonderheiten ist zu achten?
- Die Praxis zeigt ein interessantes Phänomen:
	- Wo viele Fehler gefunden wurden, werden noch viele zu finden sein!
	- evtl. dadurch zu Begründen, dass in dem Bereich unter Zeitdruck gearbeitet wurde und sich somit Fehler häufen.
- Generell muss die Möglichkeit bestehen, zwischen zwei Testzyklen Anpassungen der Priorisierung der Testfälle vorzunehmen, um auf derartige Gegebenheiten zu reagieren.
- Immer zuerst die Testfälle höchster Priorität testen!
	- Sicherstellen, dass schwere Fehler frühzeitig erkannt werden.
	- Die Testphase könnte frühzeitig abgebrochen werden.

# Psychologie des Testens
- Beim Testen entsteht eine feste Rollenverteilung, für die pot. das gegenseitige Verständnis fehlt.
- Der Hinweis auf Fehler kann zu Problemen zwischen Tester und Entwickler führen.
	- Umgangsweise mit einer Fehlerentdeckung und Fehlermeldung ist entscheidend.
	- keine persönliche Kritik, sondern sachliche Auseinandersetzung.

## Schwierigkeiten
- Unzureichende Kommunikation erschwert Zusammenarbeit zwischen Testern und Entwicklern
- Je weiter der Tester von der Entwicklung entfernt ist, desto unabhängiger und unvoreingenommener kann gearbeitet werden.
- Aber: Desto weiter weg der Tester ist, desto mehr Einarbeitungszeit wird benötigt.

## Mögliche Testumsetzung
### Entwicklertest
- Ein Entwickler steht dem eigenen Code niemals neutral gegenüber.
	- Er neigt dazu den eigenen Fehlern gegenüber blind zu sein
	- Dafür kennt der Entwickler den Code bereits.
- Ein Fehler aufgrund einer Fehlinterpretation der Anforderung bleibt unentdeckt.
### Testteams
- Bildung von Testteams aus verschiedenen Bereichen verbessern die Qualität der Tests
- Teams sollten möglichst unabhängig arbeiten können.
### Test-Outsourcing
- Komplette Ausgliederung der Tests schafft größte Distanz
	- Höchste Neutralität,
	- aber auch höchste Einarbeitungszeit.
	- ggf. auch besonderes Test-Know-how