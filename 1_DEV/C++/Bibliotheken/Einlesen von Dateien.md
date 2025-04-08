# std::fstream
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

# Flags / Exception
Flags (Exceptions) können aktiviert werden mit:
``` C++
std::ifstream filestream(file_path);  
filestream.exceptions(std::ifstream::eofbit); // Bit für End-of-File
filestream.exceptions(std::ifstream::failbit); // Bit für Fail
filestream.exceptions(std::ifstream::badbit); // Bit für Bad

filestream.exceptions(std::ifstream::eofbit | std::ifstream::failbit | std::ifstream::badbit); # Inline
```

- End-of-File (EOF)
	- Wird gesetzt, wenn File zu Ende
- Fail
	- Wird immer gesetzt wenn lesen fehlgeschlagen.
	- auch bei EOF.
- Bad
	- Externer Fehler?

## Verwendung
``` C++
try {
    int counter{0};
    filestream.open(file_path);  
    while (!filestream.eof()) {  
        std::getline(filestream, line);
        // Verarbeitung von line
        counter++;  
    }  
    filestream.close();  
} catch (std::ifstream::failure const &e) {  
    if (filestream.eof()) { # Kontrolle ob Fail vom EOF kommt
        // std::cerr << "EOF Bit: " << filestream.eof() << std::endl;  
    } else {  // sonst exception ausgeben
        std::cerr << e.what() << std::endl;  
    }  
}
```
