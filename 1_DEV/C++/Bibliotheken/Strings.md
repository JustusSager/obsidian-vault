# std::string
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
