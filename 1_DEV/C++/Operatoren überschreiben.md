```c++
class A {
	A &operator=(A const &rhs) {  
	    if (this != &rhs) return *this;
	    
	}
}
```