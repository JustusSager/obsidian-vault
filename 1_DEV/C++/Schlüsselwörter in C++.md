# extern
Kann für globale Variablen verwendet werden, sollten nicht zu sehr genutzt werden.
Eine Möglichkeit der Strukturierung ist alle in einem Modul zu sammeln. Damit ist eindeutig wo sie sind und welche existieren.
Globale Variablen erlauben Zugriff auf anderswo definierte Bezeichner.

globals.hpp
``` C++
#ifndef FH_PROJEKT_GLOBALS_HPP 
#define FH_PROJEKT_GLOBALS_HPP

extern int global_a; // Deklaration

#endif
```
globals.cpp
``` C++
#include "globals.hpp"

int global_a {42}; // Definition und Initialisierung
```

Das Keyword "extern" sorgt dafür, dass in der Header Datei die Variable "global_a" nur deklariert wird, jedoch nicht definiert. Das wird benötigt da ansonsten der include zu einer Mehrfachdefinition von global_a führt.

# const
## const Methoden einer Klasse
Methoden mit dem Schlüsselwort "const" dürfen keine Memberwerte verändern, sie können ausschließlich lesend auf Memberwerte zugreifen.
``` C++
class Example{
	int a{42};
public:
	void ResetA(){
		a = 22;
	}
	int GetA() const{
		// ResetA(); // Fehler, nur weitere const Methoden aufrufbar
		// a = 55; // schreiben ist verboten!
		return a;
	}
};
```

# static
## static macht lokal: Internal Linkage ^0a1f78
Das Keyword static sorgt dafür, dass ein Name (also ein Bezeichner für Variablen und Funktionen) nur innerhalb des Moduls zur Verfügung steht. Dadurch lassen sich Namen über die Module hinweg mehrfach verwenden.

Beispiel:
modul1.hpp
``` C++
void CallMe();
static void f(); // eig. werden nicht-öffentliche Funktionen hier gar nicht angegeben. Vorwärtsdeklaration würde man eher in modul1.cpp machen.
```
modul1.cpp
``` C++
#include <iostream>
// static void f(); // Vorwärtsdeklaration
static int a {5};
void CallMe() {
	f();
}
static void f() {
	std::cerr << "Static" << std:: endl;
}
```
main.cpp
``` C++
#include "modul1.hpp"
int main() {
	CallMe(); // ok
	f(); // Linkfehler, da static 
}
```
modul2.cpp
``` C++
static int a {5}; // ok da static
void CallMe() { // Linkfehler, da dublicate Symbol. CallMe() gibts schon in modul1
	int x {5};
}
```

## static teilt instanzübergreifend in Klassen
Variablen und Funktionen, die sich nicht mehr auf die Objektinstanz beziehen, sondern auf die gesamte Klasse, und über alle Objektinstanzen dieser Klasse gültig/identisch ist. Es ist keine Instanziierung der Klasse nötig.
Bei einer Variable existiert diese Variable nur einmal, über die Klasse und aller Instanzen dieser Klasse.
Bei einer Methode existiert kein this-Pointer, da sich die Methode nicht auf eine bestimmte Objektinstanz bezieht. Methodenaufruf wird findet nicht mit ".", sondern über den Klassennamen mit "::" statt. 

Beispiel für eine static-Variable:
``` C++
#include <iostream>
class Example {
	static int a_;
public:
	void SetA(int a) {
		Example::a_ = a;
	}
	int GetA() {
		return Example::a_;
	}
};
int Example::a_ {42}; // Initialisierung muss out-of-line sein!
int main() {
	Example e1, e2;
	e1.SetA(22); // In e1 wird a_ auf 22 gesetzt
	sts::cout << e2.GetA() << std::endl; // Ausgabe über e2 gibt dennoch auch 22 aus.
	return 0;
}
```

Beispiel für eine static-Methode:
``` C++
#include <iostream>
class Example {
	int a_;
public:
	// Mini-Factory
	static Example Create(int const v) {
		Example e;
		e.a_ = v;
		return e;
	}
	void Print() {
		std::cout << a_ << std::endl;
	}
};
int main() {
	Example e1 = Example::Create(42);
	Example e2 = Example::Create(22);
	e1.Print();
	e2.Print();
	return 0;
}
```

## static macht dauerhaft
Eine Variable wird dadurch dauerhaft. #TODO Hier nochmal schauen. Kommt aus Video 3, ca. 20 Min. 
``` C++
#include <iostream>
struct Example {
	int GetVal() {
		static int val {0};
		return val++;
	}
};
int main() {
	Example e1, e2;
	std::cout << e1.GetVal() << " " << e2.GetVal() << std::endl;
	return 0;
}
```
Hier wird die Variable val nur einmal angelegt. e1 und e2 greifen hier beide auf den selben Speicher zu (bzw. teilen sich die Variable "val").

# friend
Mit dem "friend" Schlüsselwort lassen sich Klassen (und Funktionen) als "Freunde" einer Klasse definieren. Dies erlaubt den Zugriff auf deren "private" und "protected" Funktionen und Variablen.
``` C++
#include <iostream>
class Container {
	double level {0};
public:
	void Refill() {
		level = 1.;
	}
	friend void SayLevel(Container const &c)
}
void SayLevel(Container const &c) {
	std::cout << "level: " << c.level << std::endl;
};
int main() {
	Container c;
	SayLevel(c);
	c.Refill();
	SayLevel(c);
}
```
Hier wird eine Funktion "SayLevel()" definiert, welche "befreundet" ist mit der Klasse "Container". Dadurch kann "SayLevel()" auf die private Variable "level" von "Container" zugreifen.

Alternativ, kann für eine Ausgabe auch der "<<" Operator überschrieben werden:
``` C++
#include <iostream>
class Container {
	double level {0};
public:
	void Refill() {
		level = 1.;
	}
	friend std::ostream &operator<<(std::ostream &os, Container const &c);
}
void std::ostream &operator<<(std::ostream &os, Container const &c) {
	os << "level: " << c.level << std::endl;
	return os;
};
int main() {
	Container c;
	SayLevel(c);
	c.Refill();
	SayLevel(c);
}
```
Hier wird der "<<" Operator des Ausgabe-Streams "befreundet" und für "Container" definiert, wodurch dieser auf die private Variable "level" von "Container" zugreifen kann und man jetzt mit dem "<<" Operator "level" in einen Ausgabe-Stream leiten kann.

Die Definitionen des "<<" Operators und der "SayLevel()" Funktion sind freistehend, d.h. sie ist nicht Teil der "Container" Klasse. Man kann diese auch "In-Line" definieren, dadurch werden sie jedoch immer noch nicht Teil der Klasse:
``` C++
#include <iostream>
class Container {
	double level {0};
public:
	void Refill() {
		level = 1.;
	}
	friend std::ostream &operator<<(std::ostream &os, Container const &c) {
		os << "level: " << c.level << std::endl;
		return os;
	}
};
int main() {
	Container c;
	SayLevel(c);
	c.Refill();
	SayLevel(c);
}
```

# this
Beim Aufruf einer Klassenmethode wird automatisch der sog. this-Zeiger als Funktionsparameter erzeugt.
this ist vom Typ "Typ * const". Dieser Zeiger zeigt auf die Klasseninstanz (bzw. auf das Objekt) in dem der Funktionsaufruf stattfindet.
"this" kann explizit mit "this->" dereferenziert werden.
``` C++
class Example{
	int a_, b_;
public:
	void SetAB(int const &a, int const &b){
		a_ = a; // implizit this->
		this->b_ = b; // explizit this->
	}
};
int main(){
	Example e;
	e.SetAB(2, 3);
	return 0;
}
```

## Kaskade an Methodenaufrufen
``` C++
#include <iostream>
struct Test {
	Test links() {
		std::cout << "links" << std::endl;
		return *this;
	}
	Test rechts() {
		std::cout << "rechts" << std::endl;
		return *this;
	}
};
int main() {
	Test t;
	t.links().links().rechts().links();
	return 0;
}
```

# final
## final bei Klassen
Blockiert  die Vererbung einer Klasse.
``` C++
class Example final {
	int a;
};
class Example2 : Example { // Diese Vererbung wäre unzulässig
};
```

## final bei Methoden einer Klasse
Methoden, die mit final ausgezeichnet sind dürfen nicht mehr überschrieben werden.
``` C++
struct Base{
	virtual int Op(int const a, int const b) const {
		return a+b;
	}
};
struct Derived : public Base{
	int Op(int const a, int const b) const override final{
		return Base::Op(a, b) + Base::Op(a, b);
	}
};
struct Derived2 : public Derived{
	// durch final erneutes Ueberschreiben nicht erlaubt!
	int Op(int const a, int const b) const override{
		return a-b;
	}
};
```

# virtual ^3bfa14

## virtual vor einer Methode einer Klasse
#TODO Folie 188
Eine Methode kann so überschrieben werden, dass zur Laufzeit ein Objekt einer Vererbungshierarchie dynamisch zugeordnet werden kann. 
``` C++
#include <iostream>
#include <string>
struct Basis {
	std::string s = "Basis";
	virtual std::string wert() const { return s; }
	void print() const { std::cout << wert() << std::endl; }
};
struct Wert {
	std::string s = "Wert";
	virtual std::string wert() const { return s; }
};
int main() {
	Wert w;
	w.print();
}
```
Bei "w.print()" wird auf das "print()" von "Basis" zugegriffen. "Basis" kennt jedoch nur seine eigene "wert()" Methode, welche auf das "s" von "Basis" zugreift und damit "Basis" zurückgibt.
Durch das virtual bekommt der compiler die Information, dass der Zugriff auf "wert()" zur Laufzeit ausgewertet werden soll. Dadurch wird bei dem "print()" von "Basis" nicht mehr auf das "wert()" von "Basis" zugegriffen, sondern auf das "wert()" von "Wert".

## virtual bei der Vererbung von Klassen ^5cddfb
Lösung für das [[OOP#^4efd9e|Rautenproblem]]. 
``` C++
#include <iostream>
struct P{
	int data {42};
};
struct C1 : public virtual P{};
struct C2 : public virtual P{};
struct D : public C1, public C2{
	int GetData(){
		// geht nur wenn vorher
		// mit virtual geerbt!
		// sonst mehrdeutig
		return data;
	}
};
int main() {
	D d;
	std::cout << d.GetData();
}
```

# override ^f4ccf4
- Mit override verlangt der Compiler, dass das Überschreiben der Methode auch wirklich eine andere überschreibt
- Hilft zur Vermeidung und zum Entdecken von Programmierfehlern
- I.d.R. immer override beim überschreiben von Methoden verwenden!

``` C++
struct Basis {
	virtual int Calc(int a, int b){
		return a+b;
	}
};
struct Child : public Basis {
	// Programmierfehler?!
	// Override erzeugt Compilierfehler
	int Calc(int a) override {
		return a+a;
	}
	// Wuerde sonst Basis::Calc "verstecken"
	// int Calc(int a) {return a+a;}
};
int main() {
	Child c;
	std::cout << c.Calc(22) << std::endl;
}
```

#TODO Folie 189ff.