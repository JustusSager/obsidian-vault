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
Im oben aufgeführten Programmablauf lässt sich ein Buffer Overflow missbrauchen, indem man bei der Ausführung des Unterprogramms einen Buffer Overflow nutzt um (z.B. durch Nutzereingabe eines Strings) den Speicher bis zum `Stack Basepointer` mit dem eigenen Code zu überschreiben. Der `Stack Basepointer` soll dabei auf die Speicheradresse des eingeschleusten Code zeigen. 
Sobald zu der in der Rücksprungadresse gespeicherten Adresse gesprungen wird, wird der eingeschleuste Code ausgeführt.

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
Die Funktion `versteckt` wird innerhalb von dem Skript nie aufgerufen. Dennoch lässt sich das Programm über ein Kommandozeilenparameter so manipulieren, dass die Funktion `versteckt` aufgerufen wird. 
Für die Variable `buffer` wurden 128 Bytes an Speicher allokiert. Im Anschluss an den für die Variable `buffer` reservierten Speicher liegt der `Stack Basepointer`. Da in `funk2` mit dem Methodenaufruf `strcpy` keine Kontrolle stattfindet, ob das Ziel des Kopiervorgangs auch groß genug ist für das übergebene char-Array, lässt sich ein `buffer overflow` herbeiführen und der `Stack Basepointer` manipulieren.
In diesem Fall wird ein char-Array mit einer Länge von 136 Bytes benötigt um den `Stack Basepointer` zu überschreiben. Dabei stellen die letzten 4 Byte den `Stack Basepointer` dar. Wenn also die letzten 4 Byte des char-Arrays der physischen Adresse der `versteckt`-Funktion entsprechen, wird Diese ausgeführt.

#### Öffnen einer Shell
``` C
int main() {

}
```

Die dabei geöffnete Shell besitzt die gleichen Rechte, wie das ausgeführte Programm. Der nächste Schritt wäre nun eine `privilege escalation` zu erreichen um an `root`-Rechte zu kommen.

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
