### **📖 Chapter 20: Derived Classes (C++ Programming Language, 4th Edition by Bjarne Stroustrup)**  

This chapter focuses on **inheritance in C++**, covering **base and derived classes**, **member access**, **constructors and destructors**, **polymorphism**, and **virtual functions**. Inheritance enables **code reuse**, **hierarchical relationships**, and **polymorphic behavior**.

---

## **🔷 20.1 Introduction to Derived Classes**  
### **📌 What It Covers:**  
- Explains the concept of **inheritance**—where a derived class **inherits members** from a base class.  
- Establishes an **is-a relationship** (e.g., "Dog is an Animal").  
- Demonstrates how derived classes **extend or modify** base class behavior.  

### **🛠️ Example: Basic Inheritance**
```cpp
class Animal {
public:
    void makeSound() { cout << "Some generic sound" << endl; }
};

class Dog : public Animal {  // Dog inherits from Animal
public:
    void bark() { cout << "Woof!" << endl; }
};

int main() {
    Dog d;
    d.makeSound();  // Inherited method
    d.bark();       // Derived class method
}
```
✅ **Dog has access to `makeSound()` from Animal!**  

---

## **🔷 20.2 Member Access in Derived Classes**  
### **📌 What It Covers:**  
- **Public, Protected, and Private** inheritance.  
- How access specifiers (`public`, `protected`, `private`) affect inheritance.  
- **Visibility rules:**  
  - `public` members of base class stay `public` in derived class.  
  - `protected` members remain `protected` in derived class.  
  - `private` members are **not accessible** in derived class.  

### **🛠️ Example: Access Specifiers**
```cpp
class Base {
private:
    int privateVar = 1;  // Not inherited
protected:
    int protectedVar = 2; // Inherited as protected
public:
    int publicVar = 3;    // Inherited as public
};

class Derived : public Base {
public:
    void show() {
        // privateVar = 1; ❌ Not accessible
        cout << protectedVar << endl; // ✅ Accessible
        cout << publicVar << endl;    // ✅ Accessible
    }
};
```
✅ **`protectedVar` and `publicVar` are accessible in `Derived`, but `privateVar` is not!**  

---

## **🔷 20.3 Constructors and Destructors in Derived Classes**  
### **📌 What It Covers:**  
- **How constructors of base and derived classes interact**.  
- **Order of constructor execution:**  
  - **Base class constructor runs first**, then the derived class constructor.  
- **Order of destructor execution:**  
  - **Derived class destructor runs first**, then the base class destructor.  

### **🛠️ Example: Constructor and Destructor Execution**
```cpp
class Base {
public:
    Base() { cout << "Base Constructor\n"; }
    ~Base() { cout << "Base Destructor\n"; }
};

class Derived : public Base {
public:
    Derived() { cout << "Derived Constructor\n"; }
    ~Derived() { cout << "Derived Destructor\n"; }
};

int main() {
    Derived d;
}
```
**🔹 Output:**  
```
Base Constructor  
Derived Constructor  
Derived Destructor  
Base Destructor  
```
✅ **Base class is constructed first and destructed last!**  

---

## **🔷 20.4 Virtual Functions and Polymorphism**  
### **📌 What It Covers:**  
- Introduces **dynamic (runtime) polymorphism**.  
- Uses `virtual` keyword to enable **function overriding** in derived classes.  
- Allows calling **derived class functions through base class pointers**.  

### **🛠️ Example: Virtual Functions**
```cpp
class Base {
public:
    virtual void show() { cout << "Base class show\n"; }
};

class Derived : public Base {
public:
    void show() override { cout << "Derived class show\n"; }
};

int main() {
    Base* b = new Derived();
    b->show();  // Calls Derived::show() due to virtual function
}
```
✅ **Even though `b` is a `Base*`, `Derived::show()` is called!**  

---

## **🔷 20.5 Abstract Classes and Pure Virtual Functions**  
### **📌 What It Covers:**  
- A **pure virtual function** (`= 0`) makes a class **abstract**.  
- **Abstract classes cannot be instantiated**.  
- Derived classes **must override** pure virtual functions.  

### **🛠️ Example: Abstract Class**
```cpp
class Shape {
public:
    virtual void draw() = 0;  // Pure virtual function
};

class Circle : public Shape {
public:
    void draw() override { cout << "Drawing Circle\n"; }
};

int main() {
    Shape* s = new Circle();
    s->draw();  // Calls Circle's draw()
}
```
✅ **`Shape` is an abstract class and cannot be instantiated!**  

---

## **🔷 20.6 Overriding and Hiding Base Class Members**  
### **📌 What It Covers:**  
- A derived class function **overrides** a base class function **only if it’s virtual**.  
- If it’s not virtual, the base class function is **hidden** instead of overridden.  

### **🛠️ Example: Function Hiding**
```cpp
class Base {
public:
    void show() { cout << "Base show\n"; }
};

class Derived : public Base {
public:
    void show() { cout << "Derived show\n"; }
};

int main() {
    Derived d;
    d.show();  // Calls Derived::show()
}
```
✅ **`Base::show()` is hidden, not overridden!**  

---

## **🔷 20.7 Multiple Inheritance**  
### **📌 What It Covers:**  
- A class can inherit from **multiple base classes**.  
- **Problem:** Ambiguity when two base classes have the same function name.  

### **🛠️ Example: Multiple Inheritance**
```cpp
class A {
public:
    void show() { cout << "A's show\n"; }
};

class B {
public:
    void show() { cout << "B's show\n"; }
};

class C : public A, public B {
public:
    void show() { cout << "C's show\n"; }
};

int main() {
    C c;
    c.show();  // Calls C's show
    // c.A::show();  // Use scope resolution to resolve ambiguity
}
```
✅ **Use `A::show()` or `B::show()` to specify which base class function to call!**  

---

## **🔷 20.8 Virtual Base Classes (Diamond Problem)**  
### **📌 What It Covers:**  
- **Diamond problem:** When multiple inheritance causes **duplicate base class instances**.  
- **Solution:** Use `virtual` base classes.  

### **🛠️ Example: Virtual Base Class**
```cpp
class A {
public:
    int x;
};

class B : virtual public A {};
class C : virtual public A {};
class D : public B, public C {};

int main() {
    D d;
    d.x = 10;  // No ambiguity because A is virtual
}
```
✅ **`x` is inherited only once due to `virtual` keyword!**  

---

## **🎯 Summary of Key Concepts**  
| Concept | Explanation |
|---------|------------|
| **Inheritance** | Derived classes inherit from base classes. |
| **Access Specifiers** | `public`, `protected`, `private` control member accessibility. |
| **Constructors & Destructors** | Base class constructor runs first, destructor runs last. |
| **Virtual Functions** | Enable polymorphism (dynamic method dispatch). |
| **Abstract Classes** | Contain pure virtual functions, cannot be instantiated. |
| **Multiple Inheritance** | A class can inherit from multiple base classes. |
| **Virtual Base Classes** | Solve the diamond problem in multiple inheritance. |

---

## **📌 Final Thoughts**
This chapter is **essential for object-oriented programming in C++**. 
