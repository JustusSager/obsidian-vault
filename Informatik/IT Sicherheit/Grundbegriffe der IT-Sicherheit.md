## Arten von [[Glossar#Schwachstelle|Schwachstellen]]
1. Speicherzugriff (Pufferüberlauf, fehlerhafte Zeiger/Pointer)
   Ein Programm schreibt in Speicherbereiche, die für andere Zwecke reserviert sind, oder liest Speicherbereiche, die keine gültigen Daten mehr enthalten
2. Eingabevalidierung
   Zu verarbeitende Daten bzw. Eingaben werden nicht ausreichend geprüft, wodurch Code in ein Programm eingeschleust werden kann, den dieses dann ausführt.
   -> Never trust user input!
3. Race Condition
   Parallel von mehreren Prozessoren/Kernen auszuführende Code-Teile werden in einer für das Programm ungünstigen Reihenfolge ausgeführt.
4. Privilege Escalation/Confusion
   Anweisungen können mit höheren Rechten als vorgesehen ausgeführt werden.
## Arten von [[Glossar#Verwundbarkeit|Verwundbarkeiten]]
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
