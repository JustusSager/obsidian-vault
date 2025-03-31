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

# Keyword "static" ^940195
Das Keyword static sorgt dafür, dass ein Name (also ein Bezeichner für Variablen und Funktionen) nur innerhalb des Moduls zur Verfügung steht. Dadurch lassen sich Namen über die Module hinweg mehrfach verwenden.

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

## static in Klassen
#TODO Static in Klassen kann vewendet werden, um "Dinge" einer Klasse ohne Objektinstanziierung zu nutzen.  
# Namensräume
Namensräume sollten nur innerhalb von .cpp Dateien bwz. nur innerhalb von fest definierten Blöcken verwendet werden, um den Namensraum auf einen abgesteckten Bereich zu begrenzen.
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

## Anonymer Namensraum
ist ein Namensraum, der keinen identifier hat. Dadurch steht der Inhalt nur innerhalb von dem Modul zur Verfügung. Stichwort Kapselung -> internal linkage.
Eine alternative Form der Kapselung zu [[#^940195|static]].
Funktioniert auch für lokale [[#^5925c2|Typdefinition]].

modul1.hpp
``` C++
namespace test {
	void CallMe();
}
namespace {
	void f();
}
```
modul1.cpp
``` C++
#include "modul1.hpp"
void test::CallMe() {
	f();
}
namespace {
	int a {42};
	void f() {
		std::cerr << "a is" << a << std::endl;
	}
}
```
Die Identifier a und f() stehen nur innerhalb von modul1.cpp zur Verfügung. Dadurch können die identifier in anderen Modulen wiederverwendet werden. Der identifier CallMe() kann in anderen Modulen nicht wiederverwendet werden.

# Typdefinition ^5925c2
kann verwendet werden um einen "Platzhalter"-Typen zu definieren. Falls man den Typen später ändern möchte muss dann hierfür nur bei der Typdefinition, der Typ geändert werden.
``` C++
// Im C Stil
typedef double myfloat
myfloat x {42.f}

// Im C++ Stil
using myfloat2 = double;
myfloat2 y {33.f}
```

## struct als Aggregat, Benutzerdefinierter Typ
kann auch für "struct" verwendet werden:
``` C++
// C Stil
typedef struct mytype1 {
	int a, b, c;
	float x, y, z;
}
// C++ Stil
using mytype2 = struct {
	int a, b, c;
	float x, y, z;
}
// Uniform initalizer list
mytype1 m1 {1, 2, 3, 4.f, 5.f, 6.f};
mytype2 m2 {1, 2, 3, 4.f, 5.f, 6.f};
// Designated initalizer list
// Reihenfolge dennoch relevant! b=0,,x=.0f, y=.0f
mytype2 m3 {.a = 1, .c = 3, .z = 1.0f};

// Zugriff mit . Operator
int s1 = m1.a + m1.b / m1.c;
int s2 = m2.a + m2.b / m2.c;
```
