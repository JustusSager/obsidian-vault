# Motivation hinter IT-Sicherheit
Dem Allianz Risk Barometer zufolge stellen Cyber-Vorfälle das größte Risiko für Unternehmen dar. Und das bereits zu wiederholten mal
	Quelle: https://commercial.allianz.com/content/dam/onemarketing/commercial/commercial/reports/Allianz-Risk-Barometer-2025.pdf 
## IT-Sec eine rein technische Herausforderung?
#TODO IT-Sec eine rein technische Herausforderung?
![[Pasted image 20250326211928.png]]
# Schutzziele ^b9a4e3
### Modelle
Hier sind 2 verschiedene Modelle die die wichtigsten Schutzziele dargestellt. Links die CIA-Triade, Rechts das VIVA-Modell. Im vergleich fällt auf, dass in der CIA-Triade die Authentizität fehlt.
![[schutzziele_modelle.png]]
### Vertraulichkeit ^58c934
(engl. confidentiality)
Eine unautorisierte Informationsgewinnung ist nicht möglich.
 -> Informationen sind sicher vor unbefugtem lesenden Zugriff.
### Integrität ^78c88f
(engl. integrity)
Eine unautorisierte und unbemerkte Manipulation der zu schützenden Daten ist nicht möglich.
 -> Manipulationsschutz, Informationen sind sicher vorm unbefugten schreibenden Zugriff.
### Verfügbarkeit ^ae9f9a
(engl. availability)
Authentifizierte und autorisierte Parteien können ihre Berechtigungen wahrnehmen, ohne dabei unautorisiert beeinträchtigt zu werden.
 -> erlaubte Zugriffe sind jederzeit möglich.
### Authentizität ^189d25
(engl. authenticity)
Die Echtheit und Glaubwürdigkeit ist gegeben und kann anhand einer eindeutigen Identität und charakteristischen Eigenschaften überprüft werden.
Das Schutzziel Authentizität kann sowohl für Subjekte als auch für Objekte gelten. Den Nachweis von Subjekten nennt man Authentifizierung. Beim Nachweis von Objekten geht es darum, zu prüfen, dass das Objekt tatsächlich dem zugehörigen Subjekt zugeordnet werden kann.
 -> Überprüfen, ob etwas dass ist, was es behauptet zu sein.
### Verbindlichkeit/Nichtabstreitbarkeit ^6c70b9
(engl. non-repudiation)
Es ist nicht möglich, dass eine Partei nachträglich ihre Beteiligung an einer (Trans-) Aktion abstreiten kann.
 -> eindeutiger Nachweis, dass eine "Person" an einem Prozess beteiligt war.
### Anonymisierung
(engl. anonymisation)
Veränderung von personenbezogenen Daten, so dass Einzelangaben nicht mehr einer bestimmten oder bestimmbaren Person zugeordnet werden können.
 -> siehe auch Pseudonymisierung
# Hacking
### Was ist ein Hacker?
1. Black Hats
   ... nutzen ihr Wissen für kriminelle Aktivitäten
2. White Hats
   ... halten sich an Recht und Gesetze sowie die Hacker-Ethik.
   ... verwenden ihr Wissen zur Verbesserung von (Computer-) Systemen.
3. Gray Hats
   ... nehmen es mit den Regeln nicht ganz so genau.
   ... verfolgen oft höhere Ziele (Verbesserung der Gesellschaft).
### Hacking Verfahren
- Network Hacking
- Password Hacking
- Backdoors
- Schadsoftware
- Denial of Service
### Angriffsvektor
(engl. attack vector)
Ein Angriffsvektor bezeichnet einen Angriffsweg oder eine Angriffstechnik um die Schutzziele eines Systems zu kompromittieren. Dazu nutzt der Angreifer eine oder mehrere Schwachstellen verteilt oder mehrstufig aus.
**Beispiel:**
Angriffsvektoren einer IT-Infrastruktur einer Firma oder organisation wären:
- Schadsoftware per Web, Mail, App, usw.
- Angriff auf Firmengerät unterwegs
- Zugriff auf Daten in der Cloud
- Home Automation, Schließsysteme, IoT-Geräte, usw.
- (Spear) Phishing
- Social Engineering
- verlorenes/gestohlenes Smartphone oder Notebook
- Angriff von innen, Sabotage
- Network Hacking
# Bedrohungs- und Risikoanalyse
Ziel: "Security by Design"
	beim Entwurf eines Systems werden direkt Überlegungen zur Informationssicherheit des Geräts angestellt und entsprechende Gegenmaßnahmen im Entwurf vorgesehen.
### Bedrohungsbaum
(engl. attack tree)
Ein Bedrohungsbaum ist eine graphische Darstellung der möglichen Bedrohungen in Form eines Baums. 
Die Wurzel ist das Ziel des Angriffs. Die Verzweigungen repräsentieren verschiedene Angriffspfade. Jeder Knoten beschreibt eine Teilbedingung, die erfüllt sein muss, ggf. können diese auch UND-Verknüpft werden.
![[beispiel_bedrohungsbaum.png]]
### Bedrohungsanalyse mit STRIDE
<b>S</b>poofing - Verschleierung der Identität ([[#^189d25|Authentizität]])
<b>T</b>ampering - Manipulation ([[#^78c88f|Integrität]])
<b>R</b>epudiation - Abstreitbarkeit ([[#^6c70b9|Verbindlichkeit/Nichtabstreitbarkeit]])
<b>I</b>nformation Disclosure - Verletzung der Privatsphäre ([[#^58c934|Vertraulichkeit]])
<b>D</b>enial of Service - Dienstverweigerung ([[#^ae9f9a|Verfügbarkeit]])
<b>E</b>levation of Privilege - Rechteausweitung

Vorgehen:
Jede der Kategorien bewertet in:
	1 - geringes Risiko
	2 - mittleres Risiko
	3 - hohes Risiko

Die Werte ergeben die Gesamtbewertung von 6 bis 18.
$$ score = S+T+R+I+D+E$$

Kritik:
Die Bewertung der Kategorien in gerade einmal 3 Risikoklassen sorgt für erhebliche Unterschiede in der Gesamtbewertung durch die unterschiedliche subjektive Wahrnehmung der Durchführenden.
### Risikoanalyse mit DREAD
Damage - Schadenspotenzial
Reproducibility - Reproduzierbarkeit
Explotability - Ausnutzbarkeit
Affected Users - betroffene Benutzer/-innen
Discoverability - Auffindbarkeit

**Vorgehen:**
Jeder Kategorie wird von 0 (kein Risiko) bis 10 (hohes Risiko) bewertet.

Die Werte ergeben eine Gesamtbewertung von 0 bis 10.
$$ score = \frac{D+R+E+A+D}{5} $$
![[dread_scale.png]]

### Common Vulnerability Scoring System v4.0 (CVSS)
#TODO Common Vulnerability Scoring System 
