Modularisierung ist sinnvolle Aufteilung eines Programms in Teile
Jedes Modul besteht aus eine .cpp und einer .hpp Datei
	Ausnahme dazu ist z.B. Templateprogrammierung und Headerbasierte Bibliotheken
Ein Programm sollte in Schichten modularisiert sein. Dabei dürfen Module nur auf andere Module zugreifen, die in einer niedriger liegenden Schicht liegt.
Zyklische Abhängigkeiten müssen ausgeschlossen sein.

Eine test1.cpp Datei:
``` C++
#include <iostream>
#include "test1.hpp" // hier wird der entsprechende Header eingebunden

void hello() {
	std::cout << "Hello World!" << std::endl;
}
```
und die dazugehörige test.hpp:
``` C++
// Hier sind include-Guards um die mehrfacheinbindung zu unterbinden.
#ifndef FH_PROJEKT_TEST1_HPP 
#define FH_PROJEKT_TEST1_HPP

void hello(); // hier wird die Funktion hello() bekannt gemacht

#endif
```

In einem anderen Modul lässt sich dieses Modul einbinden indem man das Modul mit 
``` C++
#include "test.hpp"

hello();
```
einbindet. Daraufhin lässt sich die Funktion aufrufen.


# CMake
CMakeLists.txt beschreibt Projektkompilierung
``` txt
cmake_minimum_required(VERSION 3.21) # benötigte Version von CMake
projekt(pic_videos) # Projektname

set(CMAKE_CXX_STANDARD 11) # verwendeter C++ Standard

add_executable(pic_videos main.cpp) # Einstiegspunt für die kompilireung und alle damit verbundenen Dateien
```
Bei erstellen oder löschen von Dateien muss CMake die Kompilierregeln einmal neu generieren.
Dabei wird der "cmake-build-debug" Ordner generiert/aktualisiert. Dort landet nach dem kompilieren auch die excecutable.

# Konstanten
konstanten können auf verschiedene Weise definiert werden
``` C++
#define CONST_N 42

int const 
```
und können natürlich auf in eigene Module ausgelagert werden. Hierfür benötigt man dann keine .cpp. Das würde man direkt in der .hpp machen.

# Globale Variablen (Keyword "extern")
sollten nicht zu sehr genutzt werden.
Eine Möglichkeit der Strukturierung ist alle in einem Modul zu sammeln. Damit ist eindeutig wo sie sind und welche existieren.

Globale Variablen erlauben Zugriff auf anderswo definierte Bezeichner.

globals.hpp
``` C++
#ifndef FH_PROJEKT_GLOBALS_HPP 
#define FH_PROJEKT_GLOBALS_HPP

extern int global_a; // Deklaration

#endif
```
globals.cpp
``` C++
#include "globals.hpp"

int global_a {42}; // Definition und Initialisierung
```

Das Keyword "extern" sorgt dafür, dass in der Header Datei die Variable "global_a" nur deklariert wird, jedoch nicht definiert. Das wird benötigt da ansonsten der include zu einer Mehrfachdefinition von global_a führt.

# Keyword "static"
Das Keyword static sorgt dafür, dass ein Name (also ein Bezeichner für Variablen und Funktionen) nur innerhalb des Moduls zur Verfügung steht. Dadurch lassen sich Namen über die Module hinweg mehrfach verwenden

Beispiel:
modul1.hpp
``` C++
void CallMe();
static void f(); // eig. werden nicht-öffentliche Funktionen hier gar nicht angegeben. Vorwärtsdeklaration würde man eher in modul1.cpp machen.
```
modul1.cpp
``` C++
// static void f(); // Vorwärtsdeklaration
static int a {5};
void CallMe() {
	f();
}
static void f() {
	std::cerr << "Static" << std:: endl;
}
```
main.cpp
``` C++
#include "modul1.hpp"
int main() {
	CallMe(); // ok
	f(); // Linkfehler, da static 
}
```
modul2.cpp
``` C++
static int a {5}; // ok da static
void CallMe() { // Linkfehler, da dublicate Symbol. CallMe() gibts schon in modul1
	int x {5};
}
```

# Namensräume
main.cpp
``` C++
int a {4}; // globaler Namensraum, darf im Projekt nur einmal vorkommen

namespace ctag { // namensraum definieren
	namespace util { // namensräume können verschachtelt werden
		void SwissArmyKnive() {
			std::cout << "Im a Swiss army knife" << std::endl;
		}
	}
}

int main() {
	{ // lokaler scope
		using namespace ctag::util // Namensraum im scope einbinden
		SwissArmyKnive();
		a = 5; // Zugriff auf den globalen Namensraum weiterhin so möglich
		::a = 6 // eindeutig auf den globalen Namensraum zugreifen
	}
	ctag::util::SwissArmyKnive(); // zugriff ohne using namespace mithilfe von fully qualified identifier 
	return 0;
}
```