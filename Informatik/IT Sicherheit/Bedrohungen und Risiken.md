# Motivation hinter IT-Sicherheit
Dem Allianz Risk Barometer zufolge stellen Cyber-Vorfälle das größte Risiko für Unternehmen dar. Und das bereits zu wiederholten mal
	Quelle: https://commercial.allianz.com/content/dam/onemarketing/commercial/commercial/reports/Allianz-Risk-Barometer-2025.pdf 
## IT-Sec eine rein technische Herausforderung?
#TODO IT-Sec eine rein technische Herausforderung?
![[Pasted image 20250326211928.png]]
# Schutzziele
### Modelle
Hier sind 2 verschiedene Modelle die die wichtigsten Schutzziele dargestellt. Links die CIA-Triade, Rechts das VIVA-Modell. Im vergleich fällt auf, dass in der CIA-Triade die Authentizität fehlt.
![[schutzziele_modelle.png]]
Die Schutzziele lauten:
- [[Glossar#Vertraulichkeit|Vertraulichkeit]] (engl. confidentiality)
- [[Glossar#Integrität|Integrität]] (engl. integrity)
- [[Glossar#Verfügbarkeit|Verfügbarkeit]] (engl. availability)
- [[Glossar#Authentizität|Authentizität]]
	- Das Schutzziel Authentizität kann sowohl für Subjekte als auch für Objekte gelten. Den Nachweis von Subjekten nennt man Authentifizierung. Beim Nachweis von Objekten geht es darum, zu prüfen, dass das Objekt tatsächlich dem zugehörigen Subjekt zugeordnet werden kann.
- [[Glossar#Verbindlichkeit/Nichtabstreitbarkeit|Verbindlichkeit / Nichtabstreitbarkeit]]
- [[Glossar#Anonymisierung|Anonymisierung]]
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
# Bedrohungs- und Risikoanalyse
Ziel: "Security by Design"
	beim Entwurf eines Systems werden direkt Überlegungen zur Informationssicherheit des Geräts angestellt und entsprechende Gegenmaßnahmen im Entwurf vorgesehen.
### Bedrohungsbaum
(engl. attack tree)
Ein Bedrohungsbaum ist eine graphische Darstellung der möglichen Bedrohungen in Form eines Baums. 
Die Wurzel ist das Ziel des Angriffs. Die Verzweigungen repräsentieren verschiedene Angriffspfade. Jeder Knoten beschreibt eine Teilbedingung, die erfüllt sein muss, ggf. können diese auch UND-Verknüpft werden.
![[beispiel_bedrohungsbaum.png]]
### Bedrohungsanalyse mit STRIDE
<b>S</b>poofing - Verschleierung der Identität ([[Glossar#Authentizität|Authentizität]])
<b>T</b>ampering - Manipulation ([[Glossar#Integrität|Integrität]])
<b>R</b>epudiation - Abstreitbarkeit ([[Glossar#Verbindlichkeit/Nichtabstreitbarkeit|Verbindlichkeit/Nichtabstreitbarkeit]])
<b>I</b>nformation Disclosure - Verletzung der Privatsphäre ([[Glossar#Vertraulichkeit|Vertraulichkeit]])
<b>D</b>enial of Service - Dienstverweigerung ([[Glossar#Verfügbarkeit|Verfügbarkeit]])
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
