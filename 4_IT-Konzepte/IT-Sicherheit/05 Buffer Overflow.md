Ein Buffer Overflow (oder Pufferüberlauf) ist, wenn eine Variable ihren eigentlich angedachten Speicherbereich überschreitet. Die kann zum Beispiel passieren, wenn ein Speicherbereich für einen String der Länge 10 reserviert wurde, jedoch ein String der Länge 20, ohne Überprüfung in den Speicherbereich geladen wird.  

Puffer = Speicherbereich
Pufferüberlauf: Die Menge der in den Puffer zu schreibenden Daten ist größer als der Speicherbereich -> Überlauf

### Normale Abarbeitung eines Programms
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

### Buffer Overflow herbeiführen
Im oben aufgeführten Programmablauf lässt sich ein Buffer Overflow missbrauchen, indem man bei der Ausführung des Unterprogramms einen Buffer Overflow nutzt um (z.B. durch Nutzereingabe eines Strings) den Speicher bis zum `Stack Basepointer` mit dem eigenen Code zu überschreiben. Der `Stack Basepointer` soll dabei auf die Speicheradresse des eingeschleusten Code zeigen. 
Sobald zu der in der Rücksprungadresse gespeicherten Adresse gesprungen wird, wird der eingeschleuste Code ausgeführt.

Herausforderung aus Angreifer-Sicht:
1. Er weiß nicht an welcher Stelle im Speicher sich die absolute Rücksprungadresse befindet.
   -> Rücksprungadresse mehrfach oberhalb Exploit-Code
2. Er kennt die absoluten Speicheradressen des Programms nicht.
   -> "Landezone" unterhalb des Exploit Code (NOP: no operation)
3. Zeichenkette darf keine `Null`-Bytes enthalten.
   -> Verwendung einer geeigneten Codierung

#### Code Beispiel
``` C
int main() {

}
```

### Schutzmaßnahmen gegen Pufferüberläufe: 
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
