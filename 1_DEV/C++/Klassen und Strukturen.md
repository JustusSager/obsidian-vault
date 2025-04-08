Klassen und Strukturen sind quasi das selbe in C++. Die Unterschiede sind weiter unten aufgelistet.
# Klassen
## Verschachtelte Klassen
``` C++
class Outer {
	int const x {42};
public:
	class Inner {
		int a {42};
	public:
		int GetAX(Outer const &o) {
			return a * o.x;
		}
	};
};
int main() {
	Outer o;
	Outer::Inner data;
	std::cout << data.GetAX(o) << std::endl;
	return 0;
}
```
Zugriff ist ähnlich zu [[Namensräume|Namensräumen]]. 

# Strukturen
## struct als Aggregat vs. Benutzerdefinierter Typ
kann auch für "struct" verwendet werden:
``` C++
// C Stil
typedef struct mytype1 {
	int a, b, c;
	float x, y, z;
}
// C++ Stil
using mytype2 = struct {
	int a, b, c;
	float x, y, z;
}
// Uniform initalizer list
mytype1 m1 {1, 2, 3, 4.f, 5.f, 6.f};
mytype2 m2 {1, 2, 3, 4.f, 5.f, 6.f};
// Designated initalizer list
// Reihenfolge dennoch relevant! b=0,,x=.0f, y=.0f
mytype2 m3 {.a = 1, .c = 3, .z = 1.0f};

// Zugriff mit . Operator
int s1 = m1.a + m1.b / m1.c;
int s2 = m2.a + m2.b / m2.c;
```

# Vorsicht bei Rückgabewerten
Wenn eine Methode eine Referenz oder Zeiger auf einen enthaltenen Wert zurückgibt, ist Vorsicht geboten.
``` C++
struct Example{
	Example m; // Memberwert
	// ok, by-value, copy-elision
	Example f1(){
		Example e; 
		return e;
	}
	// Definitiv nicht ok, weil nach dem scope der Funktion existiert e garnicht mehr!
	Example &f2(){
		Example e; 
		return e;
	}
	// Wahrscheinlich ok
	Example &f3(Example &in){
		return in;
	}
	// Vorsicht! Ok nur solange Objektinstanz existiert
	Example &f4(){
		return m;
	}
};
```

# Klasse vs. Struktur
- Standardmäßig ist die Zugriffsart bei einer Klasse "private". Bei einem "struct" ist sie standardmäßig "public".