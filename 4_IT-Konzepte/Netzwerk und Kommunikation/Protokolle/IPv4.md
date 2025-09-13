# Struktur

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

## Detailbeschreibung
### Protocol
Mögliche Werte:
- 6 - `0x06` -> TCP
- 17 - `0x11` -> UDP
