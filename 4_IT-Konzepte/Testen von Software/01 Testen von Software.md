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