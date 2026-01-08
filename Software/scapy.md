#Informatik #IT-Sicherheit 
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