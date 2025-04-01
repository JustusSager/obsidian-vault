Siehe [[OOP]], [[Speicherverwaltung]], [[Compiler, Compilersystem und co.]].

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

