Ist eine Ansammlung der wichtigsten Unterprogramme und Datentypen, standardisiert durch die ISO.
gebündelt im Namensraum "std".
# iostream
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

# iomanip ^0997aa
Konsolenausgabe formatieren. Aber die alte Variante, ab C++ 20 kann man [[#^c1a51d|format]] nutzen.

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

# format ^c1a51d
Ab C++ 20 kann man std::format benutzen um Ausgaben zu formatieren. Bei älteren Versionen kann man [[#^0997aa|iomanip]] verwenden.
Nicht jeder Compiler kennt "std::format", je nach Compiler muss auch bei C++ 20 und neuer [[#^0997aa|iomanip]] verwendet werden.

## Verwewndung
``` C++
#include <format>
int main() {
	double x {22.123456};
	std::cout << std::format("{:.2f}\n", x);
	return 0;
}
```

# fstream
Lesen und schreiben einer Datei.
"ifstream" -> Lesen aus einer Datei.
"ofstream" -> schreiben in eine Datei.
"fstream" -> Lesen und Schreiben aus/in eine Datei.

## Verwendung
``` C++
#include <iostream>
#include <fstream>
int main() {
	{ // Automatisches öffnen und schließen mit Scope
		std::ofstream raus {"data.txt"}; 
		raus << "42\n"; // schreibt in die Datei
	}
	{
		std::ifstream rein {"data.txt"};
		int i;
		rein >> i; // ließt aus der Datei
		cout << i;
	}
	// Zugriff lesend und schreibend als Binärdatei.
	std::fstream wf {"data.txt", ios::in | ios::out | ios::binary}
	char c;
	wf.read(&c, 1); // lesen
	std::cout << std::hex << static_cast<int>(c) << std::endl;
	
	c = 'b';
	wf.write(&c, 1); // c in wf schreiben (append)
	wf.close(); // Explizit schließen
	return 0;
}

```

# string
https://cplusplus.com/reference/string/string/
Nicht Verwechseln mit "cstring" aus der C-Programmiersprache.
Ist eine spezielle Implementierung von "std::basic_string". Hier lässt sich nicht auf ein anderes Codierungsformat der Buchstaben wechseln.

## Verwendung
``` C++
#include<iostream>
#include<string>
int main() {
	// Strings erzeugen
	std::string str1 {"Hallo"};
	std::string str2 {"Welt!"};
	
	// Strings aneinanderhängen
	std::string str3 = str1 + " " + str2;
	
	// Ausgabe
	std::cout << str3 << std::endl;
	
	// Erste Instanz einer Zeichenfolge finden.
	// size_type ist quasi ein int aber ermöglicht bessere Platformübergreifende kompatibilität
	std::string:size_type pos = str3.find(" ");
	
	// Substring erzeugen
	str1 = str3.substr(pos + 1);
	
	// Elementzugriff über Index
	std::cout << str1[0] << std::endl;
	return 0;
}
```

## Vergleich mit C-Strings
C-Strings sind einfach nur char-Arrays, auf die über Pointer zugegriffen wird. Es gibt hierbei keine dynamische Länge und die Verarbeitung ist unhandlich.
Die C++-Strings sind eine eigene Klasse mit eigenen Methoden die das manipulieren der strings erleichtern. Es gibt eine dynamische Speicherverwaltung, die es erlaubt, dass die Länge des Strings nicht zur Compile-Zeit bereits bekannt sein muss.

# array
https://cplusplus.com/reference/array/array/
Lineares Array Aggregat mit statischer Speicherverwaltung. D.h. die Größe eines Arrays kann während der Laufzeit nicht mehr geändert werden.
In "<>" wird der Datentyp der enthaltenen Elemente und die Länge angegeben. Siehe dazu #TODO Templates

## Verwendung
``` C++
#include<array>
int main(){
	// Array erstellen
	std::array<int, 5> sa {0, 1, 2, 3, 4};
	std::array<int, 5> sb {sa}; // value copy
	
	// Elementzugriff
	sa[2] = 55;
	return 0;
}
```

## Im Vergleich zum C-Array
``` C++
#include<array>
int main(){
	// C-Array, statisch, d.h. Groesse bekannt zur Compilezeit!
	int ca[5] {0, 1, 2, 3, 4};
	// int cb[5] {ca}; -> geht nicht!
	
	// std::array, statisch, d.h. Groesse muss zur Compilezeit bekannt sein!
	std::array<int, 5> sa {0, 1, 2, 3, 4};
	std::array<int, 5> sb {sa}; // value copy
	// Elementzugriff
	sa[2] = 55;
	return 0;
}
```

# vector
https://cplusplus.com/reference/vector/vector/
Lineare Datenstruktur mit dynamischer Speicherverwaltung.  Hierbei wird der Speicher automatisch verwaltet, es ist keine manuelle Allokation nötig. 
In "<>" wird der Datentyp der enthaltenen Elemente angegeben. Siehe dazu #TODO Templates

## Verwendung
``` C++
#include<vector>
int main() {
	// vector aus ints erstellen
	std::vector<int> v1 {1, 2, 3};
	// Anzahl der Elemente ausgeben
	v1.size();
	// Echte Größe das vectors
	v1.capacity();
	// Ein Element wird "in place" hinten hinzugefügt
	v1.emplace_back(4);
	// Ein Element wird "by copy" hinten hinzugefügt
	v1.push_back(5);
	// Das letzte Element löschen
	v1.pop_back();
	// auf echte Größe reduzieren
	v1.shrink_to_fit();
	// Zugriff
	int x = v1[0];
	return 0;
}
```

# complex 
https://cplusplus.com/reference/complex/complex/
#TODO std::complex für irgendwann
Komplexe Zahlen
``` C++
#include<complex>
```

# exception

Hinweis: reduziert die Performance!

## Verwendung
``` C++
#include <exception>  
#include <iostream>  
#include <fstream>  
int main() {  
    std::ifstream file {};  
    try {  
       // Exceptions sind bei ifstream standardmäßig aus Performancegründen abgeschaltet, diese müssen erst aktiviert werden.  
       file.exceptions(std::ifstream::failbit | std::ifstream::badbit);  
       // Nicht existierende Datei einlesen führt zu Fehler.  
       file.open("testfile.txt");  
       file.close();  
    } catch (std::exception &e) {  
        std::cerr << e.what() << std::endl;  
    }  
    return 0;  
}
```

### Standard exceptions
``` C++
#include <exception> // exceptions
#include <stdexcept> // Exceptions aus der Standardbib.
#include <iostream>
int main(int argv, char** args) {
    try {  
	    std::cout << argv << std::endl;
	    if(argv != 3) throw std::invalid_argument("Wrong number of args!");
    } catch (std::exception &e) {  
        std::cerr << e.what() << std::endl;  
    }  
    return 0;  
}
```

## Vergleich mit C
``` C
#include <stdlib>
int main() {
	if(f() == -1) handle_error(); // Variante 1
	assert(true) // Variante 2
	return 0;
}

int f() {
	if(true) { // fehler entsteht
		exit(-1);
	}
	return 0;
}

```