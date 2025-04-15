Headerdatei:
``` C++
#include <memory>
```

## Smarte Pointer ^711fef
Spezielle "schlaue" Pointer aus der Standardbibliothek, welche als eigenständige Klasse implementiert ist und die Speicherverwaltung der in C/C++ eingebauten Pointer aufbessert.

### unique_ptr
- Besitzt den Pointer, nicht kopierbar. D.h. Der Pointer gehört immer nur einem Objekt gleichzeitig. Es können nie mehrere Objekte auf diesele Adresse zeigen.
- Erste Wahl, wenn es zu jedem Zeitpunkt einen eindeutigen Besitzer des Zeigers geben soll, also jemanden, der den eingepackten rohen Zeiger am Ende wegräumen soll.
- verlässt nie den Gültigkeitsbereich, in dem er definiert worden ist und wird somit automatisch aufgeräumt, sobald die Lebenszeit des Pointers des Ende erreicht.

#### Verwendung:
``` C++
#include <iostream>
#include <memory>
struct A{
	int val {42};
	explicit A(int v) : 
		val{v} {}
	void SayVal(){
		std::cout << val << std::endl;
	}
	~A(){
		std::cout << "dtor called\n";
	}
};
int main(){
	auto a1 = std::unique_ptr<A> {new A{42}};
	// seit c++14
	auto a2 = std::make_unique<A>(43);
	std::swap(a2, a1); // Die Pointer werden vertauscht
	a1->SayVal();
	a2->SayVal();
	// dtor fuer a2 wird automatisch aufgerufen
	a1 = std::move(a2); // 
	a1->SayVal();
	// kein delete noetig!
}
```

##### Vergleich mit Stackvariable und Pointer
``` C++
#include <iostream>  
#include <memory>  
#include <string>  
struct A{  
    std::string val;  
    explicit A(std::string v) :  
            val{v} {  
        std::cout << "ctor called" << std::endl;  
    }  
    void SayVal(){  
        std::cout << val << std::endl;  
    }  
    ~A(){  
        std::cout << "dtor called\n";  
    }  
};  
int main() {  
    // Stackvariable  
    A a1 {"A1"};  
    a1.SayVal();  
    // kein delete nötig, da eine Stackvariable automatisch verwaltet ist.  
  
    // Heapobjekt mit Pointer    A *a2ptr {new A{"A2"}};  
    a2ptr->SayVal(); // dereferenzierung über "->"  
    (*a2ptr).SayVal(); // dereferenzierung über "*"  
    delete a2ptr; // delete nötig, da sonst SEGFAULT!  
  
    // Heapobjekt mit smart-Pointer    std::unique_ptr<A> a3 {new A{"A3"}};  
    a3->SayVal();  
    // kein delete nötig, da sich der smart-Pointer darum kümmert
    // ähnliches Verhalten zu Stackobjekten
}
```

##### Beispiel mit vector:
``` C++
#include <iostream>
#include <memory>
struct A{
	int val {42};
	explicit A(int v) : 
		val{v} {}
	void SayVal(){
		std::cout << val << std::endl;
	}
	~A(){
		std::cout << "dtor called\n";
	}
};
int main() {
	std::vector<std::unique_ptr<A>> vuptra;
	// unique_ptr "in place" hinten an den vector anhängen.
	vuptra.emplace_back(new A{42});
	vuptra.emplace_back(new A{43});
	// Alternativ:
	vuptra.emplace_back(std::make_unique<A>(44));
	vuptra.emplace_back(std::make_unique<A>(44));
	
	// unique_ptr "by copy" anhängen geht nicht
	// vuptra.push_back(new A{45});
	
	// erst Pointer dann anhängen
	std::unique_ptr<A> a1 {new A{45}};
	vuptra.emplace_back(a1); // funktioniert, danach zeigt a1 auf nullptr
	std::unique_ptr<A> a2 {new A{46}};
	vuptra.push_back(std::move(a2)); // funktioniert, danach zeigt a2 auf nullptr
	vuptra.push_back(make_unique<A>(47))

	// Wert löschen
	vuptra.erase(vuptra.begin()+1) // zweites Element löschen, Speicher vom A-Objekt wird automatisch auch freigegeben (Destruktor aufgerufen)
	
}
```
### shared_ptr
- Besitzt den rohen Zeiger zusammen mit anderen, Kopieren und Verschieben möglich, beim Entfernen der letzten Kopie wird auch roher Zeiger entfernt.
- Einsetzen wenn nicht klar ist, wer alles die Objekte besitzt und wann exakt sie weggeräumt werden sollen. Außerdem, wenn es Zeitpunkte gibt, zu denen mehrere Eigner die Objekte besitzen

#### Verwendung:
``` C++
#include <iostream>
#include <memory>
struct A{
	int val {42};
	explicit A(int v) : 
		val{v} {}
	void SayVal(){
		std::cout << val << std::endl;
	}
	~A(){
		std::cout << "dtor called\n";
	}
};
int main(){
	std::shared_ptr<A> a1 {new A{42}};
	// seit c++14
	auto a2 = std::make_unique<A>(43);
	a1->SayVal();
	a2->SayVal();
	std::shared_ptr<A> a3 {a1}; // a3 kann hier auf das selbe Objekt von a1 zeigen, d.h. es existtieren nur 2 A-Objekte doch 3 Zeiger
	a3->SayVal();
}
```

#### Typkonvertierung
``` C++
#include <iostream>  
#include <memory>  
class B {  
public:  
    virtual void Say() const {  
        std::cout << "B" << std::endl;  
    }  
    virtual ~B() = default;  
};  
class X : public B {  
public:  
    void Say() const override {  
        std::cout << "X" << std::endl;  
    }  
    ~X() = default;  
};  
class Y : public B {  
public:  
    void Say() const override {  
        std::cout << "Y" << std::endl;  
    }  
  
    ~Y() = default;  
};  
```

Konvertieren in Basisklasse:
``` C++
int main() {    
    std::shared_ptr<X> sptrX{new X{}};
    std::shared_ptr<B> sptrB2{nullptr};
  
    sptrB2 = std::dynamic_pointer_cast<B>(sptrX);  
    sptrB2->Say(); // Ausgabe: X
}
```

Konvertieren in "Geschwister"-Klasse
``` C++
int main() {
    std::shared_ptr<Y> sptrY{new Y{}};  
    std::shared_ptr<X> sptrX2{nullptr};  
    // funktioniert nicht, da sie spezielle unterschiedliche Objekte sind
    sptrX2 = std::dynamic_pointer_cast<X>(sptrY);  
    if (nullptr == sptrX2) {  
        std::cout << "sptrX2 is nullptr!" << std::endl;  
    }
}
```

Basisklasse (mit einer Instanz der Basisklasse) in spezielle Klasse konvertieren:
``` C++
int main() {  
    std::shared_ptr<B> sptrB{new B{}};
    std::shared_ptr<X> sptrX2{nullptr};  
    // funktioniert nicht
    sptrX2 = std::dynamic_pointer_cast<X>(sptrB);  
    if (nullptr == sptrX2) {  
        std::cout << "sptrX2 is nullptr!" << std::endl;  
    }  
}
```

Basisklasse (mit einer Instanz der speziellen Klasse) in spezielle Klasse konvertieren:
``` C++
int main() {  
    std::shared_ptr<B> sptrB{new X{}};
    std::shared_ptr<X> sptrX2{nullptr};  
    // funktioniert
    sptrX2 = std::dynamic_pointer_cast<X>(sptrB);  
    sprtX2->Say();
}
```
