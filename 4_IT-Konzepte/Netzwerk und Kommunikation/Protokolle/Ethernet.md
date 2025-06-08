Das Ethernet-Protokoll wird für kabelgebundene Verbindungen im Internet auf der [[OSI und TCP-IP Referenzmodell#^875e7a|Netzzugangsschicht]] genutzt.
Das Ethernet-Protokoll lässt sich entsprechend des [[OSI und TCP-IP Referenzmodell#^42221f|OSI-Refernzmodells]] in den Teil der Bitübertragungsschicht und in den Teil der Sicherungsschicht aufteilen

# Struktur auf der Bitübertragungsschicht

|           | Bytes   |
| --------- | ------- |
| Präambel  | 7       |
| SFD       | 1       |
| Nutzdaten | 64-1522 |
| IPG       | 12      |
## Beschreibung
### Präambel und SFD
wird genutzt um Sender und Empfänger zu synchronisieren, also einen einheitlichen Takt herzustellen. Es gibt keine separate Taktleitung, wodurch diese im Protokoll abgebildet werden muss.
Dabei wird, für 7 Bytes, immer im Wechsel ein "High" und ein "Low"-Bit gesendet. Anschließend folgt der SFD (Start Frame Delimiter) welcher das Wechselspiel fortsetzt aber mit zwei "High"-Bits endet.
![[ethernet_präambel_sfd.png]]
### Nutzdaten
Die Protokolle der höheren Schichten werden hier eingebettet.
### IPG
12 Bytes Pause.

# Struktur auf der Sicherungsschicht

|           | Bytes   |
| --------- | ------- |
| Ziel      | 6       |
| Sender    | 6       |
| Ethertype | 2       |
| Nutzdaten | 46-1500 |
| FCS       | 4       |
## Beschreibung
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
