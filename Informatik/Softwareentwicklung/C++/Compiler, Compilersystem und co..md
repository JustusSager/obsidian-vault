# Compilersystem
Ein Compilersystem ist ein Gesamtpaket aus:
- Präprozessor -> ersetzt unter anderem "#include <>"
- Compiler -> einzelne Dateien werden in Maschinencode übersetzt
- Linker -> verbindet alle übersetzten Dateien zu einer ausführbaren Datei
	- Beim statischen einbinden von externen Bibliotheken wird eine "Kopie" der Bibliothek mit in die executable reingelinkt.
	- Beim dynamischen einbinden von externen Bibliotheken wird nur auf diese verwiesen.

Es gibt verschiedene Compilersysteme, aber das GNU Compilersystem wird empfohlen.
	https://msys2.org
	Bei CLion ist dieser standardmäßig dabei. Da muss nichts weiter konfiguriert werden.
	Je nach Hersteller der CPU werden manchmal vom Hersteller auch eigene Compiler angeboten, welche potenziell besser optimiert sind.

# Build System
Ein Build System ersetzt das kompilieren über die Konsole. Dabei gibt es auch jede Menge verschiedene wie z.B. ninja.

## CMake
ist ein Build System für Build System-Dateien. 
In CLion ist CMake Standardmäßig drin und kann unten links dazu aufgefordert werden die entsprechenden Build System-Dateien zu generieren.

CMakeLists.txt beschreibt Projektkompilierung
``` txt
cmake_minimum_required(VERSION 3.21) # benötigte Version von CMake
projekt(pic_videos) # Projektname

set(CMAKE_CXX_STANDARD 11) # verwendeter C++ Standard

add_executable(pic_videos main.cpp) # Einstiegspunt für die kompilireung und alle damit verbundenen Dateien
```
Bei erstellen oder löschen von Dateien muss CMake die Kompilierregeln einmal neu generieren.
Dabei wird der "cmake-build-debug" Ordner generiert/aktualisiert. Dort landet nach dem kompilieren auch die excecutable.


# Compileroptimierung
Der Compiler ist fleißig dabei den geschriebenen Code zu optimieren. Häufig sind dabei die Optimierungen das Compilers besser, als die Optimierung, die dem Entwickler einfallen würden.
## Copy Elision
- Elision engl. = Auslassung
- Compiler vermeidet ...
Siehe Folie 151 ff.

Beispiel:
``` C++
#include <vector>
std::vector<int> createData(unsigned int size) {
	std::vector<int> result{}; // 
	for (int idx=0; idx < size; ++idx) {
		result.push_back(idx);
	}
	return result;
}
```
Nach dem scope dieser Funktion existiert "result" zwar, ist aber niemandem zugeordnet. Hier ist Spielraum für den Compiler zu optimieren. 
