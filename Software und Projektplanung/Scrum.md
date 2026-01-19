#TODO Scrum vervollständigen

# Rollen
## Developer ^f7908e
Die Developer sind die, die an dem Projekt arbeiten.
Sie sind verantwortlich für:
- Erstellung eines Plans für den kommenden Sprint ([[#^48d745|Sprint Backlog]])
- Qualitätssicherung entsprechend der [[#^66e2c1|Definition of Done]].
- flexibel den Tagesplan entsprechend des Sprint Goals anpassen.
- Sich gegenseitig professionell in die Verantwortung ziehen.
## Product Owner ^5b2639
Der Product Owner ist eine Person und ist verantwortlich für:
- die Maximierung der Projektergebnisse des Scrum Teams.
- Entwicklung und eindeutige Kommunikation des Produkt Goals.
- Erstellung und klare Kommunikation des Product Backlogs.
- Sortierung/Priorisierung der Inhalte des Product Backlogs.
- Sicherstellen, dass das Produkt Backlog transparent und verständlich für alle ist.
Diese Arbeit kann der Product Owner selbst durchführen, oder an bestimmte Teammitglieder weitergeben. Dennoch bleibt der Product Owner in der Verantwortung.
## Scrum Master ^499486
Der Scrum Master ist verantwortlich für die Einhaltung der Scrum Richtlinien. Dabei geht es um folgende Punkte:
- Die Teammitglieder über die Verfahrensweisen aufklären und in deren Umsetzung unterstützen.
- Teamgeist-Entwicklung unterstützen und ggf. Anpassung der Teamzusammensetzung
- Sicherstellen, dass die [[#^f0f8b4|Scrum Events]] ordnungsgemäß durchgeführt werden.
- Die Effektivität des Teams sicherstellen.

# Artefakte
## Product Backlog ^2f9374
Das Produkt Backlog ist die Zielsetzung des gesamten Projekts, welche mit den Stakeholdern abgestimmt wird. Es ist die Planungsgrundlage für die Sprints.
Der `Product Owner` steht in der Verantwortung für die Korrektheit und Vollständigkeit des `Product Backlogs`.

Das Produkt Backlog besteht aus folgendem:
1. Product Goal
	- Das Ziel des Projekts
2. Aufgaben
	- Eine geordnete Liste an Aufgaben welche benötigt werden um das Produkt zu verbessern / um das Product Goal zu erreichen.

## Sprint Backlog ^48d745
Das Sprint Backlog ist eine vollständig transparente Dokumentation der Tätigkeiten innerhalb des Sprints. 
Es wird von den Developern für die Developer erstellt. Daher sind auch die `Developer` in der Verantwortung die Qualität des `Sprint Backlogs` sicherzustellen.

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
Das `Increment` ist Teil eines jeden Sprints. Die `Developer` arbeiten an der Weiterentwicklung des Projekts und sollen dabei am Ende die Erfüllung der `Definition of Done` und damit die des `Increments` sicherstellen.
Das Increment besteht aus folgendem:
1. `Definition of Done` ^66e2c1
	- Die `Definition of Done` besteht aus den qualitativen Bedingungen die jeder Increment erfüllen muss, damit das Increment mit übernommen wird.
	- Jedes `Increment` muss die Definition of Done erfüllen.
	- Beispiele dafür sind  
		- das Erfüllen der gestellten Anforderungen
		- Test und Review durch eine zweite Person
		- Dokumentation
		- Einhaltung der Styling Guidelines
		- . . .
	- 

# Events ^f0f8b4
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
- Es werden ggf. Maßnahmen überlegt die die Qualität der Ergebnisse sicherstellt oder verbessert.
- Änderungen sollten auch im [[#^48d745|Sprint Backlog]] festgehalten werden.
- Sprint Retrospective wird als letzter Schritt des Sprints durchgeführt, um den Sprint zu beenden.

# Weiteres
## Aufwand einer Aufgabe einschätzen
Für jede Aufgabe soll eingeschätzt werden wie viel "Zeit" für die Aufgabe benötigt wird. Diese Einschätzung wird jedoch nicht in einer Zeiteinheit gemacht, sondern mithilfe von `Story Points`
Eine Aufgabe sollte sich innerhalb eines bestimmten Rahmens an `Story Points` befinden. Falls eine Aufgabe zu groß wird sollte sie unterteilt werden, da sie sonst zu schwer einzuschätzen wird . Bei zu kleinteiligen Aufgaben wird der Administrations- und Einschätzungsaufwand zu groß als das es sich lohnt.
Am Ende müssen sich alle `Developer` auf eine Anzahl an `Story Points` einigen.

## Story Point
Ein `Story Point` ist eine Art Aufwandseinheit für Aufgaben. Hierbei einigt man sich im Team auf eine Tätigkeit, die als Referenzwert für die Aufwandseinschätzung verwendet wird. Dadurch soll die Aufwandsschätzung zwischen den Developern vergleichbarer werden. Ein Entwickler der etwas langsamer arbeitet als ein Anderer kommt bei der Aufwandsschätzung dadurch dennoch auf den selben Aufwand.
z.B. Als `Story Point` wird die Implementierung der [[OOP#Rule of Five|Rule of Five]] in einer Klasse angesetzt. Beim Einschätzen einer Aufgabe wird jetzt überlegt wie vielen Implementierungen der `Rule of Five` diese Aufgabe entspricht.
# Quelle
- https://scrumguides.org/scrum-guide.html
