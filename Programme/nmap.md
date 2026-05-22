#Informatik #IT-Sicherheit 
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
