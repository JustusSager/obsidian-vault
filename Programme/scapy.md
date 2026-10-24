---
erstellt am: 22.05.2026 08:58
tags:
  - Informatik
  - IT-Sicherheit
Deckblatt:
---
Wird zum Aufbau eigener Netzwerkpakete verwendet.

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

# Netzwerkpakete aufbauen
Netzwerkpakete werden durch das übereinander schichten von Protokoll-Headern aufgebaut. Siehe dazu [[Netzwerkprotokolle]] und [[OSI und TCP-IP Referenzmodell]].
``` bash
IP() / ICMP()
```
Protokolle werden mit `/` aufeinander aufgebaut. Innerhalb der Klammern kommen die Konfigurationen der einzelnen Protokolle. Alle Schichten und Felder, die nicht explizit gesetzt werden, werden mit den jeweiligen Standardwerten des Rechners bzw. des Betriebssystems automatisch versehen

## Ping (IP prüfen)
ein einzelner Ping, also ein ICMP-Echo-Request
``` bash
antwort = sr1(IP(dst="192.168.10.1") / ICMP(), timeout=2)
antwort.show()
```
- `sr1()` wartet bis zum Ablauf des Timeouts.
- `show()` zeigt alle Felder des Antwortpakets.

### Ping-Sweep (IP-Scan)
Zur Ermittlung von aktiven Hosts in einem Netzwerk, mithilfe eines ICMP-Echo-Requests.
``` bash
for i in range(1, 255):
	ziel = "192.168.10." + str(i)
	print(ziel)
	antwort = sr1(IP(dst=ziel) / ICMP(), timeout=1)
	if antwort:
		antwort.show()
```

## TCP SYN Anfrage (Port prüfen)
Um zu prüfen, ob auf einem Port eine Anwendung läuft, kann man eine TCP SYN Anfrage schicken, je nach Antwort ist der Port offen (Anwendung läuft), geschlossen (Keine Anwendung) oder blockiert (z.B. durch eine Firewall).
``` bash
paket = IP(dst="<IP Ziel>")/TCP(sport=<sport>, dport=<dport>, flags="S")
	# <sport> -> der Port an den geantwortet wird
	# <dport> -> Der Port der geprüft wird, kann auc eine Liste von Ports sein

# Paket senden
ans, unans = sr(paket)
```
Wenn man keine Verbindung aufbauen möchte sondern nur schauen möchte, ob eine Anwendung an dem Port läuft, sollte man keine  TCP-ACK-Antwort senden.

### SYN-Scan (Port Scan)
Zur Ermittlung von aktiven Ports bei einem Zielsystem.
Von Interesse sind dabei System-Ports (0 - 1023) und Benutzer-Ports (1024 - 49151)
``` bash
# Portliste vorbereiten
target_ports = [i for i in range(port_from, port_to)]

# Paket vorbereiten
paket = IP(dst="<IP Ziel>")/TCP(dport=target_ports, flags="S")

# Paket senden
ans, unans = sr(paket, timeout=1)

# nur erfolgreiche drucken
ans.nsummary(lfilter = lambda s,r: r.sprintf("%TCP.flags%") == "SA")
```

### SYN-Flooding (Denial-of-Service Angriff)


## IP-Spoofing
Da jedes Feld eines Pakets selbst gesetzt werden kann, lässt sich auch die Quell-Adresse im IP-Paket verändern. 
``` bash
IP(src="1.2.3.4", dst="192.168.10.1")
```
Ist jedoch nur sinnvoll wenn man keine Antwort zurück bekommen möchte.


