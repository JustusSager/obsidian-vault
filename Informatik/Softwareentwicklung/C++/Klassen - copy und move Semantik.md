Standardmäßig wird in einer Klasse zusätzlich zum leeren Konstruktor auch ein copy-Konstruktor, move-Konstruktor, Kopier-Zuweisungsoperator und Verschiebe-Zuweisungsoperator erstellt. 

## Kopier-Konstruktor ^264f73
- Es wird eine tiefe Kopie der Attribute einer [[Wertkategorien#^58c9e0|lvalue Referenz]] in ein neues Objekt geschrieben. 
- Die alten Werte bleiben dabei unverändert.
``` C++
A(A const &a) {  
    _nptr = std::make_unique<int>(*a._nptr);  
    _aptr = std::make_unique<std::array<int, 5>>();  
    for (int i{0}; i < _aptr->size(); i++) {  
        (*_aptr)[i] = (*a._aptr)[i];  
    }  
    std::cout << "class A copy constructor: " << *_nptr << std::endl;  
}
```

## Kopier-Zuweisungsoperator ^7570ab
- ähnlich dem [[#^264f73|Kopier-Konstruktor]], nur für die Zuweisung eines Objekts statt der Instanziierung.
- es kann auch ein default gesetzt werden
- (siehe [[Klassen - Operatoren überschreiben]])
``` C++
A&(A const &a) {  
    _nptr = std::make_unique<int>(*a._nptr);  
    _aptr = std::make_unique<std::array<int, 5>>();  
    for (int i{0}; i < _aptr->size(); i++) {  
        (*_aptr)[i] = (*a._aptr)[i];  
    }  
    std::cout << "class A copy constructor: " << *_nptr << std::endl;  
}
// default 
A& operator= (A& a) = default;
```


## Verschiebe-Konstruktor ^7043d0
- Teil der Verschiebesemantik
- Die Attribute einer [[Wertkategorien#^87baab|rvalue Referenz]] werden in das neue Objekt verschoben. 
- Die alten Werte werden dadurch ungültig.
	- Je nachdem müssen/sollten die Werte händisch ungültig gemacht werden.
``` C++
A(A &&rhs) : _nptr{std::move(rhs._nptr)} {}
```

## Verschiebe-Zuweisungsoperator ^711d64
- Teil der Verschiebesemantik
-  ähnlich dem [[#^7043d0|Verschiebe-Konstruktor]], nur für die Zuweisung eines Objekts statt der Instanziierung.
- Siehe dazu [[Wertkategorien]].
- (siehe [[Klassen - Operatoren überschreiben]])
``` C++
A &operator=(A &&rhs)  noexcept {  
    if (this == &rhs) return *this;
    this->_nptr = std::move(rhs._nptr);
    return *this;
}
```
