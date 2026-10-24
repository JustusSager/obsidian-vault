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

# Rechtsgrundlagen 

## Sorgfaltspflicht
#TODO Sorgfaltspflicht

## Datenschutz-Grundverordnung (DSGVO)
- strenge Regulierungen zum Schutz von [[Glossar#Personenbezogene Daten|Personenbezogenen Daten]] auf EU-Ebene.
	- gilt grundsätzlich in der gesamten EU, ohne das dies in nationales Recht übernommen werden muss.
- vergleichsweise hohe Strafen um auch großen Unternehmen zu treffen.
- betroffene Personen müssen über Verarbeitung der Daten informiert werden.
	- Personen müssen einwilligen wenn Unternehmen [[Glossar#Personenbezogene Daten|personenbezogene Daten]] erheben.

## IT-Sicherheitsgesetz und KRITIS-Verordnung
**Ziel** ist es kritische Infrastruktur besser zu Schützen
- An der Stromversorgung hängt eine ganze Reihe an Infrastruktur die alle angewiesen auf eine dauerhafte stabile Stromversorgung.
- betroffene Unternehmen müssen Systeme zur Angriffserkennung einsetzen.
	- kritische Infrastrukturen: https://www.bbk.bund.de/DE/Themen/Kritische-Infrastrukturen/Sektoren-Branchen/sektoren-branchen_node.html

## EU Network and Information Security Directive 2 (NIS-2)
**Ziel:** Vereinheitlichung des Sicherheitsniveaus kritischer Infrastrukturen in der EU und Verbesserung der Zusammenarbeit in der Cybersicherheit zwischen EU-Ländern.
#TODO 

## Cyber Resilience Act (CRA)
- Europaweite Regelung zur Verbesserung der [[Glossar#Informationssicherheit|Informationssicherheit]] von digitale Produkten aller Art (**Produktsicherheit**)
- Hersteller von Geräten werden verpflichtet Sicherheitsupdates und Patches zur Verfügung zu Stellen.
	- Für die gesamte Lebenszeit, aber min. 5 Jahre

## Radio Equipment Directive (RED)
**Ziel:** Sicherheit von Geräten mit Funkverbindungen

## Hacking und Konsequenzen
**Strafgesetzbuch (StGB), § 202a Ausspähen von Daten**
- (1) Wer unbefugt sich oder einem anderen Zugang zu Daten, die nicht für ihn bestimmt und die gegen unberechtigten Zugang besonders gesichert sind, unter Überwindung der Zugangssicherung verschafft, wird mit Freiheitsstrafe bis zu drei Jahren oder mit Geldstrafe bestraft.
- (2) Daten im Sinne des Absatzes 1 sind nur solche, die elektronisch, magnetisch oder sonst nicht unmittelbar wahrnehmbar gespeichert sind oder übermittelt werden.

**Strafgesetzbuch (StGB), § 202b Abfangen von Daten**
Wer unbefugt sich oder einem anderen unter Anwendung von technischen Mitteln nicht für ihn bestimmte Daten (§ 202a Abs. 2) aus einer nichtöffentlichen Datenübermittlung oder aus der elektromagnetischen Abstrahlung einer Datenverarbeitungsanlage verschāt, wird mit Freiheitsstrafe bis zu zwei Jahren oder mit Geldstrafe bestraft, wenn die Tat nicht in anderen Vorschriften mit schwererer Strafe bedroht ist.

**Strafgesetzbuch (StGB), § 202c Vorbereiten des Ausspähens und Abfangens von Daten**
- (1) Wer eine Straftat nach § 202a oder § 202b vorbereitet, indem er
	- 1. Passwörter oder sonstige Sicherungscodes, die den Zugang zu Daten (§ 202a Abs. 2) ermöglichen, oder
	- 2. Computerprogramme, deren Zweck die Begehung einer solchen Tat ist, herstellt, sich oder einem anderen verschafft, verkauft, einem anderen überlässt, verbreitet oder sonst zugänglich macht, wird mit Freiheitsstrafe bis zu zwei Jahren oder mit Geldstrafe bestraft.
- (2) § 149 Abs. 2 und 3 gilt entsprechend.

**Zum "Hacker-Paragraphen":**
In Deutschland ist man nur in folgenden Fällen auf der sicheren (der legalen) Seite:
1. eigenes Netz
2. Lehre / Ausbildung
3. Explizite Ermächtigung liegt vor (z.B. Pen-Test)
4. Bug Bounty Programme

#TODO Absatz Hacking zusammenfassen