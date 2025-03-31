#TODO hier noch ergänzen aus Modul Anforderungsmanagement

Entsprechend der ISO 25000 in verschiede Anforderungsarten unterschieden:
- [[#^065da4|funktionale Anforderungen]] (Ist etwas machbar)
	- Funktionalität der Software 
- [[#^ec6199|nicht-funktionale Anforderungen]] (Wie gut ist es machbar)
	- Zuverlässigkeit
	- Benutzbarkeit
	- Effizienz
	- Änderbarkeit
	- Übertragbarkeit
	- ...

# Funktionale Anforderungen ^065da4

Leitfrage: Werden die geforderten Eigenschaften durch die vorhandenen Funktionen umgesetzt?

Das System ist auf folgende Punkte zu testen:
- Angemessenheit
  Eignet sich die vorhandenen Funktionen für die vorgesehene Verwendung?
- Richtigkeit
  Laufen die Funktionen korrekt (wie vereinbart) ab?
- Interoperabilität
  Ist ein fehlerfreies Zusammenspiel mit der Systemumgebung gegeben?
- Ordnungsmäßigkeit
  Wurden die Normen und Vorschriften eingehalten?
- Sicherheit
  Sind die Daten / Programme vor ungewünschten Zugriffen / Verlusten geschützt?

## Testen von funktionalen Anforderungen ^692e46
Es wird in 3 verschiedene Ansätze zum Test von funktionalen Anforderungen unterschieden

### Anforderungsbasierter Test
Die Testfälle leiten sich hierbei aus der Anforderungsdefinition ab. Dabei variiert die Anzahl der Testfälle je nach Anforderung.

### Geschäftsprozessbasierter Test
Hierbei dienen einzelne Geschäftsprozesse als Grundlage für die Ableitung von Testfällen.
Eine Rangfolge der Prozesse kann als Priorisierung der Testfälle mit übernommen werden.

### Anwendungsfallbasierter Test
Die Testfälle werden aus Anwendungsfällen (bzw. aus üblichen Anwenderaktionen) abgeleitet. Die Priorisierung erfolgt dabei je nach Häufigkeit der Anwendungsfälle.

# Nicht-funktionale Anforderungen ^ec6199
- Effizienz
- Zuverlässigkeit
- Ergonomie
- Änderbarkeit
- Übertragbarkeit
- Sicherheit
- Performance
- ...
Neben Bereichen wie Performance oder Sicherheit stellt Ergonomie eine weitere wichtige nicht-funktionale Anforderung dar. Software-ergonomische Anforderungen sind in der Norm ISO 9241, insbesondere im Teil 10 aufgeführt (z. B. Fehlertoleranz, Erlernbarkeit und Aufgabenangemessenheit)
Nicht-funktionale Anforderungen sind meist deutlich schwerer zu testen und daher mit einem höheren Risiko verbunden. Der Anforderungsdefinition ist häufig nicht eindeutig zu entnehmen "wie gut" etwas funktionieren soll, z.B. wegen vager Definition. Außerdem liegen nicht-funktionale Anforderungen oft implizit vor und werden daher nicht näher definiert.

## Testen von nicht-funktionalen Anforderungen ^a713b5
Der Test einer nicht-funktionalen Anforderung gilt als bestanden, wenn ein
bestimmter Wert in einer vorgegebenen Metrik erreicht ist. Z.B. Eine Metrik für Zuverlässigkeit einer Software, wie:
- MTBF - Mean Time Between Failure
- MTTR - Mean Time To Repair
Eine Quantifizierung ist jedoch häufig schwierig.

### Typische Tests

#### Lasttest
- Wie verhält sich das System unter Last (steigende Anzahl Anwender / Aktionen)?

#### Performancetest
- Wie schnell ist das System bei bestimmten Funktionen / Anwendungsfällen?

#### Volumen- / Massentest
- Wie verhält sich das System bei der Verarbeitung großer Datenmengen / Dateien?

#### Stresstest
- Wie reagiert das System bei Überlastung?
- Wie reagiert das System beim Wiedereintritt in den Normalbetrieb?

#### Test auf (Daten-) Sicherheit
- Ist das System gegen unberechtigten Zugriff geschützt?
- Sind die Daten gegen unberechtigte Zugriffe oder Verlust geschützt?

#### Stabilitätstest
- Wie häufig fällt das System pro Zeiteinheit aus? 
- Systemverhalten im Dauerbetrieb

#### Test auf Robustheit
- Wie reagiert das System auf Fehlbedienung oder Fehleingabe (exception handling)?
- Systemverhalten bei Hardwaredefekten und das Wiederanlaufverhalten

#### Kompatibilitätstest (Datenkonversion)
- Wie arbeitet das System mit anderen Programmen zusammen?
- Welche Schnittstellen bestehen zu anderen Programmen?
- Wie reagiert das System auf verschiedene Umgebungen (Hardware, BS, etc.)?

#### Test auf Gebrauchstauglichkeit
- Wie übersichtlich und verständlich ist das System?
- Wie gut kann der typische Anwender die Bedienung erlernen?

#### Prüfung der Dokumentation
- Stimmt die Programmdokumentation mit dem tatsächlichen System überein?
- Ist die Dokumentation übersichtlich und verständlich geschrieben?

#### Prüfung der Änderbarkeit/Wartbarkeit
- Liegen ordnungsgemäße Dokumente über die Systementwicklung vor?
- Wurden vorgegebene Coding-Standards eingehalten?
- Besitzt das System eine strukturierte (modulare) Systemarchitektur?

### Beispiele für das Testen von nicht-funktionalen Anforderungen
Vorgabe: Server soll maximal 200 Clientanfragen gleichzeitig bearbeiten können.
- Lasttest: Server bearbeitet 200 Clientanfragen gleichzeitig
- Stresstest: Server bearbeitet 210 Clientanfragen gleichzeitig
- Test auf Robustheit: Clients werden bei laufender Transaktion abgeschaltet

