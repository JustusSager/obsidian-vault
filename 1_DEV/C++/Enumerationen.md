- Ähnlich zum Aufzählungstyp enum aus C
- C enum ist ohne scope, bei C++ ist enum Klasse mit scope, d.h. enum ist Teil einer Klasse (bzw. eines structs)
- C++ enum class == C++ enum struct
- C++ enum erlaubt keine Vererbung

# Verwendung
enum wird definiert mit "Platzhalternamen" für dahinterliegenden Wert.
``` C++
enum class State : short {RELEASED, PRESSED, _LENGTH};
enum struct StateMouse {RELEASED, PRESSED}; // wird standardmäßig zum Typ int
// Namen dürfen mehrfach vergeben werden, da sie an class/struct name gebunden sind.
int main() {
	State s1 {State::RELEASED};
	int nStates {static_cast<int>(State::_LENGTH)} // muss explizit gecasted werden
	StateMouse s2 {s1}; // geht implizit weil short < int
	s2 = StateMouse::PRESSED;
	switch(s2){ // für switch-case sind enums empfohlen
		case StateMouse::RELEASED:
			// do something
			break;
		case StateMouse::PRESSED:
			// do something else
			break;
	}
	int 
	
}
```

Standardmäßig wird zählt ein enum von 0 beginnend hoch. Es lassen sich jedoch auch händisch Werte angeben:
``` C++
enum class State : short {RELEASED = 0, PRESSED = 1, _LENGTH = 2};
enum class Color : char {RED = 'r', GREEN = 'g', BLUE = 'b'};
```

# Vergleich C-Stil
``` C++
#include <iostream>

enum Color : char{RED, GREEN, BLUE, _LENGTH}
// nicht erlaubt wäre bei C dann:
// enum ColorRGB : char{RED, GREEN, BLUE}
// da die Bezeichner RED, GREEN, BLUE bereits vergeben sind.
int main() {
	Color c {RED};
	int nColors {_LENGTH}; // Menge an enums implizit gecastet
}
```
