- Musterimplementierungen von Lösungsansätzen spezieller wiederkehrender Problemstellungen

# Factory
- Pattern zur Erzeugung von Objekten

## Beispiel:
``` C++
#include <iostream>  
#include <memory>  
#include <vector>  
  
struct Car {  
    virtual void Drive() const = 0;  
};
struct Cabrio : public Car {  
    void Drive() const override {  
        std::cout << "Yeah, Cabrio ride!\n";  
    }  
};
struct Truck : public Car {  
    void Drive() const override {  
        std::cout << "Solid, Truck ride!\n";  
    }  
};
// Es existiert eine eigene Klasse, welche dafür zuständig ist die Objekte zu erstellen.
struct CarFactory {  
    CarFactory() = delete;  
  
    static std::unique_ptr<Car> Create(std::string const &type) {  
        if (type == "Cabrio") return std::make_unique<Cabrio>();  
        if (type == "Truck") return std::make_unique<Truck>();  
        return nullptr;  
    }  
};
int main() {  
    std::vector<std::unique_ptr<Car>> cars;  
    cars.push_back(CarFactory::Create("Truck"));  
    cars.push_back(CarFactory::Create("Cabrio"));  
    for (auto const &c: cars) c->Drive();  
}
```

# Singleton
- Nur eine Objektinstanz erlaubt
- Bspw. für Datenbankverbindungen, typischerweise nur eine Verbindung erlaubt

## Beispiel
``` C++
#include <iostream>
class Singleton {  
public:  
    static Singleton &GetInstance() {  
        static Singleton singleton; // es existiert nur eine statische Instanz der Klasse Singleton in Singleton  
        return singleton;  
    }
    void Fetch() { std::cout << "e.g. fetch data from db\n"; }
private:  
    // Kann nur innerhalb der Klasse erzeugt oder zerstört werden.  
    Singleton() { std::cout << "e.g. open db-connection\n"; }
    ~Singleton() { std::cout << "e.g. close db-connection\n"; }
    // Alle Copy und Move Konstruktoren/Operatoren werden gelöscht  
    Singleton(const Singleton &) = delete;
    Singleton &operator=(const Singleton &) = delete;
    Singleton(Singleton &&) = delete;
    Singleton &operator=(Singleton &&) = delete;  
};  
  
int main() {  
    Singleton &s1 = Singleton::GetInstance();  
    s1.Fetch();  
    Singleton &s2 = Singleton::GetInstance();  
    s2.Fetch();  
}
```

# Adapter
- Passt gegebene Klassen an neue Interfaceanforderungen an, ohne Vererbung anzuwenden.
- Gehört zur Gruppe der Strukturentwurfsmuster
- z.B. [[Standardcontainer#^cbeee3|std::queue]] oder std::stack.