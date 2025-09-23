termAgenten sollen:
- autonom mit ihrer Umwelt agieren
- durch Sensoren ihre Umwelt wahrnehmen (Perzepte)
- mithilfe ihrer Effektoren ihre Umwelt manipulieren (Aktionen)
![[agenten_und_umwelt.jpg|400]]
# Arten von Agenten
## Rationaler Agent
- ... machen das "Richtige"
- agiert so, dass gegebene Ziele erreicht werden unter folgenden Voraussetzungen:
	- Eindrücke von der Umwelt sind korrekt
	- Überzeugungen sind richtig
- Rationales Denken ist Voraussetzung für rationales Handeln, allerdings keine notwendige Voraussetzung.
	- Ein bisschen Widerspruch?
- Zur Beurteilung eines rationalen Agenten müssen objektive Performanzkriterien definiert werden
- Optimales Verhalten ist häufig unmöglich, da:
	- nur eine unvollständige Wahrnehmung der Umwelt möglich ist
		- -> Optimierung unter Unsicherheiten
	- eine hohe Berechnungskomplexität vorhanden ist
		- -> Optimierung unter Ressourcenbeschränkung
- Es handelt anhand seines Wissens und seiner Wahrnehmung und versucht die Performanz zu maximieren
- Rationales Handeln ist abhängig von:
	- Performanzkriterien (Ziele)
	- Wahrnehmungssequenzen
		- In der Regel ist eine aktive Wahrnehmung nötig
	- Wissen über die Welt
	- mögliche Aktionen
### Idealer rationaler Agent
- Für alle möglichen Wahrnehmungssequenzen und dem gegebenem Wissen über die Welt, wird die Aktion ausgewählt, welche die Performanz maximiert.
- Realisiert durch die Agentenfunktion:
  $Wahrnehmungssequenz * Weltwissen \to Aktion$ 
### Beispiele für rationale Agenten
- Medizinisches Diagnosesystem
	- Perzepte: Symptome, Antworten von Patienten
	- Aktionen: Fragen stellen, Tests durchführen
	- Ziele: Gesunder Patient, Minimierung von Kosten
	- Umgebung: Krankenhaus, Patient
- Interaktiver Englisch-Tutor
	- Perzepte: Eingegebene Worte
	- Aktionen: Übungsaufgaben stellen, Korrektur
	- Ziele: Maximierung der Testergebnisse
	- Umgebung: Gruppe von Studierenden
- Satellitenbild-Analysesystem
	- Perzepte: Bildpunkte unterschiedlicher Helligkeit
	- Aktionen: Kategorisierung des Bildmaterials
	- Ziele: Korrekte Kategorisierung
	- Umgebung: Bilder des Satelliten
### Vorteile
- rationales Handeln umfasst im Allgemeinen rationales Denken
- rationales Verhalten sollte allgemeinen Regeln folgen
	- Zugänglichkeit für die wissenschaftliche Betrachtung
	- Sicht der Mathematik, Informatik und Ingenieurswissenschaften wird gestärkt
		- Definierbarkeit, Messbarkeit, Beweisbarkeit
## Allwissender Agent
Ein allwissender Agent ...
- kennt sämtliche tatsächlichen Effekte seiner Aktionen
- ist eher theoretisch, wegen Beschränkungen wie Ressourcen und Umweltwahrnehmung
# Umgebung von Agenten
- vollständig Beobachtbar  vs. teilweise Beobachtbar
  Sind alle relevanten Aspekte der Welt den Sensoren zugänglich
- Einzelagent vs. Multiagent
  Hängt die Welt von einem oder von mehreren Agenten ab?
- deterministisch vs. stochastisch
  Hängt der Weltzustand allein vom jetzigen Zustand und der ausgeführten Aktion ab?
- episodisch vs. sequentiell
  Ist die Qualität einer Aktion nur von ihr abhängig oder auch con vorherigen Zuständen?
- statisch vs. dynamisch
  Kann sich die Welt ändern, während der Agent reflektiert?
- diskret vs. kontinuierlich
  Ist die Welt abzählbar?
# Struktur von Agenten
Die Struktur eines Agenten setzt sich zusammen aus ...
- dem Agentenprogramm
- der Agentenarchitektur, die auch die Schnittstelle zur Umwelt realisiert (Perzepte, Aktionen)
- Die Bewertung eines Agenten ist nicht Teil des Agenten, sondern erfolgt von außen.
Pseudocode:
```
function AGENT (Perzept) returns Aktion
	static: Wissen
	Wissen <- UPDATE-MEMORY(Wissen, Perzept)
	Aktion <- CHOOSE-BEST-ACTION(Wissen)
	Wissen <- UPDATE-MEMORY(Wissen, Aktion)
	
	return Aktion
```
## tabellengesteuerter Agent
