#Informatik 
Namensräume sollten nur innerhalb von .cpp Dateien bwz. nur innerhalb von fest definierten Blöcken verwendet werden, um den Namensraum auf einen abgesteckten Bereich zu begrenzen.
main.cpp
``` C++
int a {4}; // globaler Namensraum, darf im Projekt nur einmal vorkommen

namespace ctag { // namensraum definieren
	namespace util { // namensräume können verschachtelt werden
		void SwissArmyKnive() {
			std::cout << "Im a Swiss army knife" << std::endl;
		}
	}
}

int main() {
	{ // lokaler scope
		using namespace ctag::util // Namensraum im scope einbinden
		SwissArmyKnive();
		a = 5; // Zugriff auf den globalen Namensraum weiterhin so möglich
		::a = 6 // eindeutig auf den globalen Namensraum zugreifen
	}
	ctag::util::SwissArmyKnive(); // zugriff ohne using namespace mithilfe von fully qualified identifier 
	return 0;
}
```

## Anonymer Namensraum
ist ein Namensraum, der keinen identifier hat. Dadurch steht der Inhalt nur innerhalb von dem Modul zur Verfügung. Stichwort Kapselung -> internal linkage.
Eine alternative Form der Kapselung zu [[Schlüsselwörter in C++#s|static]].
Funktioniert auch für lokale [[#^5925c2|Typdefinition]].

modul1.hpp
``` C++
namespace test {
	void CallMe();
}
namespace {
	void f();
}
```
modul1.cpp
``` C++
#include "modul1.hpp"
void test::CallMe() {
	f();
}
namespace {
	int a {42};
	void f() {
		std::cerr << "a is" << a << std::endl;
	}
}
```
Die Identifier a und f() stehen nur innerhalb von modul1.cpp zur Verfügung. Dadurch können die identifier in anderen Modulen wiederverwendet werden. Der identifier CallMe() kann in anderen Modulen nicht wiederverwendet werden.
