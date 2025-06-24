Nur KFZ kennt seine inneren Werte und kann auf diese Zugreifen. Zugriff von außen ist verboten.
Der Zugriff auf die Daten soll soweit wie möglich beschränkt werden.
Der Datenzugriff erfolgt typischerweise über "Getter" und "Setter" Methoden.
	bedingt sinnvoll da es viel "boilerplate" Code erzeugt. Man könnte auch einfach die entsprechenden Variablen public machen.
	Erst wirklich sinnvoll bei der Verarbeitung der übergebenen Attribute.
	
Zugriffsspezifizierer ("public", "protected", "private") legen Zugriffsart fest. 
Standardmäßig ist die Zugriffsart bei einer Klasse "private". Bei einem "struct" ist sie standardmäßig "public".

``` C++
class MyClass1 {
	std::string name; // ist private
	public:
		void print();
	protected:
		int a;
}
```

## public
Ein Zugriff auf die Variablen und Methoden ist ...
- von außerhalb der Klasse möglich
- von erbenden Klassen möglich (Siehe [[OOP - 2 Vererbung]])
- innerhalb der eigenen Klasse möglich

## protected
Ein Zugriff auf die Variablen und Methoden ist ...
- nicht mehr von außerhalb der Klasse (ausgenommen erbende Klassen) möglich
- von erbenden Klassen möglich (Siehe [[OOP - 2 Vererbung]])
- innerhalb der eigenen Klasse möglich

## private
Ein Zugriff auf die Variablen und Methoden ist ...
- nicht mehr von außerhalb der Klasse (ausgenommen erbende Klassen) möglich.
- nicht mehr von den erbenden Klassen möglich.
- innerhalb der eigenen Klasse möglich.
