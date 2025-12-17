# Iteratoren als Teil von Arrays und Vektoren
Eine Klasse welche, ähnlich zu Zeigern eines C-Array, ermöglicht auf eine Datenmenge zu zu greifen. [[Informatik/Softwareentwicklung/C++/Bibliotheken#Standardcontainer|Standardcontainer]] wie z.B. std::vector haben eingebaute Methoden die Zugriff ermöglichen. 
Es gibt verschiedene Iterator-Klassen, welche aufeinander aufbauen und unterschiedlich viel können. Siehe dazu: https://cplusplus.com/reference/iterator/


``` C++
#include <iostream>
#include <vector>
struct A{
	int instanceID;
	explicit A(int const id) : instanceID{id} {}
	void SayHi() const {
		std::cout << "Hi, I am instance " << instanceID << std::endl;
	}
};
int main(){
	std::vector<A> va;
	va.emplace_back(0);
	va.emplace_back(1);
	va.begin()->SayHi(); // erstes Element
	(va.begin()+1)->SayHi(); // zweites Element
	(va.end()-1)->SayHi(); // letztes Element
	// auto ist hier sehr angenehm, da Datentyp komplex
	for(auto it=va.begin();it<va.end();it++){
		(*it).SayHi();
	}
	auto cit {va.crbegin()}; // const reverse iterator
	std::cout << cit->instanceID << std::endl; // ok
	// cit->instanceID = 42; // Fehler, nur Lesezugriff erlaubt da const
}
```

# Input Iterator
- Unterstützt Vergleichsoperationen
- Dereferenzierung als [[Wertkategorien#^4dff75|rvalue]].
- Kann inkrementiert werden.

# Output Iterator
- Dereferenzierung als [[Wertkategorien#^ee367c|lvalue]].
- Kann inkrementiert werden.

# Forward Iterator

^bba8d7

- Aufbauend auf Input und Output Iterator

# Bidirectional Iterator

^0bd03d

- Aufbauend auf Forward Iterator
- Kann dekrementiert werden

# Random Access Iterator

^258c73

- Aufbauend auf Bidirectional Iterator
- unterstützt Rechenoperationen
- unterstützt Ungleichungen
- unterstützt "compound assignment operations (+= and -=)"
- unterstützt "offset dereference operator ([])"
