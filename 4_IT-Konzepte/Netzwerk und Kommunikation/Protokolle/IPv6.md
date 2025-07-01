# Struktur

|                           | Bits | Beschreibung                                                                                             |
| ------------------------- | ---- | -------------------------------------------------------------------------------------------------------- |
| Version                   | 4    | Version des IP-Protokolls. Hier typischerweise 0b0110 = 6                                                |
| Traffic Class             | 8    | Der Wert des Feldes definiert die Priorität des Paketes.                                                 |
| Flow Label                | 20   |                                                                                                          |
| Payload Length            | 16   | Hier steht die im IP-Paket transportierten Daten in Byte.                                                |
| Next Header               | 8    | Hier ist das übergeordnete Transportprotokoll angegeben. Bei [[IPv4]] hieß das Feld einfach Protokoll.   |
| Hop Limit                 | 8    | Dieses Feld enthält die Anzahl der verbleibenden weiterleitenden Stationen, bevor das IP-Paket verfällt. |
| Source Address            | 32   | IP-Adresse der Quelle                                                                                    |
| Destination Address       | 32   | IP-Adresse des Ziels                                                                                     |
| IPv6-Header-Erweiterungen |      | Im IPv6-Header können optional Informationen im separaten Header dem IP-Kopf angehängt werden.           |
#TODO IPv6 vervollständigen