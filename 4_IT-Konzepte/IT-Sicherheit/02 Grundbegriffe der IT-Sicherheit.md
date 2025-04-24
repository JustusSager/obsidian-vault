### Safety (Funktionssicherheit) ^228645
Das System funktioniert wie vorhergesehen. 
- Safety ist die Absicherung des Menschen vor der Maschine.
- Schutz vor unbeabsichtigten Schäden.
### Security (Informationssicherheit) ^ec9f9a
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
