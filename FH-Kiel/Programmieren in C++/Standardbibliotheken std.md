Ist eine Ansammlung der wichtigsten Unterprogramme und Datentypen, standardisiert durch die ISO.
gebündelt im Namensraum "std".
# iostream

## Verwendung
#TODO std::cerr
``` C++
#include<iostream>
int main() {
	// Konsolenausgabe
	std::cout << "Hello World!" << std::endl;
	
	// ebenfalls Konsolenausgabe, aber irgendwas ist anders.
	std::cerr << "Hello World!" << std::endl;
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
Lineare Datenstruktur mit dynamischer Speicherverwaltung.  Hierbei wird der Speicher automatisch verwaltet, es ist keine manuelle Allokation nötig. 
In "<>" wird der Datentyp der enthaltenen Elemente angegeben. Siehe dazu #TODO Templates
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
Komplexe Zahlen
``` C++
#include<complex>
```