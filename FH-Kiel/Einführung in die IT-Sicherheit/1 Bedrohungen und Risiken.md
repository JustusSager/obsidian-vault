Quellbezug:
- Vorlesung 1 und die dazugehörigen Folien 
# Motivation hinter IT-Sicherheit

Dem Allianz Risk Barometer zufolge stellen Cyber-Vorfälle das größte Risiko für Unternehmen dar. Und das bereits zu wiederholten mal
	Quelle: https://commercial.allianz.com/content/dam/onemarketing/commercial/commercial/reports/Allianz-Risk-Barometer-2025.pdf 

# Grundbegriffe

### Safety (Funktionssicherheit) ^228645
Das System funktioniert wie vorhergesehen. 
 -> Safety ist die Absicherung des Menschen vor der Maschine.

### Security (Informationssicherheit)
Das System nimmt nur Zustände ein, die zu keinem unautorisiertem Zugriff (lesend und schreibend) führen.
Erweitert [[#^228645|Funktionssicherheit]] um den Schutz der enthaltenen Informationen.
	IT-Sicherheit: Eigentlich nennt man IT-Sicherheit Informationssicherheit
	Cybersicherheit: teils analog zu Informationssicherheit
	Protection: Backups, etc von Informationen (nicht Modulrelevant)

### Daten^67e685
Daten sind kontextfreie Angaben, ohne diese zu interpretieren.

### Informationen
sind [[#^67e685|Daten]], die kontextbezogen interpretiert werden und zu einem Erkenntnisgewinn führen. 
Informationen bzw. Daten sind grundsätzlich <b>schützenswerte Güter</b> (engl. assets)

### Angriff
ist der unautorisierte Zugriff bzw. Zugriffsversuch auf ein System bzw. die Informationen eines Systems.

### Operational Technology (OT)
Hard- und Software, die zur Steuerung und Überwachung physischer Maschinen und industrieller Anlagen eingesetzt werden (inkl. zugehöriger Prozesse).
Hier wird auf eine bewusste Trennung zwischen Informationstechnologie (IT) (wie dem Internet) und der Steuerung von z.B. großen Industrieanlagen gesetzt. Eine solche Trennung lässt sich meist jedoch nicht praktisch umsetzen.

### Schwachstelle
(engl. weakness)
Unter einer Schwachstelle versteht man grundsätzlich einen sicherheitsrelevanten Fehler.

#### Arten von Schwachstellen
1. Speicherzugriff (Pufferüberlauf, fehlerhafte Zeiger/Pointer)
   Ein Programm schreibt in Speicherbereiche, die für andere Zwecke reserviert sind, oder liest Speicherbereiche, die keine gültigen Daten mehr enthalten
2. Eingabevalidierung
   Zu verarbeitende Daten bzw. Eingaben werden nicht ausreichend geprüft, wodurch Code in ein Programm eingeschleust werden kann, den dieses dann ausführt.
   -> Never trust user input!
3. Race Condition
   Parallel von mehreren Prozessoren/Kernen auszuführende Code-Teile werden in einer für das Programm ungünstigen Reihenfolge ausgeführt.
4. Privilege Escalation/Confusion
   Anweisungen können mit höheren Rechten als vorgesehen ausgeführt werden.

### Verwundbarkeit
(engl. vulnerability)
Eine Verwundbarkeit ist eine Schwachstelle, über die die Schutzziele eines Systems umgangen, getäuscht oder unautorisiert modifiziert werden können.

#### Arten von Verwundbarkeiten
- Design
  z.B. hartverdrahtetes Passwort, welches nicht geändert werden kann und quasi im Handbuch für das Gerät mit drinsteht.
  Eine (mehr oder weniger) bewusste Designentscheidung, die sich als Verwundbar herausstellt.
- Implementierung
  z.B. TLS Heartbeat -> Heartbleed. Arbeitsspeicherdaten von Servern konnten mit TLS Heartbeat ohne Authentifizierung "mitgehört" werden.
  Ein Fehler in der Implementierung (Umsetzung) führt zu einer Verwundbarkeit. z.B. fehlende Überprüfung von User Input.
- Konfiguration
	- fehlende Verschlüsselung der Website
	- automatischer Login als Superuser auf Websites (war z.B. eine Standardkonfiguration bei einem selbstbau SmartHome Systems)
	- default password
	- (...)

### Bedrohung 
(engl. threat)
Eine Bedrohung liegt vor, wenn ein Angreifer beabsichtigt, durch Ausnutzen einer oder mehrerer Verwundbarkeiten eines Systems die Vorkehrungen zur Gewährleistung der Schutzziele zu kompromittieren.

### Risiko
(engl. risk) 
Ausgehend von einer Bedrohung beschreibt das Risiko die Wahrscheinlichkeit des Eintritts eines Schadensereignisses unter Berücksichtigung der Höhe des zu erwartenden Schadens.
Analogie:
	Ein Frontalzusammenstoß mit 130 kmh von 2 Autos bringt einen sehr hohen Schaden. Ein Zusammenstoß mit einem Baum bei 5 kmh hingegen bringt nur einen sehr geringen Schaden. Die Wahrscheinlichkeit für das Erste ist jedoch scheinbar so gering, dass annähernd jeder bereit ist dieses Risiko in Kauf zu nehmen und dennoch Auto zu fahren. Also dennoch ein geringes Risiko.
Um zu bewerten, ob von einer Bedrohung eine konkrete Gefährdung ausgeht, müssen zunächst die zu schützenden Güter bewertet, das Schadenspotenzial bestimmt und die Eintrittswahrscheinlichkeit abgeschätzt werden.

## IT-Sec eine rein technische Herausforderung?
#TODO
![[Pasted image 20250326211928.png]]

# Schutzziele

### Modelle
Hier sind 2 verschiedene Modelle die die wichtigsten Schutzziele dargestellt. Links die CIA-Triade, Rechts das VIVA-Modell. Im vergleich fällt auf, dass in der CIA-Triade die Authentizität fehlt.
![[schutzziele_modelle.png]]

### Vertraulichkeit^58c934
(engl. confidentiality)
Eine unautorisierte Informationsgewinnung ist nicht möglich.
 -> Informationen sind sicher vor unbefugtem lesenden Zugriff.

### Integrität ^78c88f
(engl. integrity)
Eine unautorisierte und unbemerkte Manipulation der zu schützenden Daten ist nicht möglich.
 -> Manipulationsschutz, Informationen sind sicher vorm unbefugten schreibenden Zugriff.

### Verfügbarkeit^ae9f9a
(engl. availability)
Authentifizierte und autorisierte Parteien können ihre Berechtigungen wahrnehmen, ohne dabei unautorisiert beeinträchtigt zu werden.
 -> erlaubte Zugriffe sind jederzeit möglich.

### Authentizität ^189d25
(engl. authenticity)
Die Echtheit und Glaubwürdigkeit ist gegeben und kann anhand einer eindeutigen Identität und charakteristischen Eigenschaften überprüft werden.
Das Schutzziel Authentizität kann sowohl für Subjekte als auch für Objekte gelten. Den Nachweis von Subjekten nennt man Authentifizierung. Beim Nachweis von Objekten geht es darum, zu prüfen, dass das Objekt tatsächlich dem zugehörigen Subjekt zugeordnet werden kann.
 -> Überprüfen, ob etwas dass ist, was es behauptet zu sein.

### Verbindlichkeit/Nichtabstreitbarkeit^6c70b9
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

Beispiel:
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

Vorgehen:
Jeder Kategorie wird von 0 (kein Risiko) bis 10 (hohes Risiko) bewertet.

Die Werte ergeben eine Gesamtbewertung von 0 bis 10.
$$ score = \frac{D+R+E+A+D}{5} $$
![[dread_scale.png]]

### Common Vulnerability Scoring System v4.0 (CVSS)
#TODO siehe Foliensatz 01_it_sec_intro_handout Folie 32

