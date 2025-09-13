# Physischer Zugriff
## Angriffsvektoren
#### Boot- und Live-Media-Angriffe
-**Externe Boot-Medien** - Angreifer kann System von USB-Stick booten, um lokale Festplatte zu mounten, sofern diese nicht ausreichend geschützt ist.
- **Manipulation des Bootloaders** - Durch Änderung an Bootloader oder BIOS/UEFI-Setup können Sicherheitsmechanismen umgangen werden.
#### Auslesen von Daten im Arbeitsspeicher
- **Cold Boot Attack** - Beim Herunterfahren können sensible Daten, z.B. Schlüssel, im RAM verbleiben – Angreifer kann diese extrahieren.
- **Direct Memory Access (DMA) Angriffe** - Angreifer kann über Schnittstellen wie Thunderbolt, FireWire oder PCIe direkten Zugriff auf Arbeitsspeicher erhalten, um vertrauliche Informationen auszulesen.
#### Manipulation und Implantation von Hardware
- **Hardware-Backdoors** - Physische Implantate oder modifizierte Hardwarekomponenten können dauerhaft Zugriffsmöglichkeiten ermöglichen.
- **Keylogger und Überwachungsgeräte** - Einsatz von Hardware-Keyloggern oder anderen Überwachungsgeräten erlaubt Erfassung von Tastatureingaben und anderen Aktivitäten.
#### Manipulation von Firmware und Software
- **Firmware-Angriffe** - Modifizierter BIOS/UEFI-Code oder infizierte Firmware auf Peripheriegeräten kann tiefgreifende Kontrolle über das System ermöglichen.
- **Angriffe auf Debug-Schnittstellen** - Physische Zugangsmöglichkeiten zu Schnittstellen (z. B. JTAG, serielle Debug-Ports) können Ausführung von Code oder Manipulation des Systems erlauben.
#### Direkter Diebstahl oder Austausch von Komponenten
- **Datendiebstahl** - Über physischen Diebstahl von Speichermedien oder anderen Komponenten kann Angreifer sensible Informationen erhalten und offline analysieren.
- **Manipulation von Hardwarekomponenten** - Austausch oder Ergänzung von Komponenten, um z.B. Daten abzufangen oder zu modifizieren.
#### Absichtliche Zerstörung von Hardware
- **Physische Zerstörung** - Angreifer beschädigt oder zerstört direkt Komponenten (z.B. Festplatten, Netzteile, Motherboards).
- **Überhitzung oder Kurzschlüsse** - Manipulationen an Stromversorgung oder Kühlung können zu Überhitzung oder elektrischen Fehlfunktionen bis hin zum Ausfall des Systems führen.
#### Sabotage durch Manipulation von Software/Hardware-Interaktionen
- **Manipulation der Firmware** - Gezielte Eingriffe in Firmware-Updates oder Überschreiben von Firmware kann zu dauerhafter Beeinträchtigung der Funktionsfähigkeit eines Systems führen.
- **Fehlkonfigurationen** - Absichtliche Veränderung kritischer Optionen der Systemkonfiguration (z.B. Überhitzungsschutz).

## Mögliche Absichten des Angreifers
- Datenexfiltration
- Einrichtung von persistenter Kontrolle
- Manipulation und Sabotage
- Erzielung von Wettbewerbsvorteilen oder Spionage
- ...
