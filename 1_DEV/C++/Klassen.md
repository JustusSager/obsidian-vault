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

## Konstruktor ^6cee62
- Kurz ctor
- Konstruktorname = Klassenname
- Wenn ctor nicht explizit definiert wird, wird automatisch einer generiert, welcher keine Übergabeparameter hat (Default ctor). Sobald ein Konstruktor definiert wird, wird kein default ctor mehr erstellt.
- Ein Konstruktor darf keine Exceptions auslösen
- Konstruktoren werden nicht weitervererbt
- Siehe dazu auch [[OOP - 2 Vererbung#^9b1e21|Vererbung von Konstruktoren]].
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

## Destruktor ^cf0bc4
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
- Siehe dazu [[OOP - 3 Kapselung]].

