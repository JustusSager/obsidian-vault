# Grundideen der OOP
Eine Klasse lässt sich sowohl mit "class" als auch mit "struct" realisieren.
## 1. Abstraktion
Abstraktes KFZ -> PKW -> Sport PKW -> Sport Cabrio PKW

## 2. Vererbung ^ec603c
Bei der Vererbung erbt eine spezialisierte Klasse die grundlegenden Eigenschaften einer verallgemeinerten/abstrakteren Klasse.  
Sport Cabrio PKW erbt von KFZ "kann fahren" und "hat Kraftantrieb"

Vererbung muss jedoch nicht erzwungen werden. Wenn es keinen sinnvollen Einsatz gibt, lieber weglassen, oder eine Alternative wählen. Siehe [[#^bfc8e0|Alternative zur Vererbung]].

Beispiel:
``` C++
#include <iostream>
class KFZ {
	bool hatKraftantrieb {False};
public:
	void Fahren() {
		// ..
	}
	bool HatKraftantrieb() {
		return hatKraftantrieb;
	}
}
class PKW : public KFZ {
}
int main() {
	PKW pkw;
	// über PKW kann man auf die Methode von KFZ zugreifen
	pkw.Fahren();
}
```

### public, protected und private
Man kann bei der Vererbung, die Zugriffsrechte der Methoden und Variablen, die man erbt, manipulieren.  Siehe dazu [[#^c813ad|Kapselung]]
Wenn der Erbende eine "class" ist, ist der default die "private" Vererbung. Bei "struct" ist es die "public" Vererbung.
public
- public Methoden und Variablen bleiben in der erbenden Klasse public.
- protected Methoden und Variablen bleiben in der erbenden Klasse protected.
- die erbende Klasse kann nicht auf private Methoden und Variablen zugreifen.
protected
- public Methoden und Variablen werden in der erbenden Klasse protected.
- protected Methoden und Variablen bleiben in der erbenden Klasse protected.
-  die erbende Klasse kann nicht auf private Methoden und Variablen zugreifen.
private
- public Methoden und Variablen werden in der erbenden Klasse private.
- protected Methoden und Variablen werden in der erbenden Klasse private.
-  die erbende Klasse kann nicht auf private Methoden und Variablen zugreifen.

## 3. Kapselung ^c813ad
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

### public
Ein Zugriff auf die Variablen und Methoden ist ...
- von außerhalb der Klasse (ausgenommen erbende Klassen) möglich
- von erbenden Klassen möglich
- innerhalb der eigenen Klasse möglich

### protected
Ein Zugriff auf die Variablen und Methoden ist ...
- nicht mehr von außerhalb der Klasse (ausgenommen erbende Klassen) möglich
- von erbenden Klassen möglich
- innerhalb der eigenen Klasse möglich

### private
Ein Zugriff auf die Variablen und Methoden ist ...
- nicht mehr von außerhalb der Klasse (ausgenommen erbende Klassen) möglich.
- nicht mehr von den erbenden Klassen möglich.
- innerhalb der eigenen Klasse möglich.

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
- Kurz ctor
- Konstruktorname = Klassenname
- Wenn ctor nicht explizit definiert wird, wird automatisch einer generiert, welcher keine Übergabeparameter hat (Default ctor). Sobald ein Konstruktor definiert wird, wird kein default ctor mehr erstellt.
- Ein Konstruktor darf keine Exceptions auslösen
- Konstruktoren werden nicht weitervererbt
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

### Vererbung von Konstruktoren
Konstruktoren werden in C++11 standardmäßig nicht weiter vererbt!
``` C++
#include <iostream>
class Parent {
protected:
	int x_;
public:
	Parent() = default;
	Parent(int const &x) : x_{x} {}
	void SayX() {
		std::cout << x_ << std::endl;
	}
};
class Child : Parent {
	
}
int main() {
	Child c = Child(42) // funktioniert nicht 
}
```
In Version C++17 (aufwärts) läufts irgendwie anders. Da würde es durchlaufen, solange in Child keine Konstruktoren definiert sind.

Es lässt sich jedoch festlegen, dass die Konstruktoren mit übernommen werden.
``` C++
class Parent {
protected:
	int x_;
public:
	Parent() = default;
	Parent(int const &x) : x_{x} {}
	void SayX() {
		std::cout << x_ << std::endl;
	}
};
class Child : Parent {
	using Parent::Parent // eindeutig die Konstruktoren mit übernehmen
}
int main() {
	Child c = Child(42)
}
```

## Destruktor

^cf0bc4

- Kurz dtor
- Wenn der dtor nicht explizit angegeben wird, wird automatisch einer erzeugt.
- Ein Destruktor darf keine Exceptions auslösen

### Nutzung:
- Freigabe von dynamisch allokiertem Speicher
- Trennen von Datenbankverbindungen
- ...


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

## RAII
(Resource Acquisition Is Initialisation)
- Anforderung einer Resource = Initialisierung einer Resource
- Initialisierung durch [[#^6cee62|ctor]]
- Löschen der Ressourcen durch [[#^cf0bc4|dtor]]
- Richtig angewendetes RAII extrem wichtig für die Vermeidung von Speicherleaks!
- Eigener dtor nicht nötig wenn Klasse nur ...
	- 'Werte' d.h. keinen dynamisch mit new/delete verwalteten Speicher nutzt
	- Container wie bspw. [[Arrays und Vektoren#^3232b4|std::vector]] aus der Standardbibliothek nutzt, da diese bereits selbst Acquise und Freigabe des dynamischen Speichers verwalten

## Alternative zur [[#^ec603c|Vererbung]] ^bfc8e0
Nicht immer ist eine Vererbung sinnvoll zur Modellierung des Systems. Alternativ gibt es dazu:
### Komposition: 
"hat ein" Beziehung als starke Bindung. D.h. ein Objekt enthält immer ein anderes Objekt, welches teil von ihm ist.
Z.B. Ein Auto Objekt hat immer ein Lenkrad Objekt, welches ein Teil des Auto Objekts ist.
``` C++
class Auto {
	Lenkrad lenkrad_;
	std::vector<Rad> raeder_;
	// ...
};
```
Lenkrad und Rad sind feste Bestandteile von Auto.

![[OOP_Komposition.png]]

### Aggregation
"hat ein" Beziehung als lose Bindung. D.h. ein Objekt kann in Beziehung zu einem anderen verbundenen Objekt stehen. Beide Objekte sind jedoch unabhängig voneinander (separierbar).
Z.B. Auto hat einen Besitzer, Auto hat eine Garage

``` C++
class Auto {
	Garage& garage_;
	Person& eigentuemer_;
	// ...
};
```
Garage und Person werden von Auto nur referenziert.

![[OOP_Aggregation.png]]

## Überladen von Methoden
Beim Überladen von Methoden bleibt der Rückgabewert gleich.
### Überladen von Operatoren
``` C++
class Vektor{
	double x_, y_;
public:
	Vektor(double x, double y) :
	x_{x}, y_{y} {}
	// Skalarprodukt
	double operator*(Vektor const &rhs){
		return this->x_*rhs.x_ + this->y_*rhs.y_;
	}
	// Multiplikation mit Skalar
	Vektor operator*(double const &rhs){
		return Vektor {this->x_*rhs, this->y_*rhs};
	}
};
int main(){
	Vektor v1 {1., 2.};
	double s = v1*v1; // Skalarprodukt
	Vektor v2 {v1 * 2.5};
	Vektor v3 {2.5 * v1} // würde nicht gehen da der Operator * nur andersherum überladen wurde
	return 0;
}
```



## Überschreiben von Methoden


# Begriffe
Funktionen in einer Klasse heißen Methoden.
	Eine Botschaft besteht aus dem Namen der Funktion und evtl. Argumenten.
		Objekte verständigen sich über Botschaften.
Variablen einer Klasse heißen Attribute (Properties)

## wichtigste Methoden
- Mutatoren: Verändern den Wert eines Attributes (z.B. "Setter")
- Accessoren: Gewähren Zugriff auf Attribut(e) (z.B. "Getter")
