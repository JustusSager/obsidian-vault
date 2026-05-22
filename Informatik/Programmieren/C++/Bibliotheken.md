#Informatik 
# Konsolen Ein-/Ausgabe
## std::iostream
https://cplusplus.com/reference/istream/iostream/
Verwendet Streams zur Zeichenübertragung. Ein Stream empfängt oder erzeugt "Zeichenstrom".
### Verwendung
#### Konsolenausgabe
#TODO std::cerr
``` C++
#include<iostream>
int main() {
	// Konsolenausgabe
	std::cout << "Hello World!" << std::endl;
	// Mit "<<" wird der string "Hello World!" in das Streamobjekt std::cout hineingeschoben. 
	
	// ebenfalls Konsolenausgabe, aber irgendwas ist anders.
	std::cerr << "Hello World!" << std::endl;
	return 0;
}
```

"<<" erlaubt alle Standard Datentypen und "std::string", lässt sich jedoch auch als Operator in eigene Datentypen integrieren. Siehe dazu #TODO.
Analog dazu, lässt sich mit dem ">>" Operator das einlesen von Streams realisieren.

#### Konsoleneingabe
Analog zum "<<" Operator lässt sich mit dem ">>" Operator das einlesen von Streams realisieren.
``` C++
#include <iostream>
#include <string>
using DataType = struct { 
	std::string name, plz_ort;
};
int main(){
	DataType person {"", ""};
	// Einlesen bis naechstes Whitespace
	std::cout << "Name: ";
	std::cin >> person.name;
	std::cout << "Plz und Ort: ";
	// Auslesen aller evtl. noch vorh. Whitespaces (also Eingabefeld bereinigen)
	std::cin >> std::ws;
	// Einlesen bis Newline
	std::getline(std::cin, person.plz_ort);
	// Ausgabe der Daten
	std::cout << "Name: " << person.name << std::endl;
	std::cout << "Plz und Ort: " << person.plz_ort << std::endl;
	return 0;
}
```

### Vergleich mit stdio von C
``` C
#include<stdio>
double x = 4.4373746483
printf("Hallo Welt!\n%.4f", x);
```

## std::iomanip
Konsolenausgabe formatieren. Aber die alte Variante, ab C++ 20 kann man häufig (je nach Compiler) [[#std format|format]] nutzen.

### Verwendung
``` C++
#include <iostream>
#include <iomanip>
using std::cout; // sorgt dafür, dass man cout, statt std::cout schreiben kann.
int main(){
	// Punktschreibweise nicht wissenschaftlich
	cout << std::fixed
	<< std::setprecision(15); // 15 Nachkommastellen
	cout << 0.5 << "\n"; // Ausgabe 0.500000000000000
	cout << std::setprecision(5); // 5 Nachkommastellen
	cout << 0.25 << "\n"; // Ausgabe 0.25000
	return 0;
}
```
"std::endl" erzeugt ein "\n" und 'flusht' den Ausgabepuffer (also setzt die Ausgabe zurück).
"std::flush" 'flusht' nur den Ausgabebuffer.
## std::format
Ab C++ 20 kann man std::format benutzen um Ausgaben zu formatieren. Bei älteren Versionen kann man [[#std iomanip|iomanip]] verwenden.
Nicht jeder Compiler kennt "std::format", je nach Compiler muss auch bei C++ 20 und neuer [[#std iomanip|iomanip]] verwendet werden.
### Verwendung
``` C++
#include <format>
int main() {
	double x {22.123456};
	std::cout << std::format("{:.2f}\n", x);
	return 0;
}
```
# Standardcontainer
- https://en.cppreference.com/w/cpp/container
- Bei diesen Containern werden Templates zur Typisierung des Inhalts verwendet. Siehe dazu #TODO Templates
## Strings (std::string)
https://cplusplus.com/reference/string/string/
Nicht Verwechseln mit "cstring" aus der C-Programmiersprache.
Ist eine spezielle Implementierung von "std::basic_string". Hier lässt sich nicht auf ein anderes Codierungsformat der Buchstaben wechseln.
### Verwendung
``` C++
#include<iostream>
#include<string>
int main() {
	// Strings erzeugen
	std::string str1 {"Hallo"};
	std::string str2 {"Welt!"};
	
	// Strings aneinanderhängen
	std::string str3 = str1 + " " + str2;
	
	// Ausgabe
	std::cout << str3 << std::endl;
	
	// Erste Instanz einer Zeichenfolge finden.
	// size_type ist quasi ein int aber ermöglicht bessere Platformübergreifende kompatibilität
	std::string:size_type pos = str3.find(" ");
	
	// Substring erzeugen
	str1 = str3.substr(pos + 1);
	
	// Elementzugriff über Index
	std::cout << str1[0] << std::endl;
	return 0;
}
```

### Typkonvertierung
``` C++
#include <string>  
int main() {  
    std::string s1 {"1234"};  
    int i = std::stoi(s1);  
    std::string s2 {"1234.567"};  
    double d = std::stod(s2);  
    std::string s3 {"1234.567"};  
    float f = std::stof(s3);  
    std::cout << i << " " << d << " " << f << std::endl;  
}
```
### Vergleich mit C-Strings
C-Strings sind einfach nur char-Arrays, auf die über Pointer zugegriffen wird. Es gibt hierbei keine dynamische Länge und die Verarbeitung ist unhandlich.
Die C++-Strings sind eine eigene Klasse mit eigenen Methoden die das manipulieren der strings erleichtern. Es gibt eine dynamische Speicherverwaltung, die es erlaubt, dass die Länge des Strings nicht zur Compile-Zeit bereits bekannt sein muss.


## Smarte Pointer (std::memory)
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

##### Beispiel mit vector
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

#### Verwendung
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

## Sequentielle Container
### std::array
- https://cplusplus.com/reference/array/array/ 
- Lineares Array Aggregat
- statische Speicherverwaltung, d.h. die Größe eines Array kann während der Laufzeit nicht geändert werden.
- liefert einen [[Iteratoren#Random Access Iterator|Random Access Iterator]].
#### Verwendung
``` C++
#include<array>
int main(){
	// Array erstellen
	std::array<int, 5> sa {0, 1, 2, 3, 4};
	std::array<int, 5> sb {sa}; // value copy
	
	// Elementzugriff
	sa[2] = 55;
	return 0;
}
```
#### Im Vergleich zum C-Array
``` C++
#include<array>
int main(){
	// C-Array, statisch, d.h. Groesse bekannt zur Compilezeit!
	int ca[5] {0, 1, 2, 3, 4};
	// int cb[5] {ca}; -> geht nicht!
	
	// std::array, statisch, d.h. Groesse muss zur Compilezeit bekannt sein!
	std::array<int, 5> sa {0, 1, 2, 3, 4};
	std::array<int, 5> sb {sa}; // value copy
	// Elementzugriff
	sa[2] = 55;
	return 0;
}
```
### std::vector
- https://cplusplus.com/reference/vector/vector/
- Lineare Datenstruktur 
- dynamischer Speicherverwaltung, d.h. hierbei wird der Speicher automatisch verwaltet, es ist keine manuelle Allokation nötig. 
- liefert einen [[Iteratoren#Random Access Iterator|Random Access Iterator]].
#### Verwendung
``` C++
#include<vector>
int main() {
	// vector aus ints erstellen
	std::vector<int> v1 {1, 2, 3};
	// Anzahl der Elemente ausgeben
	v1.size();
	// Echte Größe das vectors
	v1.capacity();
	// Ein Element wird "in place" hinten hinzugefügt, es wird keine Kopie erzeugt. Wichtig für unique_ptr.
	v1.emplace_back(4);
	// Ein Element wird "by copy" hinten hinzugefügt
	v1.push_back(5);
	// Das letzte Element löschen
	v1.pop_back();
	// auf echte Größe reduzieren
	v1.shrink_to_fit();
	// Zugriff
	int x = v1[0];
	return 0;
}
```
### std::deque
- https://cplusplus.com/reference/deque/deque/
- Double Ended Queue
- schnelles Einfügen / Lesen / Löschen an beiden Enden der Queue
- Kann (in Blöcken) fragmentiert auf dem Speicher liegen.
- liefert einen [[Iteratoren#Random Access Iterator|Random Access Iterator]].
#### Verwendung
``` C++
#include <iostream>
#include <deque>
int main(){
	std::deque<int> di {1, 2, 3, 4, 5};
	di.pop_back();
	for(auto const &v: di){
		std::cout << v << std::endl;
	}
	di.pop_front();
	for(auto const &v: di){
		std::cout << v << std::endl;
	}
}
```
### std::list
- https://cplusplus.com/reference/list/list/
- Doppelt verkettete Liste
- einfügen, löschen, teilen meist ressourcenintensiver zum vector.
- liegt fragmentiert im Speicher.
- liefert einen [[Iteratoren#Bidirectional Iterator|Bidirectional Iterator]].
### std::forward_list
- https://cplusplus.com/reference/forward_list/forward_list/
- Einfach verkettete Liste
- weniger Speicherbedürftig als list, aber hat auch weniger features.
- kann Fragmentiert im Speicher liegen.
- liefert einen [[Iteratoren#Forward Iterator|Forward Iterator]].
## Assoziative Container
### std::map
- https://cplusplus.com/reference/map/map/
- Assoziativer Container
#### Verwendung
``` C++
#include <iostream>
#include <map>
int main(){
	std::map<std::string, std::string> mymap;
	mymap.emplace("one", "eins");
	mymap.emplace("two", "zwei");
	mymap["three"] = "drei";
	std::cout << mymap["one"] << std::endl;
	std::cout << mymap["two"] << std::endl;
	std::cout << mymap["three"] << std::endl;
	for(auto const &v: mymap){
		std::cout << v.first << " " << v.second << std::endl;
	}
}
```
## Container adaptors
- Liefern ein anderes Interface für einen darunterliegenden sequentiellen Container.
### std::queue
- https://cplusplus.com/reference/queue/queue/
- Queue. 
- Achtung, nicht threadsicher!
- Standardmäßig wird [[#std deque]] darunterliegend verwendet.
#### Verwendung
``` C++
#include <iostream>
#include <queue>
struct QElement{
	QElement(std::string const &s) : word{s}{}
	std::string word;
};
int main(){
	std::queue<QElement> q;
	// produce
	q.emplace("Hallo");
	q.emplace("schoene");
	q.emplace("Welt!");
	// consume
	do{
		std::cout << q.front().word << std::endl;
		q.pop();
	} while(!q.empty());
}
```
# Standardalgorithmen
## std::algorithm
Enthält typische Standardalgorithmen wie Suchen, Zählen, Sortieren, etc. für Daten-Container (siehe dazu z.B. [[#Standardcontainer]]). Dabei werden [[Iteratoren]] verwendet um auf der Datenmenge zu arbeiten.
Nicht jeder Algorithmus ist auf jeden Container anwendbar.

### Sortieren 
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

### Sortieren mit Vergleichsfunktion
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

### Sortieren mit Lambda Ausdruck
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

### Sortieren mit Funktor
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
## utility
### std::swap
``` C++
#include <utility>
int main() {
	unique_ptr<int> ptr1 {5};
	unique_ptr<int> ptr2 {7};
	// Die beiden Pointer vertauschen
	std::swap(ptr1, ptr2);
}
```
### std::move
- macht aus einer [[Wertkategorien#lvalue|lvalue]] eine [[Wertkategorien#lvalue Referenz|rvalue Referenz]].
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
# Einlesen von Dateien
## std::fstream
Lesen und schreiben einer Datei.
"ifstream" -> Lesen aus einer Datei.
"ofstream" -> schreiben in eine Datei.
"fstream" -> Lesen und Schreiben aus/in eine Datei.
### Verwendung
``` C++
#include <iostream>
#include <fstream>
int main() {
	{ // Automatisches öffnen und schließen mit Scope
		std::ofstream raus {"data.txt"}; 
		raus << "42\n"; // schreibt in die Datei
	}
	{
		std::ifstream rein {"data.txt"};
		int i;
		rein >> i; // ließt aus der Datei
		cout << i;
	}
	// Zugriff lesend und schreibend als Binärdatei.
	std::fstream wf {"data.txt", ios::in | ios::out | ios::binary}
	char c;
	wf.read(&c, 1); // lesen
	std::cout << std::hex << static_cast<int>(c) << std::endl;
	
	c = 'b';
	wf.write(&c, 1); // c in wf schreiben (append)
	wf.close(); // Explizit schließen
	return 0;
}
```
### Flags / Exception
Flags (Exceptions) können aktiviert werden mit:
``` C++
std::ifstream filestream(file_path);  
filestream.exceptions(std::ifstream::eofbit); // Bit für End-of-File
filestream.exceptions(std::ifstream::failbit); // Bit für Fail
filestream.exceptions(std::ifstream::badbit); // Bit für Bad

filestream.exceptions(std::ifstream::eofbit | std::ifstream::failbit | std::ifstream::badbit); # Inline
```
- End-of-File (EOF)
	- Wird gesetzt, wenn File zu Ende
- Fail
	- Wird immer gesetzt wenn lesen fehlgeschlagen.
	- auch bei EOF.
- Bad
	- Externer Fehler?
#### Verwendung
``` C++
try {
    int counter{0};
    filestream.open(file_path);  
    while (!filestream.eof()) {  
        std::getline(filestream, line);
        // Verarbeitung von line
        counter++;  
    }  
    filestream.close();  
} catch (std::ifstream::failure const &e) {  
    if (filestream.eof()) { # Kontrolle ob Fail vom EOF kommt
        // std::cerr << "EOF Bit: " << filestream.eof() << std::endl;  
    } else {  // sonst exception ausgeben
        std::cerr << e.what() << std::endl;  
    }  
}
```
# Exception
## std::exception
**Hinweis:**
- reduziert die Performance!
### Verwendung
``` C++
#include <exception>  
#include <iostream>  
#include <fstream>  
int main() {  
    std::ifstream file {};  
    try {  
       // Exceptions sind bei ifstream standardmäßig aus Performancegründen abgeschaltet, diese müssen erst aktiviert werden.  
       file.exceptions(std::ifstream::failbit | std::ifstream::badbit);  
       // Nicht existierende Datei einlesen führt zu Fehler.  
       file.open("testfile.txt");  
       file.close();  
    } catch (std::exception &e) {  
        std::cerr << e.what() << std::endl;  
    }  
    return 0;  
}
```
### Vergleich mit C
``` C
#include <stdlib>
int main() {
	if(f() == -1) handle_error(); // Variante 1
	assert(true) // Variante 2
	return 0;
}

int f() {
	if(true) { // fehler entsteht
		exit(-1);
	}
	return 0;
}

```
## std::stdexcept
Erweitert das Basismodul [[#std exception]] um verschiedene häufig vorkommende Exception Module.
### Verwendung
``` C++
#include <exception> // exceptions
#include <stdexcept> // Exceptions aus der Standardbib.
#include <iostream>
int main(int argv, char** args) {
    try {  
	    std::cout << argv << std::endl;
	    // Mit "throw" lässt sich eine bestimmte Exception auslösen
	    if(argv != 3) throw std::invalid_argument("Wrong number of args!");
    } catch (std::exception &e) {  
        std::cerr << e.what() << std::endl;
        // "throw" im catch Blöck würde dazu führen, dass die Exception an den nächst höheren Block "weitergegeben" wird.
    }  
    return 0;  
}
```
# Datum und Uhrzeit
## std::ctime 
#TODO ctime
## std::chrono 
#TODO chrono
# Weitere
## std::complex 
https://cplusplus.com/reference/complex/complex/
#TODO std::complex für irgendwann
Komplexe Zahlen
``` C++
#include<complex>
```
## Module der Boost Bibliothek
- Ist eine Vorstufe der Standardbibliothek
	- Viele des Standardbibliotheken waren vorher teil der Boost Bibliothek
- #TODO Boost Bibliothek mal anschauen
- www.boost.org 
## Simple and Fast Multimedia Lib (SFML)
## itk
- https://itk.org/
