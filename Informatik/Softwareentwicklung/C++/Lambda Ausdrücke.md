#Informatik 
- Neu seit C++ 11
- Namenlose Funktionen

``` C++
#include <cstdio>
int main(){
	int a {42}, b{55};
	// Lambda funktion mit direktem Aufruf
	int c = [&a, b](int x) -> int { 
		a = a+b; 
		return a+x;
	}(22);
	// Lambda Funktion welche über den "namen" Aufgerufen wird.
	auto f = [](int i, int j, int k){
		printf("a: %d, b: %d, c: %d", i, j, k);
	};
	f(a, b, c);
}
```
In den ersten eckigen Klammern kann der scope der Funktion erweitert werden.