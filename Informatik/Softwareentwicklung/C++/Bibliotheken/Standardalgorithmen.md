# std::algorithm
Enthält typische Standardalgorithmen wie Suchen, Zählen, Sortieren, etc. für Daten-Container (siehe dazu z.B. [[Standardcontainer]]). Dabei werden [[Iteratoren]] verwendet um auf der Datenmenge zu arbeiten.
Nicht jeder Algorithmus ist auf jeden Container anwendbar.

## Sortieren 
``` C++
#include <iostream>
#include <algorithm>
#include <vector>
#include <cmath>
double rand_d() { // [0..1]
	double v = rand();
	v /= RAND_MAX;
	return v;
}
int main()
{
	std::vector<double> vd;
	for(int i=0;i<10;i++){
		vd.emplace_back(rand_d());
	}
	for(auto const &v: vd) std::cout << v << ", ";
	std::cout << std::endl << std::is_sorted(vd.begin(), vd.end());
	std::cout << std::endl;
	std::sort(vd.begin(), vd.end()); // introsort Kombination aus Quick und Heapsort
	for(auto const &v: vd) std::cout << v << ", ";
	std::cout << std::endl << std::is_sorted(vd.begin(), vd.end());
}
```

## Sortieren mit Vergleichsfunktion
``` C++
#include <iostream>
#include <algorithm>
#include <vector>
class Rect final{
	double w_, h_;
	double area;
public:
	explicit Rect(double w, double h) : 
		w_{w}, h_{h}, area{w*h} {}
	double GetArea() const {
		return area;
	}
	// Vergleichsfunktion von Rect
	static bool VergleichAufsteigend(Rect const&a, Rect const&b){
		return a.area < b.area;
	}
	// Ausgabe der Rect
	friend std::ostream &operator<<(std::ostream &os, const Rect &rect) {
		os << "w_: " << rect.w_ << " h_: " <<
		rect.h_ << " area: " << rect.area;
		return os;
	}
};
int main(){
	std::vector<Rect> vs;
	vs.emplace_back(2., 5.);
	vs.emplace_back(2.1, 4.9);
	vs.emplace_back(1., 5.25);
	vs.emplace_back(6.3, 4.25);
	std::sort(vs.begin(), vs.end(), Rect::VergleichAufsteigend);
	for(auto const &v: vs) std::cout << v << std::endl;
}
```

## Sortieren mit Lambda Ausdruck
Siehe [[Lambda Ausdrücke]].
``` C++
#include <iostream>
#include <algorithm>
#include <vector>
class Rect final{
	double w_, h_;
	double area;
public:
	explicit Rect(double w, double h) : 
		w_{w}, h_{h}, area{w*h} {}
	double GetArea() const {
		return area;
	}
	// Ausgabe der Rect
	friend std::ostream &operator<<(std::ostream &os, const Rect &rect) {
		os << "w_: " << rect.w_ << " h_: " <<
		rect.h_ << " area: " << rect.area;
		return os;
	}
};
int main() {
	std::vector<Rect> vs;
	vs.emplace_back(2., 5.);
	vs.emplace_back(2.1, 4.9);
	vs.emplace_back(1., 5.25);
	vs.emplace_back(6.3, 4.25);
	bool aufsteigend {true};
	std::sort(vs.begin(), vs.end(), // Lambda Ausdruck
		[aufsteigend](Rect const &a, Rect const &b) -> bool { 
			if(aufsteigend) return a.GetArea() < b.GetArea();
			return a.GetArea() > b.GetArea();
	});
	for(auto const &v: vs) std::cout << v << std::endl;
}
```

## Sortieren mit Funktor
Siehe [[Funktoren]].
``` C++
#include <iostream>
#include <algorithm>
#include <vector>
class Rect final{
	double w_, h_;
	double area;
public:
	explicit Rect(double w, double h) : 
		w_{w}, h_{h}, area{w*h} {}
	double GetArea() const {
		return area;
	}
	// Ausgabe der Rect
	friend std::ostream &operator<<(std::ostream &os, const Rect &rect) {
		os << "w_: " << rect.w_ << " h_: " <<
		rect.h_ << " area: " << rect.area;
		return os;
	}
};
struct Compare{
	bool operator()(Rect const &a, Rect const &b){
		return a.GetArea() > b.GetArea();
	}
};
int main() {
	std::vector<Rect> vs;
	vs.emplace_back(2., 5.);
	vs.emplace_back(2.1, 4.9);
	vs.emplace_back(1., 5.25);
	vs.emplace_back(6.3, 4.25);
	// keine Instanz von Compare noetig, wird in std::sort erzeugt
	std::sort(vs.begin(), vs.end(),Compare());
	for(auto const &v: vs) std::cout << v << std::endl;
}
```


# utility

## std::swap
``` C++
#include <utility>
int main() {
	unique_ptr<int> ptr1 {5};
	unique_ptr<int> ptr2 {7};
	// Die beiden Pointer vertauschen
	std::swap(ptr1, ptr2);
}
```

## std::move
- macht aus einer [[Wertkategorien#^ee367c|lvalue]] eine [[Wertkategorien#^87baab|rvalue Referenz]].
- Ein Objekt wird verschoben statt kopiert.
``` C++
#include <utility>
#include <string>
#include <vector>
int main() {
	std::string str {"Salut"};
	std::vector<std::string> v;
	// by copy, str wird als rvalue kopiert und dann eingefügt
	v.push_back(str);
	// move, weniger teuer, str wird verschoben statt kopiert
	// der Inhalt von str ist jetzt in v. str gültig aber Inhalt weg 
	v.push_back(std::move(str));
}
```
