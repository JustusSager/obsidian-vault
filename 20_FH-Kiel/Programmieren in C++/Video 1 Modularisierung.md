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


# 
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


