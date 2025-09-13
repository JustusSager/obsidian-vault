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

## public, protected und private
Man kann bei der Vererbung, die Zugriffsrechte der Methoden und Variablen, die man erbt, manipulieren.  Siehe dazu [[OOP - 3 Kapselung]]
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

## Alternative zur klassischen Vererbung
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

## Mehrfachvererbung
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
![[mehrfachvererbung-rautenproblem.png]]
Lösung:
Verwendung von virtueller Vererbung. Siehe dazu [[Schlüsselwörter in C++#^5cddfb|virtual bei der Vererbung von Klassen]]. 

## Vererbung von Konstruktoren ^9b1e21
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
	using Parent::Parent; // eindeutig die Konstruktoren mit übernehmen
}
int main() {
	Child c = Child(42)
}
```
