## Compilersystem
Ein Compilersystem ist ein Gesamtpaket aus:
- Präprozessor -> ersetzt unter anderem "#include <>"
- Compiler -> einzelne Dateien werden in Maschinencode übersetzt
- Linker -> verbindet alle übersetzten Dateien zu einer ausführbaren Datei

Es gibt verschiedene Compilersysteme, aber das GNU Compilersystem wird empfohlen.
	https://msys2.org
	Bei CLion ist dieser standardmäßig dabei. Da muss nichts weiter konfiguriert werden.
	Je nach Hersteller der CPU werden manchmal vom Hersteller auch eigene Compiler angeboten, welche potenziell besser optimiert sind.

## Build System
Ein Build System ersetzt das kompilieren über die Konsole. Dabei gibt es auch jede Menge verschiedene wie z.B. ninja.

### CMake
ist ein Build System für Build System-Dateien. 
In CLion ist CMake Standardmäßig drin und kann unten links dazu aufgefordert werden die entsprechenden Build System-Dateien zu generieren.

