# Grundideen der OOP
Eine Klasse lässt sich sowohl mit "class" als auch mit "struct" realisieren.
## 1. Abstraktion
Abstraktes KFZ -> PKW -> Sport PKW -> Sport Cabrio PKW

## 2. Vererbung
Sport Cabrio PKW erbt von KFZ "kann fahren" und "hat Kraftantrieb"

## 3. Kapselung
Nur KFZ kennt seine inneren Werte und kann auf diese Zugreifen. Zugriff von außen ist verboten.
Der Zugriff auf die Daten soll soweit wie möglich beschränkt werden.
Der Datenzugriff erfolgt typischerweise über "Getter" und "Setter" Methoden.
	bedingt sinnvoll da es viel "boilerplate" Code erzeugt. Man könnte auch einfach die entsprechenden Variablen public machen.
	Erst wirklich sinnvoll bei der Verarbeitung der übergebenen Attribute.
	
Zugriffsspezifizierer ("public", "protected", "private") legen Zugriffsart fest. 
Standardmäßig ist die Zugriffsart bei einer Klasse "private". Bei einem "struct" ist sie standardmäßig "public".
``` C++
class MyClass1 {
	std::string name; // ist private
	public:
		void print();
	protected:
		int a;
}
```

## 4. Polymorphismus (Vielgestaltigkeit)
Sport PKW kann sich wie abstraktes KWZ verhalten.

# Umsetzung
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
Kurz ctor
Konstruktorname = Klassenname
Wenn ctor nicht explizit definiert wird, wird automatisch einer generiert, welcher keine Übergabeparameter hat (Default ctor). Sobald ein Konstruktor definiert wird, wird kein default ctor mehr erstellt.
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

# Begriffe
Funktionen in einer Klasse heißen Methoden.
	Eine Botschaft besteht aus dem Namen der Funktion und evtl. Argumenten.
		Objekte verständigen sich über Botschaften.
Variablen einer Klasse heißen Attribute (Properties)

## wichtigste Methoden
- Konstruktoren: Erzeugen ein Objekt.
- Destruktoren: Zerstören ein Objekt.
- Mutatoren: Verändern den Wert eines Attributes (z.B. "Setter")
- Accessoren: Gewähren Zugriff auf Attribut(e) (z.B. "Getter")


