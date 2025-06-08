# Prinzipien zum Entwurf sicherer Systeme
#### Erlaubnisprinzip
`fail-safe defaults`
Jeder Zugriff ist zunächst grundsätzlich verboten (engl. default deny). Nur durch explizite Erlaubnis kann das Zugriffsrecht gewährt werden.

#### Vollständigkeitsprinzip
`complete mediation`
Jeder Zugriff auf jedes Objekt ist auf seine Zulässigkeit zu prüfen. Das Prinzip erzwingt, dass Zugriffskontrolle grundsätzlich aus Sicht des gesamten Systems betrachtet werden muss.

#### Prinzip der minimalen Rechte
`least privilege, need to know`
Jedes Subjekt erhält nur die Zugriffsrechte, die es zur Wahrnehmung seiner Aufgaben benötigt.

#### Prinzip der wirtschaftlichen Mechanismen
`economy of mechanism`
Der Entwurf der Sicherheitsfunktionen sollte so einfach und klein wie möglich sein.

#### Prinzip des offenen Entwurfs
`open design`
Das Design der Sicherheitsfunktionen sollte nicht geheim gehalten, sondern offen gelegt werden. Die Entkopplung der Sicherheitsfunktionen von z.B. kryptographischen Schlüsseln erlaubt die Untersuchung des Designs durch Dritte, ohne dabei Gefahr zu laufen, konkrete Daten zu kompromittieren.

# Sicherheitsgrundfunktionen
- Identifikation und Authentifikation
- Rechteverwaltung
- Rechteprüfung
- Beweissicherung
- Wiederaufbereitung
	- Keine Daten im Cache hinterlassen.
- Gewährleistung der Funktionalität

