Sport PKW kann sich wie abstraktes KFZ verhalten.

### Laufzeitpolymorphismus
- Allgemeinere Klasse wird in einer Deklaration verwendet, zur Laufzeit wird jedoch eine andere konkretere Klasse verwendet, mit ihren speziellen Eigenschaften.
- Diese Form der Polymorphie erfordert in C++ den Einsatz von Referenzen oder Zeigern, d.h. Referenzsemantik
- Vorgehensweise:
	- Erzeugen einer Vererbungshierarchie
	- Nutzung von [[Schlüsselwörter in C++#^3bfa14|virtual]] für Methoden -> d.h. Auflösen zur Laufzeit
	- Überschreiben ([[Schlüsselwörter in C++#^f4ccf4|override]]) von Methoden in spezialisierten Klassen
	- Nutzung von pur-virtuelle Methoden für Abstrakte Klassen / Interfaces
	- Implementieren von Methoden in spezialisierten Klassen
- Der Compiler implementiert den Laufzeitpolymorphismus i.d.R. über sogenannte virtual-Table
- Best practice: Klasse entweder ganz ohne oder ganz mit “virtual”
	- Ohne Hierarchie (d.h. Vererbung) ganz ohne “virtual”
	- Mit Hierarchie ganz mit “virtual”
- Virtuelle Methoden
	- Können nicht statisch sein
	- Müssen über Referenzsemantik angesprochen werden, um Laufzeitpolymorphismus zu erreichen
- [[Klassen#^6cee62|Konstruktor]] kann nicht virtuell sein, da Typ bei Objekterzeugung zu Compilezeit bereits bekannt ist
- [[Klassen#^cf0bc4|Destruktor]]
	- Von Basis muss virtuell sein, damit zur Laufzeit der richtige Destruktor aufgerufen werden kann
	- Wenn über Basis auf Objekt bei Laufzeitpolymorphismus zugegriffen wird, wird sonst nur der Basisdestruktor aufgerufen (statische Bindung)
	- Achtung, ggf. Speicherlecks die schwer zu detektieren sind!

Klassen:
``` C++
#include <iostream>  
  
class B {  
public:  
    // virtual muss nur bei der geerbten Klasse angegben werden  
    virtual void Say() const {  
        std::cout << "B" << std::endl;  
    }  
  
    // Achtung, auch der Destruktor muss virtual gesetzt werden!  
    virtual ~B() {  
        std::cout << "B dtor" << std::endl;  
    }  
};  
  
class X : public B {  
public:  
    void Say() const override {  
        std::cout << "X" << std::endl;  
    }  
  
    // Es wird sowohl der Destruktor von X als auch von B aufgerufen.  
    ~X() {  
        std::cout << "X dtor" << std::endl;  
    }  
};  
  
class Y : public B {  
public:  
    void Say() const override {  
        std::cout << "Y" << std::endl;  
    }  
  
    ~Y() {  
        std::cout << "Y dtor" << std::endl;  
    }  
};
```

Aufruf als Stackvariablen:
``` C++
int main() {
	B b;
	b.Say(); // Ausgabe: B
	X x;
	x.Say(); // Ausgabe: X
	b = x;
	b.Say(); // Ausgabe: B, also nicht Polymorph
}
```

Aufruf über Referenzsemantik:
``` C++
int main() {
	X x;
	B &refx {x};
	refx.Say(); // Ausgabe: X Polymorphismus funktioniert, weil Referenzsemantik
}
```

Aufruf über Pointer:
``` C++
int main() {
	B *ptrb {new X{}}; // Hinter dem Zeiger vom Typ B, verstekt sich ein Objekt vom Typ X
	ptrb->Say(); // Ausgabe: X, beim dereferenzieren wird Methode von Typ X aufgerufen
	delete ptrb; // Aber Achtung, wenn der Destruktor von B nicht "virtual" ist, wird nur der Destruktor von B aufgerufen, nicht der von X!
}
```

Aufruf über [[Memory Management Lib#^711fef|smarte Pointer]]:
``` C++
#include <memory>
int main() {  
    std::unique_ptr<B> ptrb {new X{}};  
    ptrb->Say();  // Ausgabe: X
}
```
