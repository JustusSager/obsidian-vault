![[passwort_hash.png]]
Beim erstellen eines Passworts wird der Hash des Passworts (zuzüglich eines `Salts`) in der Datenbank gespeichert. 
Zur Überprüfung eines Passworts wird der Hash des Passworts mit dem in der Datenbank gespeicherten Hash verglichen.
Siehe hierzu [[Kryptographie#Hash Funktionen|Hash Funktionen]].

# Online-Angriff gegen Passwörter
**Situation:**
- Angreifer kennt den Hash-Wert des Passworts nicht.
- Es muss mit einem Webserver (oder anderem IT-System) interagiert werden.
- Angreifer sendet potenzielles Passwort an Server.
- Server akzeptiert oder verwirft gesendetes Passwort des Angreifers.

**Gängige Sicherheitsmaßnahmen:**
- Beschränkung der Anzahl der Anmeldeversuche
- erzwungene Wartezeit nach Fehlversuch

# Offline-Angriff gegen Passwörter
**Situation:**
- Angreifer kennt Hash-Wert des Passworts.
	- z.B. durch Datenleak einer Datenbank.
- Angreifer kann für beliebige potenzielle Passwörter den zugehörigen Hash-Wert berechnen.
- Angreifer vergleicht Hash-Wert der Passworts mit selbst berechneten Hash-Werten.
- Angreifer hat beliebig viele Versuche.
**Sicherheitsmaßnahmen:**
- schwierig und aufwändig
- info@vk-gallion.de
