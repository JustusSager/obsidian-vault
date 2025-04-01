Siehe außerdem [[Schlüsselwörter in C++]], [[Enumerationen]], [[Lambda Ausdrücke]].

# Verschachtelte Klassen
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
Zugriff ist ähnlich zu [[Video 1 Modularisierung#^e9da44|Namensräumen]]. 
