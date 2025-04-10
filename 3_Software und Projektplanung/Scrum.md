Siehe Quelle: https://scrumguides.org/scrum-guide.html
#TODO Scrum vervollständigen

# Rollen
## Product Owner ^5b2639


## Scrum Master ^499486


## Developer ^f7908e


# Artefakte
## Product Backlog ^2f9374
Das Produkt Backlog ist die Zielsetzung des gesamten Projekts, welche mit den Stakeholdern abgestimmt wird. Es ist die Planungsgrundlage für die Sprints.

Das Produkt Backlog besteht aus folgendem:
1. Product Goal
	- Das Ziel des Projekts
2. Aufgaben
	- Eine geordnete Liste an Aufgaben welche benötigt werden um das Produkt zu verbessern / um das Product Goal zu erreichen.

## Sprint Backlog ^48d745
Das Sprint Backlog ist eine vollständig transparente Dokumentation der Tätigkeiten innerhalb des Sprints. Es wird von den Developern für die Developer erstellt.

Das Sprint Backlog besteht aus 3 Aspekten:
1. Sprint Goal
	- Das Sprint Goal wird während des [[#^7bb76e|Sprint Planning]] festgelegt.
	- Das Sprint Goal beinhaltet was am Ende des Sprints erreicht sein soll. 
	- Es dient dazu, bei der Bearbeitung der Aufgaben, nicht den Fokus zu verlieren. Eine Art Leitlinie für den Sprint.
2. Aufgaben
	- Es werden Aufgaben aus dem [[#^2f9374|Produkt Backlog]] ausgewählt welche innerhalb des Sprints abgearbeitet werden sollen.
	- Diese Aufgaben können jedoch im laufe des Sprints noch angepasst und in ihrer Umsetzung verändert werden.
3. Die Ergebnisse der [[#^2ab3fb|Sprint Retrospective]], festgehalten für künftige Sprints.

## Increment ^8c2259
Das Increment besteht aus folgendem:
1. Definition of Done

# Events
## Sprint
Ein Sprint ist das Basisevent, von dem die anderen Events teil sind. Ein Sprint hat immer eine feste Länge von einem Monat oder weniger. Durch diesen festen Intervalle kann eine Voraussehbarkeit des Projekts durch regelmäßige Inspektion und Überarbeitung der Ziele sichergestellt werden.

### Sprint Ablauf:
1. Sprint Planning
   Zu beginn des Sprints.
2. Daily Scrum
   Täglich während des Sprint. Hiervon wird der Arbeitstag begleitet
3. Sprint Review
   Gegen Ende des Sprints.
4. Sprint Retrospective
   Als letztes Event des Sprints.
## Sprint Planning ^7bb76e
- Wird immer zu beginn eines neuen Sprints durchgeführt.
- Das gesamte Scrum Team arbeitet gemeinsam an dem Plan für den kommenden Sprint.
- Product Owner stellt sicher, dass die Anwesenden bereit sind, die wichtigsten Punkte des Product Backlogs zu besprechen.
- Das Scrum Team kann auch externe einladen.
- Zeit ist begrenzt auf 8 Stunden oder weniger.

Hauptthemen der Sprint Planung:
1. Warum ist dieser Sprint von Wert?
   Product Owner schlägt vor, wie das Produkt den Wert für die Stakeholder steigern kann. Das gesamte Team diskutiert mit.
2. Was kann in diesem Sprint umgesetzt werden?
   In Diskussion mit dem Product Owner, wählen die Developer die zu entwickelnden Punkte aus dem [[#^2f9374|Product Backlog]] aus, welche in diesem Sprint umgesetzt werden sollen.
3. Wie werden die ausgewählten Punkte umgesetzt?
   Die Developer entwickeln für jeden ausgewählten Punkt einen Plan, wie dadurch ein [[#^8c2259|Increment]] entsteht, welches der "Definition of Done" entspricht.

Das Sprint Goal, die aus dem [[#^2f9374|Product Backlog]] gewählten Punkte und der Plan der Umsetzung dieser Punkte werden als [[#^48d745|Sprint Backlog]] zusammengefasst.

## Daily Scrum
- Fortschritt in Richtung Sprint Goal begutachten.
- Sprint Backlog ggf. anpassen
- anstehende Arbeit planen
- 15-Min Event der Developer. Scrum Master und Product Owner nehmen nur teil, wenn sie auch als Entwickler aktiv sind.
- Die Developer können jede Strategie verwenden, die sie möchten.
- soll Kommunikation und schnelle Entscheidungsfindung fördern.
- Ist jedoch kein Ausschluss von anderen Besprechungen die pot. mehr ins Detail gehen.

## Sprint Review
- Das Scrum Team präsentiert die Ergebnisse des Sprints den Stakeholdern und den den Fortschritt in Richtung Product Goal.
- Scrum Team und Stakeholder betrachten gemeinsam was im Sprint geschafft wurde.
- [[#^2f9374|Product Backlog]] kann hier mit neuen Ideen angepasst werden.
- Es sollte nicht nur auf eine Präsentation des Scrum Teams reduziert werden.
- Zeit begrenzt auf maximal 4 Stunden. 

## Sprint Retrospective ^2ab3fb
- Scrum Team untersucht wie der letzte Sprint lief und was verbessert werden könnte. 
- Scrum Team stellt heraus, welche Änderungen die Effektivität des kommenden Sprints erhöhen könnte.
- Änderungen können auch im [[#^48d745|Sprint Backlog]] festgehalten werden.
- Sprint Retrospective wird als letzter Schritt des Sprints durchgeführt, um den Sprint zu beenden.
