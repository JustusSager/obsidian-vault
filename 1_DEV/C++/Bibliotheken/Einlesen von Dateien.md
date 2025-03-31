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
