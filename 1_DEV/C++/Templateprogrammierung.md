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

# Vererbung

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

# Variadische Templates
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
