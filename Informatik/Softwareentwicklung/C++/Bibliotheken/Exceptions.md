# std::exception ^29a8b2
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

# std::stdexcept
Erweitert das Basismodul [[#^29a8b2|Exception]] um verschiedene häufig vorkommende Exception Module.

## Verwendung
``` C++
#include <exception> // exceptions
#include <stdexcept> // Exceptions aus der Standardbib.
#include <iostream>
int main(int argv, char** args) {
    try {  
	    std::cout << argv << std::endl;
	    // Mit "throw" lässt sich eine bestimmte Exception auslösen
	    if(argv != 3) throw std::invalid_argument("Wrong number of args!");
    } catch (std::exception &e) {  
        std::cerr << e.what() << std::endl;
        // "throw" im catch Blöck würde dazu führen, dass die Exception an den nächst höheren Block "weitergegeben" wird.
    }  
    return 0;  
}
```

# Eigene Exceptions schreiben
Aufbauend auf dem Modul [[#^29a8b2|Exception]] kann man eigene Exception Module schreiben.
#TODO

