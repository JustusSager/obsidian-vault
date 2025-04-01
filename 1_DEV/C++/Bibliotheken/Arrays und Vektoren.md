# std::array
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

# std::vector ^3232b4
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
