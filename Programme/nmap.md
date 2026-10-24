---
erstellt am: 22.05.2026 08:58
tags:
  - Informatik
  - IT-Sicherheit
Deckblatt:
---
Open Source Werkzeug für Netzwerk-Scans und Sicherheitsüberprüfung.

# Port Scan:
``` bash
sudo nmap -sS -p <Ports> <IP-Ziel>
	-p <Ports> # Ports die überprüft werden sollen. 
		Kommagetrennte Liste (80,433,...) oder
		Bereiche (0-1023)
	-sT # TCP-Connect-Scan: Three-Way-Handshake 
	-sS # SYN-Scan (TCP)
	-sV # finde die Software (+ Version) an dem Port heraus
	-O # versucht Betriebssystem herauszufinden
	-v # verbose
	-vv # very verbose
```

# IP Scan (Ping-Sweep)
``` bash
sudo nmap -sn
```