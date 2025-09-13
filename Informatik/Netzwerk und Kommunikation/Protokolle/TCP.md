- Teil der [[OSI und TCP-IP Referenzmodell#^3189dd|Transportschicht]] des [[OSI und TCP-IP Referenzmodell#^68e9fc|TCP/IP-Referenzmodells]].

# Struktur
|                              | Bits    |
| ---------------------------- | ------- |
| Source Port                  | 16      |
| Destination Port             | 16      |
| Sequence Number (SEQ)        | 32      |
| Acknowledgement Number (ACK) | 32      |
| Data Offset                  | 4       |
| Reserved                     | 4       |
| Flags (FLGS)                 | 8       |
| (Receive) Window             | 16      |
| Checksum                     | 16      |
| Urgent Pointer               | 16      |
| Options ...                  | 0 - 320 |
## Beschreibung
### Source Port
- 16 Bit
### Destination Port
- 16 Bit
### Sequence Number
- Dient der Sortierung der TCP-Segmente. 
- Wird initialisiert wenn die SYN-Flag gesetzt ist
### Acknowledgement Number
- 32 Bit
- Gibt die Sequenznummer an, die der Absender dieses TCP-Segments als Nächstes erwartet
### Data Offset
- 4 Bit
- Länge der TCP-Headers in 32-Bit-Blöcken (ohne Nutzdaten)
### Reserved
- 4 Bit
- Reserviert, müssen alle 0 sein
### Control-Flags
- 8 Bit
	1. CWR (Congestion Window Reduced)
	   Senderate reduziert
	2. ECE 
	   Netzwerküberlastung mitteilen
	3. URG (Urgent)
	   Anwendung bearbeitet Daten nach dem Header sofort, unterbricht bisherige Verarbeitung des aktuellen TCP-Segments
	4. ACK (Acknowledgement)
	   Empfang von TCP-Segmenten beim Datentransfer bestätigen
	5. PSH (Push)
	6. RST (Reset)
	   Verbindung abbrechen
	7. SYN
	   Synchronisation von Sequenznummern
	8. FIN (Finish)
	   Schlussflag
### (Receive) Window
- 16 Bit
### Checksum
- 16 Bit
- Prüfsumme, Erkennung von Übertragungsfehlern
- besteht aus der Ziel-IP, der Quell-IP, der TCP-Protokollkennung (0x0006) und der Länge des TCP-Headers inkl. Nutzdaten (in Bytes)
### Urgent Pointer
- 16 Bit
### Options
- 0 - 40 Bytes

# Verbindungsaufbau

## Erfolgreicher Verbindungsaufbau
![[Pasted image 20250521192323.png]]
Initial wird vom Client und vom Server jeweils eine zufällige Sequenznummer $x$ und $y$ gewählt. 

## Fehlgeschlagener Verbindungsaufbau
![[Pasted image 20250521192417.png]]

## Datenübertragung
![[Pasted image 20250521192630.png]]
Bei der Sequenznummer `12921` wurden die Daten nicht ordnungsgemäß übertragen, weshalb in der Antwort des Servers die `ACK` noch bei `12921` statt bei `15841` liegt. Dadurch weiß der Client, dass die Daten `2921 - 4380` und `4381 - 5840` noch einmal erneut gesendet werden müssen.

## Verbindungsabbau
![[Pasted image 20250521193058.png]]
