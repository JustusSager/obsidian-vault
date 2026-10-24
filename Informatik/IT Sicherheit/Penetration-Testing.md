# Bestandteile eines Sicherheitschecks
## Schwachstellen-Scan
automatisiertes Verfahren um Schwachstellen im System zu finden

## Penetrationstest
Hier soll auch versucht werden die Schwachstellen auszunutzen  

## Security Audit
eine formalisierte Überprüfung eines Systems nach bestimmten Standards wie der ISO27001.

# Arten von Penetration-Tests
Lässt sich nach dem OSSTMM-Model aufteilen.

**Blind**
Der Angreifer weiß wenig über das Ziel, der Verteidiger weiß über den Angriff bescheid.
-> Die Fähigkeiten des Pentesters werden getestet
**Double Blind**
Der Angreifer weiß nichts über das Ziel und der Verteidiger weißt nichts über den Angriff
-> Ist am nächsten an der Realität
**Gray Box**
Der Angreifer weiß ein bisschen was. Der Verteidiger weiß über den Angriff bescheid.
-> Schwachstellen werden gesucht. Was findet der Angreifer so über das System raus?
**Double Grey**
Sowohl Angreifer als auch Verteidiger sind teilweise eingeweiht.
-> Eine Mischung der anderen Tests.
**Tandem**
Alle Informationen werden offen gelegt. 
-> Es wird spezifisch nach Schwachstellen in einem System gesucht.
**Reversal**
Die Angreifer kennen alle Informationen über das System. Die Verteidiger wissen von nichts.
-> Die Reaktion der Verteidiger wird getestet

# Ablauf eines Penetration-Tests

**1. Vorbereitung**
- Was soll raus kommen?
- Was soll getestet werden?
- Welche Geräte werden angefasst?
- In welchem Zeitraum findet der Test statt?

**2. Informationsbeschaffung**
- Möglichst viele Informationen über das System beschaffen wie möglich
- Ziel ist das System so gut kennen zu lernen wie möglich und den Aufbau des Systems zu verstehen.

**3. Bewertung der Informationen und Risikoanalyse**
- Bewertung der in **2.** zusammengetragenen Informationen
- Am besten hier nochmal vom Auftraggeber die geplante Vorgehensweise absegnen lassen, bevor es mit **4.** weiter geht.

**4. Penetration**
- Durchführung des Angriffs, Eindringen in System
- Einsatz von Exploit-Code

**5. Abschlussanalyse und Reporting**
- Zusammenfassung der Penetration-Tests
- Beinhaltet:
	- Eine kurze einfach verständliche (nicht technische) Zusammenfassung, mit einfach verständlichem Schweregrad (z.B. Ampel-Skala) für das Management
	- Technische Zusammenfassung und mögliche Lösungsmöglichkeiten für die IT Abteilung
	- Bewertung der Sicherheitslücke  