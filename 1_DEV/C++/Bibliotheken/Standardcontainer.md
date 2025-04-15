- https://en.cppreference.com/w/cpp/container

# Sequentielle Container

## std::array
- https://cplusplus.com/reference/array/array/ 
- Lineares Array Aggregat
- statische Speicherverwaltung, d.h. die Größe eines Array kann während der Laufzeit nicht geändert werden.
- In <> wird der Datentyp der enthaltenen Elemente und die Länge angegeben. Siehe dazu #TODO Templates.

### Verwendung
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

### Im Vergleich zum C-Array
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

## std::vector ^3232b4
- https://cplusplus.com/reference/vector/vector/
- Lineare Datenstruktur 
- dynamischer Speicherverwaltung, d.h. hierbei wird der Speicher automatisch verwaltet, es ist keine manuelle Allokation nötig. 
- In "<>" wird der Datentyp der enthaltenen Elemente angegeben. Siehe dazu #TODO Templates

### Verwendung
``` C++
#include<vector>
int main() {
	// vector aus ints erstellen
	std::vector<int> v1 {1, 2, 3};
	// Anzahl der Elemente ausgeben
	v1.size();
	// Echte Größe das vectors
	v1.capacity();
	// Ein Element wird "in place" hinten hinzugefügt, es wird keine Kopie erzeugt. Wichtig für unique_ptr.
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

## std::deque
- Double Ended Queue
- schnelles Einfügen / Lesen / Löschen an beiden Enden der Queue
- Kann fragmentiert auf dem Speicher liegen.

### Verwendung
``` C++
#include <iostream>
#include <deque>
int main(){
	std::deque<int> di {1, 2, 3, 4, 5};
	di.pop_back();
	for(auto const &v: di){
		std::cout << v << std::endl;
	}
	di.pop_front();
	for(auto const &v: di){
		std::cout << v << std::endl;
	}
}
```

## std::queue
- Queue. 
- Achtung, nicht threadsicher!

### Verwendung
``` C++
#include <iostream>
#include <queue>
struct QElement{
	QElement(std::string const &s) : word{s}{}
	std::string word;
};
int main(){
	std::queue<QElement> q;
	// produce
	q.emplace("Hallo");
	q.emplace("schoene");
	q.emplace("Welt!");
	// consume
	do{
		std::cout << q.front().word << std::endl;
		q.pop();
	} while(!q.empty());
}
```


## std::list
- Doppelt verkettete Liste
- einfügen, löschen, teilen meist ressourcenintensiver zum vector.
- kann Fragmentiert im Speicher liegen.

## std::forward_list
- Einfach verkettete Liste
- weniger Speicherbedürftig als list, aber hat auch weniger features.
- kann Fragmentiert im Speicher liegen.

# Assoziative Container

## std::map
- Assoziativer Container

## Verwendung
``` C++
#include <iostream>
#include <map>
int main(){
	std::map<std::string, std::string> mymap;
	mymap.emplace("one", "eins");
	mymap.emplace("two", "zwei");
	mymap["three"] = "drei";
	std::cout << mymap["one"] << std::endl;
	std::cout << mymap["two"] << std::endl;
	std::cout << mymap["three"] << std::endl;
	for(auto const &v: mymap){
		std::cout << v.first << " " << v.second << std::endl;
	}
}
```
