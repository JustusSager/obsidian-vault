# Grundideen der OOP
Eine Klasse lässt sich sowohl mit "class" als auch mit "struct" realisieren.
## 1. Abstraktion
Abstraktes KFZ -> PKW -> Sport PKW -> Sport Cabrio PKW

## 2. Vererbung ^ec603c
Bei der Vererbung erbt eine spezialisierte Klasse die grundlegenden Eigenschaften einer verallgemeinerten/abstrakteren Klasse.  
Sport Cabrio PKW erbt von KFZ "kann fahren" und "hat Kraftantrieb"

Vererbung muss jedoch nicht erzwungen werden. Wenn es keinen sinnvollen Einsatz gibt, lieber weglassen, oder eine Alternative wählen.

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

### Alternative zur klassischen Vererbung
Nicht immer ist eine Vererbung sinnvoll zur Modellierung des Systems. Alternativ gibt es dazu:
#### Komposition: 
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

#### Aggregation
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


### Mehrfachvererbung
In C++ kann eine Klasse von mehreren Klassen erben. Hat in der OOP jedoch eher selten einen Anwendungsfall.
``` C++
#include <string>  
#include <iostream>  
class Pferd {  
public:  
    std::string GetMom() {  
        return "Pferd";  
    }  
};  
class Esel {  
public:  
    std::string GetDad() {  
        return "Esel";  
    }  
};  
class Maultier final : public Pferd, public Esel {  
public:  
    std::string GetParents() {  
        return GetMom() + " und " + GetDad();  
    }  
};  
int main() {  
    Maultier m;  
    std::cout << m.GetParents() << std::endl;  
}
```

#### Rautenproblem ^4efd9e
Bei der Mehrfachvererbung kann es zum Rautenproblem kommen.
![[Pasted image 20250408152112.png]]
Lösung:
Verwendung von virtueller Vererbung. Siehe dazu [[Schlüsselwörter in C++#^5cddfb|virtual bei der Vererbung von Klassen]]. 

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
- [[Klassen und Strukturen#^6cee62|Konstruktor]] kann nicht virtuell sein, da Typ bei Objekterzeugung zu Compilezeit bereits bekannt ist
- [[Klassen und Strukturen#^cf0bc4|Destruktor]]
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

Aufruf über [[Standardcontainer#^711fef|smarte Pointer]]:
``` C++
#include <memory>
int main() {  
    std::unique_ptr<B> ptrb {new X{}};  
    ptrb->Say();  // Ausgabe: X
}
```

# RAII
(Resource Acquisition Is Initialisation)
- Anforderung einer Resource = Initialisierung einer Resource
- Initialisierung durch [[Klassen und Strukturen#^6cee62|ctor]]
- Löschen der Ressourcen durch [[Klassen und Strukturen#^cf0bc4|dtor]] 
- Richtig angewendetes RAII extrem wichtig für die Vermeidung von Speicherleaks!
- Eigener dtor nicht nötig wenn Klasse nur ...
	- 'Werte' d.h. keinen dynamisch mit new/delete verwalteten Speicher nutzt
	- Container wie bspw. [[Standardcontainer#^3232b4|std::vector]] aus der Standardbibliothek nutzt, da diese bereits selbst Acquise und Freigabe des dynamischen Speichers verwalten

# Überladen von Methoden
Beim Überladen von Methoden bleibt der Rückgabewert gleich.
## Überladen von Operatoren
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



# Überschreiben von Methoden
#TODO 
