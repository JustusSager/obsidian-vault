# `metasploit`
CLI Schnittstelle zu einer Datenbank mit bekannten Sicherheitslücken und Skripten zu dessen Ausführung.
``` bash
msfconsole # metasploit starten
search <service> # suchen nach Lücken in service
info <id> # info zu gefundenen
	-d # weitere infos
use <id oder voller Pfad> # Exploit nutzen
show options # Optionen anzeigen
set <Parameter> <Wert> # Parameter setzen
run # exploit starten
```
# `nmap` ^313460
Open Source Werkzeug für Netzwerk-Scans und Sicherheitsüberprüfung.
### Port scan durchführen:
``` bash
sudo nmap -sS -p <Ports> <IP-Ziel>
	-sS # SYN-Scan (TCP)
	-p <Ports> # Ports die überprüft werden sollen. (Kommagetrennte Liste)
	-sV # finde die Software (+ Version) an dem Port heraus
	-v # verbose
	-vv # very verbose
	-O # versucht Betriebssystem herauszufinden
```
# `hydra`
### Befehl
``` bash
hydra <options> <IP-Adresse> <Dienst>
	-l <> # Benutzernamen eingeben
	-L <Dateiname> # Eine Datei mit Benutzernamen angeben
	-p <> # Passwort eingeben
	-P <Dateiname> # Eine Datei mit Passwörtern angeben
	-t <>
```
# `hping3` ^3cba1b
### SYN-Flooding
``` bash
sudo hping3 <options> <Ziel-IP>
	-c <Paketzahl> # Anzahl der Pakete z.B. 15000
	-d <Paketgröße> # Paketgröße in Bytes z.B. 120
	-S # setzt das SYN-Flag (TCP)
	-p <Port> # Zielport
	-w <Fenstergröße> # Fenstergröße z.B. 64
	--flood # sendet Pakete so schnell wie möglich
```
# `scapy`
### Starten von `scapy`
``` bash
sudo scapy
```
### Befehle innerhalb der `scapy` Konsole
``` bash
lsc() # List commands
ls(...) # Datenfelder des angegebenen Protokols anzeigen
	- (Ether) # Ethernet Protocol
	- (IP) # IP Protocol
	- (ICMP) # ICMP Protocol
send(<paketname>) # verbereitetes Paket senden
ans, unans = sr(<paketname>) # Paket senden und antwort erwarten
	# Gibt eine Liste an Antworten zurück
	# ans -> erfolgreich
	# unans -> nicht beantwortet
```
### Echo durchführen
``` bash
# Paket vorbereiten
paket = IP(dst="<IP-Ziel>", ttl=13)/ICMP()/"Irgendein Payload"

# Paket senden
ans, unans = sr(paket)

```
### Port Scan durchführen
``` bash
# Paket vorbereiten
paket = IP(dst="<IP Ziel>")/TCP(sport=<sport>, dport=<dport>, flags="S")
	# <sport> -> der Port auf an den geantwortet wird
	# <dport> -> Der Port der geprüft wird, kann auc eine Liste von Ports sein

# Paket senden
ans, unans = sr(paket)
```
# `aircrack-ng`
https://www.aircrack-ng.org/
Meine uralte Dokumentation als ich im Hacker Fieber war.
#TODO aircrack-ng aufarbeiten und updaten
### WLAN Hash abgreifen
``` bash
# Nach Programmen suchen die den Monitor Modus aufhalten.
airmon-ng check
# Diese Programme beenden
airmon-ng check kill
# Monitor Modus der Wlan Karte starten.
airmon-ng start <WlanKarte>
# Netzwerke in Reichweite anzeigen
airodump-ng <WlanKarte>
# Handshake abgreifen starten
airodump-ng --bssid <BSSID> -c <Channel> --write <Dateiname> <WlanKarte>
# Geräte im Netzwerk deathentifizieren
airodump-ng --deauth <Anzahl> -a <BSSID> <WlanKarte>
```
# `GoPhish` ^7dddde
Software zum aussenden und überwachen von Phishing E-Mails.
- Linux
- Web-basiert
### Konfiguration
- Default Admin Webpage Port: 3333
- Default Username: admin
- Default Passwort: phishing
### Sending Profile
Hier wird die Verbindung zu einem E-Mail Server konfiguriert, von dem die Mails versendet werden.
#### Konfiguration:
- Interface Type: SMTP
- SMTP From: (vorgespielte) Absende-Adresse des Mailservers
- Host: Serveradresse des SMTP Mailservers. 
	- Siehe dazu: [[MailHog]].
- Username/Password: Anmeldedaten des Mailservers

### Landing Pages
Hier können Fake Websites konfiguriert werden, auf die der Link in der Mail verweist.
### Email Templates
Hier können E-Mails formuliert werden, die rausgeschickt werden.
#### Mail im HTML Format
``` html
<html>
<head>
	<title></title>
	<meta charset="utf-8">
</head>
<body>
<!-- Hier den Inhalt der Mail reinschreiben -->
</body>
</html>
```
#### Link zur Landing Page einbinden
``` html
<a href="{{.URL}}">TEXT</a>
```
Hiermit kann ein Link zu der in der Campaign angegebenen Landing Page eingebettet werden.
### Users & Groups
Hier werden die Empfänger der Mails angegeben.
### Campaigns
Hier läuft alles zusammen.
#### Konfiguration
- Email Template: Das erstellte Email Template wählen. Siehe weiter oben.
- Landing Page: Die erstellte Landing Page wählen. Siehe weiter oben.
- URL: die URL des GoPhish Servers. z.B. "http://192.169.233.5"
