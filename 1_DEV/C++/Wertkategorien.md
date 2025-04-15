# lvalue ^ee367c
- Benutzt identifizierbaren Speicherbereich
- auch left-hand-side-value oder locator value genannt
- sind nie rvalue
``` C++
a = 55; // a ist lvalue
```

# rvalue ^4dff75
- Temporäre Objekte
- kein identifizierbarer Speicherbereich
- auch right-hand-side-value genannt
- Funktions-Rückgabewerte sind auch rvalue
``` C++
a = 55; // 55 ist rvalue -> literal
vector.push_back(C{}) // C{} ist rvalue und temporär
```

# lvalue Referenz ^58c9e0
- lvalue Referenzen sind "normale" Referenzen
- Objekt darf nicht "geklaut" (d.h. verschoben) werden.

# rvalue Referenz ^87baab
- rvalue Referenzen sind Referenzen auf temporäre Werte 
- Eingeleitet mit "&&"
- Vergrößert die Lebenszeit eines temporären Werts
- Wert hinter einer rvalue Referenz darf “geklaut” (d.h. verschoben) werden, da Wert dahinter temporär, Zustand danach unspezifiziert

# Beispiel
``` C++
int f(){
	int a{42+1}; return a;
}
int main() {
	std::string s1 {"Test"}; // s1 ist lvalue
	std::string& x {s1}; // Referenz vom Typ String die auf den Wert von s1 referenziert. -> lvalue Referenz
	// error: can't bind to lvalue
	// std::string&& r1 {s1};
	// okay: lvalue reference to const extends lifetime
	const std::string& r2 {s1 + s1};
	// error: can't modify through reference to const
	// r2 += "Test";
	// okay: rvalue reference extends lifetime
	std::string&& r3 = s1 + s1;
	r3 += "Test";
	// okay: can modify through reference to non-const
	std::cout << r3 << '\n';
	// error: can't bind to rvalue
	//int &lvref = f();
	// okay: lvalue reference to const extends lifetime
	int const &clvref = f();
	// okay: rvalue reference extends lifetime
	int &&rvref = f();
	std::cout << rvref << std::endl;
}
```