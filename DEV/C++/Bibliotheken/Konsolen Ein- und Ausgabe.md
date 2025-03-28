# std::iostream
https://cplusplus.com/reference/istream/iostream/
Verwendet Streams zur Zeichenübertragung. Ein Stream empfängt oder erzeugt "Zeichenstrom".

## Verwendung
### Konsolenausgabe
#TODO std::cerr
``` C++
#include<iostream>
int main() {
	// Konsolenausgabe
	std::cout << "Hello World!" << std::endl;
	// Mit "<<" wird der string "Hello World!" in das Streamobjekt std::cout hineingeschoben. 
	
	// ebenfalls Konsolenausgabe, aber irgendwas ist anders.
	std::cerr << "Hello World!" << std::endl;
	return 0;
}
```

"<<" erlaubt alle Standard Datentypen und "std::string", lässt sich jedoch auch als Operator in eigene Datentypen integrieren. Siehe dazu #TODO.
Analog dazu, lässt sich mit dem ">>" Operator das einlesen von Streams realisieren.

### Konsoleneingabe
Analog zum "<<" Operator lässt sich mit dem ">>" Operator das einlesen von Streams realisieren.
``` C++
#include <iostream>
#include <string>
using DataType = struct { 
	std::string name, plz_ort;
};
int main(){
	DataType person {"", ""};
	// Einlesen bis naechstes Whitespace
	std::cout << "Name: ";
	std::cin >> person.name;
	std::cout << "Plz und Ort: ";
	// Auslesen aller evtl. noch vorh. Whitespaces (also Eingabefeld bereinigen)
	std::cin >> std::ws;
	// Einlesen bis Newline
	std::getline(std::cin, person.plz_ort);
	// Ausgabe der Daten
	std::cout << "Name: " << person.name << std::endl;
	std::cout << "Plz und Ort: " << person.plz_ort << std::endl;
	return 0;
}
```

## Vergleich mit stdio von C
``` C
#include<stdio>
double x = 4.4373746483
printf("Hallo Welt!\n%.4f", x);
```

# std::iomanip ^0997aa
Konsolenausgabe formatieren. Aber die alte Variante, ab C++ 20 kann man häufig (je nach Compiler) [[#^c1a51d|format]] nutzen.

## Verwendung
``` C++
#include <iostream>
#include <iomanip>
using std::cout; // sorgt dafür, dass man cout, statt std::cout schreiben kann.
int main(){
	// Punktschreibweise nicht wissenschaftlich
	cout << std::fixed
	<< std::setprecision(15); // 15 Nachkommastellen
	cout << 0.5 << "\n"; // Ausgabe 0.500000000000000
	cout << std::setprecision(5); // 5 Nachkommastellen
	cout << 0.25 << "\n"; // Ausgabe 0.25000
	return 0;
}
```
"std::endl" erzeugt ein "\n" und 'flusht' den Ausgabepuffer (also setzt die Ausgabe zurück).
"std::flush" 'flusht' nur den Ausgabebuffer.

# std::format ^c1a51d
Ab C++ 20 kann man std::format benutzen um Ausgaben zu formatieren. Bei älteren Versionen kann man [[#^0997aa|iomanip]] verwenden.
Nicht jeder Compiler kennt "std::format", je nach Compiler muss auch bei C++ 20 und neuer [[#^0997aa|iomanip]] verwendet werden.

## Verwendung
``` C++
#include <format>
int main() {
	double x {22.123456};
	std::cout << std::format("{:.2f}\n", x);
	return 0;
}
```
