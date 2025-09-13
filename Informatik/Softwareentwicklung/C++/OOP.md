# Grundideen der OOP
Eine Klasse lässt sich sowohl mit "class" als auch mit "struct" realisieren.

Die Grundideen von OOP lassen sich aufteilen in folgende vier Punke:
1. Abstraktion
	1. Abstraktes KFZ -> PKW -> Sport PKW -> Sport Cabrio PKW
2. [[OOP - 2 Vererbung|Vererbung]]
3. [[OOP - 3 Kapselung|Kapselung]]
4. [[OOP - 4 Polymorphismus|Polymorphismus (Vielgestaltigkeit)]]

# RAII
(Resource Acquisition Is Initialisation)
- Anforderung einer Resource = Initialisierung einer Resource
- Initialisierung durch [[Klassen#^6cee62|ctor]]
- Löschen der Ressourcen durch [[Klassen#^cf0bc4|dtor]] 
- Richtig angewendetes RAII extrem wichtig für die Vermeidung von Speicherleaks!
- Eigener dtor nicht nötig wenn Klasse nur ...
	- 'Werte' d.h. keinen dynamisch mit new/delete verwalteten Speicher nutzt
	- Container wie bspw. [[Standardcontainer#^3232b4|std::vector]] aus der Standardbibliothek nutzt, da diese bereits selbst Acquise und Freigabe des dynamischen Speichers verwalten

# Rule of three/five/zero
Best Practice bezüglich der Implementierung bestimmter Methoden in Klassen.
## Rule of three
- Eher aus der Zeit vor C++ 11
- Wenn eine der folgenden Methoden implementiert werden muss, sollten alle implementiert werden bzw. explizit unnutzbar gemacht werden (=delete)
	- [[Klassen#^cf0bc4|Destruktor]] 
	- [[Klassen - copy und move Semantik#^264f73|Kopier-Konstruktor]] 
	- [[Klassen - copy und move Semantik#^7570ab|Kopier-Zuweisungsoperator]] 

## Rule of Five ^42ba48
- Erweiterung der Rule of three ab C++ 11
- manchmal auch "Big five" genannt.
- Wenn eine der folgenden Methoden implementiert werden muss, sollten alle implementiert werden bzw. explizit unnutzbar gemacht werden (=delete)
	- [[Klassen#^cf0bc4|Destruktor]] 
	- [[Klassen - copy und move Semantik#^264f73|Kopier-Konstruktor]] 
	- [[Klassen - copy und move Semantik#^7570ab|Kopier-Zuweisungsoperator]] 
	- [[Klassen - copy und move Semantik#^7043d0|Verschiebe-Konstruktor]] 
	- [[Klassen - copy und move Semantik#^711d64|Verschiebe-Zuweisungsoperator]] 

## Rule of zero
Wenn möglich sollten keine speziellen Destruktoren, Kopier-, Verschiebe-Konstruktoren, Kopier- und Verschiebe-Zuweisungsoperatoren verwendet werden. Aber sobald eins nötig ist, z.B. der Destruktor zur Speicherfreigabe, sollten alle Implementiert werden.