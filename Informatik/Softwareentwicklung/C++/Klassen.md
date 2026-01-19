#Informatik 
Klassen und Strukturen sind quasi das selbe in C++. Die Unterschiede sind weiter unten aufgelistet.

# Verwendung
## Innerhalb der Main
``` C++
struct MyClass2 {
	std::string name;
	void Print() {
		std::cout << name << std::endl;
	}
}

int main() {
	MyClass2 o {"test"};
	o.Print();
}
```

## In einem eigenen Modul
Jede Klasse kommt typischerweise jedoch in eine eigene Datei:
MyClass2.hpp
``` C++
struct MyClass2 {
	std::string name;
	void HelloWorld();
}
```
MyClass2.cpp
``` C++
#include "MyClass2.hpp"
// diese Funktion ist nur innerhalb der Datei gülig und gehört nich zur Klasse
static Get42() {
	return 42;
}
// Hier ist die Implementierung der Methode HelloWorld() der Klasse MyClass2
void MyClass2::HelloWorld() {
	std::cout << "Hello World!" << std::endl;
}
```

Früher wurde teilweise auch Methoden in der Header Datei implementiert.
MyClass3.hpp
``` C++
struct MyClass3 {
	std::string name;
	inline void SchnelleInlineFkt() {
		return 42 + 1;
	}
}
```

## Konstruktor
- Kurz ctor
- Konstruktorname = Klassenname
- Wenn ctor nicht explizit definiert wird, wird automatisch einer generiert, welcher keine Übergabeparameter hat (Default ctor). Sobald ein Konstruktor definiert wird, wird kein default ctor mehr erstellt.
- Ein Konstruktor darf keine Exceptions auslösen
- Konstruktoren werden nicht weitervererbt
- Siehe dazu auch [[OOP#Vererbung von Konstruktoren|Vererbung von Konstruktoren]].
``` C++
struct Example {
	int a;
	Example(int const &v) : a{v} {}
}

int main() {
	Example o; // funktioniert nicht mehr, da kein ctor ohne Übergabeparameter angelegt wird.
	return 0;
}
```

Default ctor soll generiert werden:
``` C++
struct Example {
	int a;
	Example(int const &v) : a{v} {}
	Example() = default; // Default ctor wird erstellt
}

int main() {
	Example o; // funktioniert wieder
	return 0;
}
```

Default ctor deaktivieren:
siehe hierzu [[#]]
``` C++
struct Example {
	int a;
	Example() = delete; // Es wird gar kein ctor generiert
}

int main() {
	Example o; // funktioniert nicht, da es keinen Konstruktor gibt.
	return 0;
}
```
### Initialisierung eines Attributs
``` C++
struct Example {
	int a {42}; // Variante 3
	void SaySomething() {
		std::cout << a << std::endl;
	}
	// Variante 1
	Example() {
		a = 42;
	}
	// Variante 2
	Example() : a{42} {} // Inline Konstruktor
}

int main() {
	Example o;
	return 0;
}
```
Variante 1:
	Die Initialisierung des Attributs wird im Konstruktor-Körper gemacht. 
Variante 2:
	Die Initialisierung des Attributs wird vor dem Konstruktor-Körper gemacht. 
Variante 3:
	Die Initialisierung des Attributs wird bei der Definition und Deklaration des Attributs gemacht.

### Initialisierung mit Übergabeparameter
``` C++
struct Example {
	std::string s {"Hi"};
	// Konstruktor ueberladen mit Argument
	Example(std::string const &v): s{v} {} // Inline Konstruktor
}

int main() {
	Example o {"Moin"};
	return 0;
}
```

### Default Wert
``` C++
struct Example {
	std::string s;
	// Konstruktor ueberladen mit Argument
	Example(std::string const &v = "Hi"): s{v} {} // Inline Konstruktor
}

int main() {
	Example o1; // Aufruf mit Nutzung des Default Werts
	Example o2 {"Moin"}; // Aufruf mit Übergabeparameter
	return 0;
}
```

## Destruktor
- Kurz dtor
- Wenn der dtor nicht explizit angegeben wird, wird automatisch einer erzeugt.
- Ein Destruktor darf keine Exceptions auslösen
Verwendet für:
- Freigabe von dynamisch allokiertem Speicher
- Trennen von Datenbankverbindungen
- ...

## Accessoren
- kurz getter
- Gewähren Zugriff auf Attribut(e)

## Mutatoren
- kurz setter
- Verändern den Wert eines Attributes

## #TODO wo gehört das hin?

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
# Kopier- und Verschiebesemantik
Standardmäßig wird in einer Klasse zusätzlich zum leeren Konstruktor auch ein copy-Konstruktor, move-Konstruktor, Kopier-Zuweisungsoperator und Verschiebe-Zuweisungsoperator erstellt. 

## Kopier-Konstruktor
- Es wird eine tiefe Kopie der Attribute einer [[Wertkategorien#lvalue|lvalue Referenz]] in ein neues Objekt geschrieben. 
- Die alten Werte bleiben dabei unverändert.
``` C++
A(A const &a) {  
    _nptr = std::make_unique<int>(*a._nptr);  
    _aptr = std::make_unique<std::array<int, 5>>();  
    for (int i{0}; i < _aptr->size(); i++) {  
        (*_aptr)[i] = (*a._aptr)[i];  
    }  
    std::cout << "class A copy constructor: " << *_nptr << std::endl;  
}
```

## Kopier-Zuweisungsoperator
- ähnlich dem [[#Kopier-Konstruktor]], nur für die Zuweisung eines Objekts statt der Instanziierung.
- es kann auch ein default gesetzt werden
- (siehe [[#Operatoren überschreiben]])
``` C++
A&(A const &a) {  
    _nptr = std::make_unique<int>(*a._nptr);  
    _aptr = std::make_unique<std::array<int, 5>>();  
    for (int i{0}; i < _aptr->size(); i++) {  
        (*_aptr)[i] = (*a._aptr)[i];  
    }  
    std::cout << "class A copy constructor: " << *_nptr << std::endl;  
}
// default 
A& operator= (A& a) = default;
```


## Verschiebe-Konstruktor
- Teil der Verschiebesemantik
- Die Attribute einer [[Wertkategorien#rvalue Referenz|rvalue Referenz]] werden in das neue Objekt verschoben. 
- Die alten Werte werden dadurch ungültig.
	- Je nachdem müssen/sollten die Werte händisch ungültig gemacht werden.
``` C++
A(A &&rhs) : _nptr{std::move(rhs._nptr)} {}
```

## Verschiebe-Zuweisungsoperator
- Teil der Verschiebesemantik
-  ähnlich dem [[#Verschiebe-Konstruktor]], nur für die Zuweisung eines Objekts statt der Instanziierung.
- Siehe dazu [[Wertkategorien]].
- (siehe [[#Operatoren überschreiben]])
``` C++
A &operator=(A &&rhs)  noexcept {  
    if (this == &rhs) return *this;
    this->_nptr = std::move(rhs._nptr);
    return *this;
}
```


# Verschachtelte Klassen / Strukturen
``` C++
class Outer {
	int const x {42};
public:
	class Inner {
		int a {42};
	public:
		int GetAX(Outer const &o) {
			return a * o.x;
		}
	};
};
int main() {
	Outer o;
	Outer::Inner data;
	std::cout << data.GetAX(o) << std::endl;
	return 0;
}
```
Zugriff ist ähnlich zu [[Namensräume|Namensräumen]]. 
# Enumeratoren
Klassen/Strukturen mit fest vordefinierten Werten.
- Ähnlich zum Aufzählungstyp enum aus C
- C enum ist ohne scope, bei C++ ist enum Klasse mit scope, d.h. enum ist Teil einer Klasse (bzw. eines structs)
- C++ enum class == C++ enum struct
- C++ enum erlaubt keine Vererbung

## Verwendung
enum wird definiert mit "Platzhalternamen" für dahinterliegenden Wert.
``` C++
enum class State : short {RELEASED, PRESSED, _LENGTH};
enum struct StateMouse {RELEASED, PRESSED}; // wird standardmäßig zum Typ int
// Namen dürfen mehrfach vergeben werden, da sie an class/struct name gebunden sind.
int main() {
	State s1 {State::RELEASED};
	int nStates {static_cast<int>(State::_LENGTH)} // muss explizit gecasted werden
	StateMouse s2 {s1}; // geht implizit weil short < int
	s2 = StateMouse::PRESSED;
	switch(s2){ // für switch-case sind enums empfohlen
		case StateMouse::RELEASED:
			// do something
			break;
		case StateMouse::PRESSED:
			// do something else
			break;
	}
	int 
	
}
```

Standardmäßig wird zählt ein enum von 0 beginnend hoch. Es lassen sich jedoch auch händisch Werte angeben:
``` C++
enum class State : short {RELEASED = 0, PRESSED = 1, _LENGTH = 2};
enum class Color : char {RED = 'r', GREEN = 'g', BLUE = 'b'};
```

## Vergleich C-Stil
``` C++
#include <iostream>

enum Color : char{RED, GREEN, BLUE, _LENGTH}
// nicht erlaubt wäre bei C dann:
// enum ColorRGB : char{RED, GREEN, BLUE}
// da die Bezeichner RED, GREEN, BLUE bereits vergeben sind.
int main() {
	Color c {RED};
	int nColors {_LENGTH}; // Menge an enums implizit gecastet
}
```

# Templateprogrammierung
- Teil der generischen Programmierung
- Programmierung von Klassen, in der die Datentypen (bzw. die Art der Datenstruktur) erst später festgelegt wird.
- werden zur Compilezeit "ausgestanzt", d.h. es werden die benötigten Funktionen mit den richtigen Datentypen gewählt und in das Programm eingebunden.
- Die Methoden der Templates werden in der Headerdatei implementiert, nicht in einer separaten Cpp-Datei!

Templateparameter als Typ
``` C++
template<typename T>
struct MyClass {
	// Hier kann T als Platzhalter-Typ verwendet werden
}
```

Templateparameter als int
``` C++
#include<iostream>
template<int Funktionsauswahl=0>
struct MyClass {
	switch(Funktionsauswahl) {
		case 0:
			std::cout << "Erste Funktion" << std::endl;
			break;
		case 1:
			std::cout << "Zweite Funktion" << std::endl;
			break;
	}
}
```
Der Compiler optimiert / teilt diese Klasse auf die unterschiedlichen Anwendungsmöglichkeiten auf, d.h. z.B. dass die switch-case verschwindet und auf mehrere verschiedene Klassen verteilt wird.

## Vererbung
``` C++
#include <iostream>  
#include <vector>  
  
// Erben von Templateparameter  
template<typename T>  
struct MyVector : std::vector<T> {  
    void Print() {  
        for (T const &v: *this) {  
            std::cout << v << std::endl;  
        }  
    }  
};  
  
int main() {  
    MyVector<int> vi;  
    vi.emplace_back(42);  
    vi.emplace_back(43);  
    vi.Print();  
    MyVector<std::string> vs;  
    vs.emplace_back("Hallo");  
    vs.emplace_back("Welt!");  
    vs.Print();  
}
```
Hier keine typische Vererbung, eher Erweiterung des "std::vector" um die Methode "Print()".

## Variadische Templates
- Templates mit variabler Anzahl an Template-Parametern 

``` C++
#include <iostream>  
#include <array>  
  
template<typename T, int NDIM = 3>  
struct Vektor {  
    std::array<T, NDIM> data;  
  
    // Variadisches Methodentemplate  
    template<typename... TArgs>  
    Vektor(TArgs... args) : data{args...} {}  
  
    Vektor operator+(Vektor const &rhs) const {  
        Vektor v;  
        for (int i = 0; i < NDIM; i++) {  
            v.data[i] = this->data[i] + rhs.data[i];  
        }  
        return v;  
    }  
  
    void Print() {  
        for (auto const &v: data) std::cout << v << " ";  
        std::cout << std::endl;  
    }  
};  
  
int main() {  
    Vektor<double> vd1{1.1, 2.2, 3.3}, vd2{0.5, 2.2, -0.7};  
    Vektor<double> vd3 = vd1 + vd2;  
    vd3.Print();  
    Vektor<int, 5> vi1{1, 2, 3, 4, 5}, vi2{-1, 3, 4, -9, 2};  
    Vektor<int, 5> vi3 = vi1 + vi2;  
    vi3.Print();  
}
```
# Operatoren überschreiben
```c++
class A {
	int level {5};
	// Zuweisungsoperator
	A &operator=(A const &rhs) {  
	    if (this != &rhs) return *this;
	    // Was soll passieren bei einer Zuweisung
	}
	// Multiplikation mit double
	A &operator*(double const &rhs){
		//
	}
	// Linksshiftoperator
	friend void std::ostream &operator<<(std::ostream &os, A const &a)
}
void std::ostream &operator<<(std::ostream &os, A const &a) {
	os << "level: " << a.level << std::endl;
	return os;
};
```

# struct als Aggregat vs. Benutzerdefinierter Typ
kann auch für "struct" verwendet werden:
``` C++
// C Stil
typedef struct mytype1 {
	int a, b, c;
	float x, y, z;
}
// C++ Stil
using mytype2 = struct {
	int a, b, c;
	float x, y, z;
}
// Uniform initalizer list
mytype1 m1 {1, 2, 3, 4.f, 5.f, 6.f};
mytype2 m2 {1, 2, 3, 4.f, 5.f, 6.f};
// Designated initalizer list
// Reihenfolge dennoch relevant! b=0,,x=.0f, y=.0f
mytype2 m3 {.a = 1, .c = 3, .z = 1.0f};

// Zugriff mit . Operator
int s1 = m1.a + m1.b / m1.c;
int s2 = m2.a + m2.b / m2.c;
```

# Vorsicht bei Rückgabewerten
Wenn eine Methode eine Referenz oder Zeiger auf einen enthaltenen Wert zurückgibt, ist Vorsicht geboten.
``` C++
struct Example{
	Example m; // Memberwert
	// ok, by-value, copy-elision
	Example f1(){
		Example e; 
		return e;
	}
	// Definitiv nicht ok, weil nach dem scope der Funktion existiert e garnicht mehr!
	Example &f2(){
		Example e; 
		return e;
	}
	// Wahrscheinlich ok
	Example &f3(Example &in){
		return in;
	}
	// Vorsicht! Ok nur solange Objektinstanz existiert
	Example &f4(){
		return m;
	}
};
```

# Klasse vs. Struktur
- Standardmäßig ist die Zugriffsart bei einer Klasse "private". Bei einem "struct" ist sie standardmäßig "public".
- Siehe dazu [[OOP#Kapselung]].

