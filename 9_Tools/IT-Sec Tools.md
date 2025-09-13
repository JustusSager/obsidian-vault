# `nmap`
Open Source Werkzeug für Netzwerk-Scans und Sicherheitsüberprüfung.
#### Port scan durchführen:
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
#### Befehl
``` bash
hydra <options> <IP-Adresse> <Dienst>
	-l <> # Benutzernamen eingeben
	-L <Dateiname> # Eine Datei mit Benutzernamen angeben
	-p <> # Passwort eingeben
	-P <Dateiname> # Eine Datei mit Passwörtern angeben
	-t <>
```
# `hping3`
#### SYN-Flooding
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
#### Starten von `scapy`
``` bash
sudo scapy
```
#### Befehle innerhalb der `scapy` Konsole
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
#### Echo durchführen
``` bash
# Paket vorbereiten
paket = IP(dst="<IP-Ziel>", ttl=13)/ICMP()/"Irgendein Payload"

# Paket senden
ans, unans = sr(paket)

```
#### Port Scan durchführen
``` bash
# Paket vorbereiten
paket = IP(dst="<IP Ziel>")/TCP(sport=<sport>, dport=<dport>, flags="S")
	# <sport> -> der Port auf an den geantwortet wird
	# <dport> -> Der Port der geprüft wird, kann auc eine Liste von Ports sein

# Paket senden
ans, unans = sr(paket)
```