#Informatik
``` C++
class Example{
	int sz, *ia;
public:
	// ctor
	Example(int const n) : sz{n}, ia{new int[n]} {
	}
	// dtor
	~Example(){
		delete [] ia;
	};
};
int main(){
	// Variante 1
	Example e{24}; 
	// Variante 2
	Example *pt {new Test};
		// Zeugs
	delete pt;
	return 0;
}
```
Bei der Variante 1 ist das Objekt "e" auf dem Stack. Dabei wird "e" automatisch allokiert (ctor) und zerstört (dtor).
Bei der Variante 2 wird das Objekt "händisch" allokiert (ctor) und zerstört (dtor). Das Objekt auf das der Zeiger "pt" zeigt liegt hierbei auf dem Heap.
# Stack- oder auch Stapelspeicher
Wird automatisch vom Compiler verwaltet. D.h. Objekte werden im Scope automatisch erzeugt und bereinigt. 
Die Stackgröße ist i.d.R. begrenzt.
First-In Last-out Stapelstruktur, interne Adressierung über Stapelzeiger (engl. stack pointer)

``` C++
void f(int p) {
	// Argument p existiert als Kopie auf dem Stack -> by-value
	// weiter Stack Variablen wären:
	int a[] {1, 2, 3};
	double b {2.2};
}
```

# Heapspeicher
Frei allokierbarer Speicherpool
Manuelle Verwaltung (new / delete)
	in der Regel benutzerspezifische ctor/dtor nötig. Siehe dazu[[Klassen#Konstruktor|Konstruktor]].
Rohe Zeiger -> sollte man im modernen C++ soweit möglich vermeiden.
Objektlebenszeit über den Scope hinweg.

Speicher der hier allokiert wird muss auch wieder freigegeben werden.
	Das Betriebssystem gibt jedoch Speicher nach Programmende auch wieder frei.
## Dynamische Heapspeicherverwaltung im C-Stil
``` C++
#include <cstdlib>
#include <cassert>
#include <iostream>

int main() {
	int *ia {nullptr};
	// 1034 integers vom heap Speicher
	ia = (int*) malloc(1024*sizeof(int))
	if(nullptr != ia) {
		for (int i = 0; i < 1024; i++) {
			ia[i] = i;
		}
		for (int i = 0; i < 1024; i++) {
			std::cout << ia[i] << std::endl;
		}
		free(ia);
	} else {
		assert(ia);
	}
}
```

## Dynamische Heapspeicherverwaltung im C++ Stil
Siehe hierzu auch [[Informatik/Softwareentwicklung/C++/Bibliotheken#Standardcontainer|Standardcontainer]], das ist eine abstrakte Implementierung der Dynamischen Heapspeicherverwaltung.
``` C++
#include <iostream>
// #include <new> // meist sowieso da
int main() {
	try {
		int *ia {nullptr}, *val {nullptr};
		// Array
		ia = new int[1024];
		// Einzelwert
		val = new int; 
		*val = 22;
		// Logik
		for (int i {0}; i < 1024; i++) {
			ia[i] = i;
		}
		for (int i {0}; i < 1024; i++) {
			std::cout << i << std::endl;
		}
		// Freigeben
		delete [] ia;
		delete val;
	} catch (std::bad_alloc &e) {
		std::cerr << e.what() << std::endl;
	}
}
```
