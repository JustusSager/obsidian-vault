```c++
class A {
	int level {5};
	// Zuweisungsoperator
	A &operator=(A const &rhs) {  
	    if (this != &rhs) return *this;
	    // Was soll passieren bei einer Zuweisung
	}
	// Multiplikation mit double
	A &operator*(double const &rhs){
		//
	}
	// Linksshiftoperator
	friend void std::ostream &operator<<(std::ostream &os, A const &a)
}
void std::ostream &operator<<(std::ostream &os, A const &a) {
	os << "level: " << a.level << std::endl;
	return os;
};
```
