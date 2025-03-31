# Vor Folie 21
#TODO 

# Testen im Software-Lebenszyklus
![[v-modell.png]]
## Komponententest
Definition: Testen der einzelnen Softwarebausteine (Komponenten) im Anschluss an deren Programmierung.
Die einzelnen Komponenten (z.B. eine bestimmte Klasse) wird isoliert getestet, um nach internen Fehlern zu suchen. Eine Wechselwirkung mit anderen Komponenten wird nicht überprüft.

Kann verschiedene Bezeichnungen haben:
- Modultest (z.B. in C)
- Klassentest (z.B. in Java, C++)
- Unit-Test (z.B. in Pascal)

### Umsetzung
Das Testobjekt ist i.d.R kein eigenständig ausführbarer Programmteil. Daher wird mithilfe eines Testtreibers auf die öffentlichen Schnittstellen der Komponente zugegriffen. Der Testtreiber kann eigenständig ausgeführt werden und ermöglicht den Komponententest mithilfe von simulierten Ein-/Ausgaben aus der Komponente.
Wenn der Quellcode vorliegt (bzw. Tester = Entwickler) kann sehr entwicklungsnah getestet werden und z.B. mithilfe von einem Debugger die exakte Fehlerquelle festgestellt werden.
Platzhalter (oder Stubs) werden benötigt, wenn die Komponente komplexere Eingaben benötigt oder Ausgaben zu verarbeiten sind. Stubs stellen dabei ggf. Testdaten (Dummies) zur Verfügung.

![[Komponententest_zusammenspiel.png]]

Jede der Funktionen der Komponente wird anhand von mindestens eines Testfalls geprüft.
Dabei sollten folgende Test durchgeführt werden:
- Test auf Funktionalität (Test mit erfolgreicher Eingabe)
- Negativtest (Testfall welcher falsche/unzulässige Eingabewerte enthält)
- Je nach [[Anforderungsdefinition]] weitere (z.B. auf Effizienz, Änderbarkeit, ... )
### Ziel
Funktionalität der Komponente sicherstellen
- Werden alle Spezifikationen erfüllt?
- Werden alle Funktionen korrekt ausgeführt?
Test der Robustheit
- Überprüfen wie die Softwarekomponente auf Fehleingaben reagiert.
- Besitzt die Komponente für jede mögliche Falscheingabe eine Ausnahmebehandlung, gilt sie als Robust
	- Ohne Ausnahmebehandlung fließen die Falscheingaben sonst in die Verarbeitung.
	- Mögliche Folgen wären Fehlfunktionen und Programmabstürze.

### Häufig gefundene Fehler
- Fehler in der Verarbeitung 
- Fehlende Funktionen

## Integrationstest
Definition: Test des Zusammenspiels einzelner Softwarebausteine (Komponenten) im Anschluss an deren Integration.
Hierbei wird die Wechselwirkung zwischen verschiedenen zusammenhängenden Komponenten getestet. Dazu werden verschiedene zusammenhängende Bausteine (Komponenten) zu größeren Baugruppen zusammengefasst und auf ihr Zusammenspiel getestet. Jeder Baustein sollte dafür vorher für sich schonmal getestet worden sein. 

### Umsetzung
Dieses (Teil-) System ist i.d.R immer noch kein selbstständig ausführbares System. Daher wird wieder ein Testtreiber benötigt, der die zusammengesetzten Komponenten auf ihre Wechselwirkung untereinander überprüft. Diese Testtreiber übernehmen hierbei wieder die Simulation einer Umgebung für das (Teil-) System. Platzhalter ersetzen hierbei wieder die fehlenden Komponenten. 

### Ziel
- Schnittstellenfehler ermitteln, um korrektes Zusammenspiel der Komponenten sicher zu stellen.
	- Platzhalter aus dem Komponententest werden hier (zum Teil) zu "realen" Komponenten, die potenziell anders reagieren.
- u.a. auch Blick auf Performance und Sicherheit
- 
### Integrationsstrategien
Es existieren verschiedene Integrationsstrategien. Die Wahl der Strategie muss dabei die Testeffizienz und Aufwand berücksichtigen. 
![[Integrationsstrategien.png]]

#### Bottom-Up
Systematische Integration von unten nach oben. Begonnen wird dabei mit den Komponenten, die keine weiteren Programmteile aufrufen. Schrittweise werden die Komponenten hinzugefügt, welche auf bereits integrierte aufbauen.
Dadurch entstehen keine Lücken, die durch Platzhalter gefüllt werden müssen. Jedoch müssen Vorgelagerte Komponenten über Testtreiber simuliert werden. Diese Strategie lässt sich jedoch nur bei streng hierarchisch aufgebauter Software umsetzen. Daher ist diese Strategie in Rheinform kaum von praktischer Relevanz.
Empfohlen bei Neuentwicklung und bei großen, verteilten Entwicklerteams.

#### Top-Down
Die Integration verläuft systematisch von oben nach unten. D.h. es wird mit der Komponente begonnen welche von keinem anderen Baustein aufgerufen wird. Schrittweise werden die Komponenten integriert, die von dem bereits zusammengefügten Teil aufgerufen werden. Es werden dadurch keine Testtreiber benötigt, jedoch müssen alle noch nicht integrierten Komponenten durch Platzhalter ersetzt werden. Ähnlich zur Bottom-Up Strategie funktioniert dies nur in streng hierarchisch aufgebauter Software und ist dadurch in ihrer Rheinform kaum von praktischer Relevanz.
Empfohlen vor allem bei der Nutzung von Fremdsoftware oder Frameworks.

#### geschäftsprozessorientierte Integration
- Integration wird nach Geschäftsprozessen durchgeführt
- Integriert werden jeweils die Komponenten, die von einem Geschäftsprozess benötigt werden
- Wird auch End-to-End Test genannt
- Testtreiber ersetzen hierbei übergeordnete Bausteine
- untergeordnete Komponenten werden mit Platzhaltern ersetzt

#### Ad-Hoc-Integration
- Bereits getestete Komponenten werden (soweit möglich) unmittelbar nach der Programmierung und erfolgtem Komponententest integriert
- Keine Verzögerungen der Tests, führt ggf. zur Verkürzung des gesamten Softwareentwicklungsprozesses
- Je nach Art der Komponente werden Testtreiber und Platzhalter benötigt
- Diese Strategie kann quasi immer genutzt werden, in der Praxis oft in verbindung mit anderen Strategien

#### Big Bang
- Integration erfolgt erst wenn alle Komponenten vorliegen
- Testbereich hat viel "Leerlauf", es kann lange nichts getestet werden.
- Der Test wird deutlich komplizierter und umfangreicher. Fehlerwirkungen treten gehäuft auf und lassen sich nur schwer nachvollziehen.
- Diese Strategie wird z.B. bei Wartungs- oder Erweiterungsprojekten sowie bei IT-Migrationen eingesetzt

### Integration und Tests koordinieren
![[koordination_integration_und_test.png]]

## Systemtest
Das Gesamtsystem wird geprüft auf die Einhaltung der spezifischen [[Anforderungsdefinition|Anforderungen]]. Zu diesem Zeitpunkt wurden bereits alle Komponenten und deren Zusammenspiel getestet, es soll hier jedoch das Gesamtsystem unter Einsatzbedingungen und aus der Perspektive des Anwenders getestet werden. 

### Umsetzung
- Das System sollte unter realer Systemumgebung getestet werden mit praxisnahen Daten
- Es werden keine Testtreiber und Platzhalter mehr eingesetzt
- Alle externen Schnittstellen werden unter Produktivbedingungen getestet
- Es soll bei den Tests eine möglichst exakte Nachbildung der späteren Produktivumgebung erreicht werden, aber keine Tests in der Produktivumgebung!
	- Fehler könnten zu Schäden an der Produktivumgebung führen
	- Tests in der realen Produktivumgebung sind schwer reproduzierbar

### Ziel
- Test des integrierten Systems aus Anwendersicht
- Vollständige und korrekte Umsetzung aller [[Anforderungsdefinition|Anforderungen]] 
	- Zum Testen von Anforderungen siehe [[Anforderungsdefinition#^692e46|Testen von funktionalen Anforderungen]] und [[Anforderungsdefinition#^a713b5|Testen von nicht-funktionalen Anforderungen]] 
- Einsatz in realer Systemumgebung sicherstellen

## Abnahmetest
Definition: Der Abnahmetest prüft das Produkt aus Kunden- bzw. Anwendersicht bevor es produktiv eingesetzt wird – Werden die Anforderungen und Erwartungen des Kunden/Anwenders erfüllt?
Dabei wird der Kunde aktiv an dem Test beteiligt. Bei einer Individualsoftware der Auftraggeber oder Kunde. Bei einem Massenprodukt eine repräsentative Auswahl von Anwendern. 

### Mögliche Formen des Abnahmetests

#### Test auf vertragliche Akzeptanz
Es wird durch den Kunden geprüft, ob das Produkt den vertraglichen Anforderungen gerecht wird. Hierbei wird sich an die vertraglich vereinbarten Abnahmekriterien gehalten, was prinzipiell bereits intern durch den Systemtest abgedeckt ist, der Kunde bestimmt jedoch hierbei die Testfälle. Der Test findet außerdem in der Umgebung des Kunden statt.

#### Test auf Benutzerakzeptanz
Hierbei wird getestet, ob das Produkt die Erwartungen verschiedener Anwender erfüllt und einen positiven Eindruck hinterlässt oder ob das Produkt potenziell gravierende Fehler aufweist, die die Benutzerakzeptanz reduziert.
Akzeptanztests sind in Abhängigkeit der Individualisierung einer Software durchzuführen. Für kundenspezifische Individualsoftware müssen zwangsläufig alle Anforderungen der speziellen Anwendergruppe erfüllt werden. Für Standardsoftware ist es aufgrund der Vielzahl verschiedener Anwendergruppen generell schwierig, allgemeine Akzeptanz zu erreichen.

#### Feldtest
Es findet eine Auslieferung von stabilen Vorabversionen der Software (Beta-Version) an einen repräsentativ ausgewählten Kundenkreis statt. Dadurch kann der Kunde bereits vorher das Produkt in seiner jeweiligen produktiven Systemumgebung testen und Fehlerwirkungen protokolieren.
Alternativ vorab ein Alpha-Test einer Vorabversion (Alpha-Version). Repräsentative Anwender in der Umgebung des Herstellers nehmen diesen Test vor.
Der Feldtest soll über den Systemtest hinaus sicherstellen, dass dass die Software in einer Vielzahl verschiedener Umgebungen ausführbar ist. Die Nutzung von Feldtests senkt den Aufwand des Systemtests und ermöglicht weitaus umfassendere Tests (Ermöglichung von Tests in unterschiedlichen Umgebungen).

#### Testen nach der Produktabnahme
Der Kunde hat das Produkt abgenommen und es in Produktion gebracht. Die eigentliche Entwicklungsphase und die damit verbundenen Tests sind bereits abgeschlossen, aber die Software selbst steht noch am Anfang ihrer Lebenszeit. Sie wird oft über viele Jahre eingesetzt und auch weiterentwickelt.
- Sie ist sicher nicht fehlerfrei und wird deshalb weiter bearbeitet.
- Sie muss an neue Bedingungen angepasst oder in neue Umgebungen integriert werden.
Jede neue Produktversion, jedes Update und jede andere Veränderung muss erneut getestet werden!
Softwarewartung unterscheidet zwei Arten von Tätigkeiten
- Eigentliche Wartung: Beseitigung von Fehlern, die bereits seit Entwicklung der Software vorhanden sind
- Softwarepflege: Anpassungen der Software an geänderte Einsatzbedingungen
Darüber hinaus kann die Software außerdem um neue Schnittstellen und Funktionalitäten erweitert werden. Hierfür sollte man jedoch erneut das Vorgehensmodell durchlaufen.

Test einer bereits getesteten Software, um zu prüfen, ob durch Änderungen (z. B. nach Fehlerkorrektur) neue Fehler entstanden sind nennt man Regressionstest. Regressionstests werden damit bereits vor Produktabnahme benötigt und eingesetzt. Diese Regressionstests können wiederum in:
- Fehlernachtest (auch Retest genannt)
	- Wiederholte Ausführung von Testfällen, die Fehlerwirkungen gezeigt haben, um nachzuweisen, dass der Fehler behoben wurde.
	- Fehlernachtest ist damit ein Teil des Regressionstests
- Test der geänderten Funktionalität
	- Test aller Softwareteile, an denen Änderungen vorgenommen wurden
- Test neuer Funktionalität
	- Test ausschließlich neuer Programmkomponenten
	- Diese sind vorab als Komponente etc. schon getestet worden
- Vollständiger Regressionstest
	- Kompletter Systemtest wird durchgeführt / wiederholt
unterteilt werden.
Eine Kombination aus Tests der geänderten Teile (Fehlernachtest etc.) und einer Auswahl von Testfällen des Systemtests (z. B. gemäß der Priorisierung der zu testenden Funktionen) wird meist den Anforderungen am ehesten gerecht.
