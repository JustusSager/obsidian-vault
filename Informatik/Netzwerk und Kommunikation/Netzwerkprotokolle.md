# Ethernet
Das Ethernet-Protokoll wird für kabel-gebundene Verbindungen im Internet auf der [[OSI und TCP-IP Referenzmodell#^875e7a|Netzzugangsschicht]] genutzt.
Das Ethernet-Protokoll lässt sich entsprechend des [[OSI und TCP-IP Referenzmodell#^42221f|OSI-Refernzmodells]] in den Teil der Bitübertragungsschicht und in den Teil der Sicherungsschicht aufteilen

## Struktur auf der Bitübertragungsschicht

|           | Bytes   |
| --------- | ------- |
| Präambel  | 7       |
| SFD       | 1       |
| Nutzdaten | 64-1522 |
| IPG       | 12      |
### Präambel und SFD
wird genutzt um Sender und Empfänger zu synchronisieren, also einen einheitlichen Takt herzustellen. Es gibt keine separate Taktleitung, wodurch diese im Protokoll abgebildet werden muss.
Dabei wird, für 7 Bytes, immer im Wechsel ein "High" und ein "Low"-Bit gesendet. Anschließend folgt der SFD (Start Frame Delimiter) welcher das Wechselspiel fortsetzt aber mit zwei "High"-Bits endet.
![[ethernet_präambel_sfd.png]]
### Nutzdaten
Die Protokolle der höheren Schichten werden hier eingebettet.
### IPG
12 Bytes Pause.

## Struktur auf der Sicherungsschicht

|           | Bytes   |
| --------- | ------- |
| Ziel      | 6       |
| Sender    | 6       |
| Ethertype | 2       |
| Nutzdaten | 46-1500 |
| FCS       | 4       |
### Ziel und Sender
[[MAC-Adressen]] des Ziels und des Absenders.
Werden als LSB-first und Big Endian übertragen.
### Ethertype
Beschreibt das Protokoll der Nutzdaten
**Mögliche Werte:**
- `0x86DD`: IPv6
- `0x0800`: IPv4
- `0x0842`: Wake on LAN
### Nutzdaten
Die Nutzdaten müssen mindestens 46 Bytes lang sein, Kürzere Nutzdaten werden am Ende mit Nullbytes aufgefüllt. Nutzdaten die länger als 1500 Bytes sind müssen in mehrere Pakete aufgeteilt werden.
### FCS (Frame Check Sequence)
Prüfsumme aller Daten des Protokolls, welche nach dem CRC-32.Verfahren gebildet wird. Der Empfänger kann dasselbe Verfahren anwenden und prüfen, ob die Prüfsummen übereinstimmen. Dadurch können Übertragungsfehler entdeckt werden.
# WiFi
#TODO WiFi
# IPv4
Teil der TCP-IP [[OSI und TCP-IP Referenzmodell#Schicht 2 – Internetschicht|Internetschicht]].
## Struktur

|                              | Bits | Beschreibung                                                                        |
| ---------------------------- | ---- | ----------------------------------------------------------------------------------- |
| Version                      | 4    | Version des IP-Protokolls. Hier typischerweise 0b0100 = 4                           |
| Internet Header Length (IHL) | 4    | Länge des IP-Headers als Vielfaches von 32 Bit.                                     |
| Type of Service (ToS)        | 8    |                                                                                     |
| Total Length                 | 16   | Enthält die Gesamtlänge des IP-Paketes.                                             |
| Identification               | 16   |                                                                                     |
| Flags                        | 3    |                                                                                     |
| Fragment-Offset              | 13   |                                                                                     |
| Time-to-Live (TTL)           | 8    | Verbleibende Lebensdauer des Pakets in Sekunden. Typischerweise zwischen 30 und 64. |
| Protocol                     | 8    | Art des enthaltenen Protokolls (z. B. TCP oder UDP).                                |
| Header Checksum              | 8    |                                                                                     |
| Source IP-Address            | 32   | IP-Adresse des Absenders                                                            |
| Destination IP-Address       | 32   | IP-Adresse des Empfängers                                                           |
| Options / Padding            | 32   |                                                                                     |
#TODO IPv4 vervollständigen
### Protocol
Mögliche Werte:
- 6 - `0x06` -> TCP
- 17 - `0x11` -> UDP
# IPv6
Teil der TCP-IP [[OSI und TCP-IP Referenzmodell#Schicht 2 – Internetschicht|Internetschicht]].
## Struktur

|                           | Bits | Beschreibung                                                                                             |
| ------------------------- | ---- | -------------------------------------------------------------------------------------------------------- |
| Version                   | 4    | Version des IP-Protokolls. Hier typischerweise 0b0110 = 6                                                |
| Traffic Class             | 8    | Der Wert des Feldes definiert die Priorität des Paketes.                                                 |
| Flow Label                | 20   |                                                                                                          |
| Payload Length            | 16   | Hier steht die im IP-Paket transportierten Daten in Byte.                                                |
| Next Header               | 8    | Hier ist das übergeordnete Transportprotokoll angegeben. Bei [[#IPv4]] hieß das Feld einfach Protokoll.  |
| Hop Limit                 | 8    | Dieses Feld enthält die Anzahl der verbleibenden weiterleitenden Stationen, bevor das IP-Paket verfällt. |
| Source Address            | 32   | IP-Adresse der Quelle                                                                                    |
| Destination Address       | 32   | IP-Adresse des Ziels                                                                                     |
| IPv6-Header-Erweiterungen |      | Im IPv6-Header können optional Informationen im separaten Header dem IP-Kopf angehängt werden.           |
#TODO IPv6 vervollständigen
# TCP
- Teil der [[OSI und TCP-IP Referenzmodell#^3189dd|Transportschicht]] des [[OSI und TCP-IP Referenzmodell#^68e9fc|TCP/IP-Referenzmodells]].

## Struktur
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
## Verbindungsaufbau
### Erfolgreicher Verbindungsaufbau
![[tcp_handshake.png]]
Initial wird vom Client und vom Server jeweils eine zufällige Sequenznummer $x$ und $y$ gewählt. 
### Fehlgeschlagener Verbindungsaufbau
![[tcp_rst.png]]
### Datenübertragung
![[tcp_lost_data.png]]
Bei der Sequenznummer `12921` wurden die Daten nicht ordnungsgemäß übertragen, weshalb in der Antwort des Servers die `ACK` noch bei `12921` statt bei `15841` liegt. Dadurch weiß der Client, dass die Daten `2921 - 4380` und `4381 - 5840` noch einmal erneut gesendet werden müssen.
### Verbindungsabbau
![[tcp_fin.png]]
# UDP
- Teil der [[OSI und TCP-IP Referenzmodell#^3189dd|Transportschicht]] des [[OSI und TCP-IP Referenzmodell#^68e9fc|TCP/IP-Referenzmodells]].
## Struktur

|                  | Bits | Beschreibung                                       |
| ---------------- | ---- | -------------------------------------------------- |
| Source Port      | 16   | Quell-Port der Anwendung, die das Paket verschickt |
| Destination Port | 16   | Ziel Port des Pakets                               |
| Länge            | 16   | Länge des gesamten UDP-Pakets.                     |
| Checksum         | 16   | Checksum                                           |
#TODO UDP vervollständigen
