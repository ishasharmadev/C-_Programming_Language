## **🔥 C++ Interview Questions on Classes (Beginner → Advanced) — Chapter 16: Classes**  
(*Based on* **The C++ Programming Language (4th Edition) by Bjarne Stroustrup**)

---

## **🟢 Beginner-Level Questions**  

### **1️⃣ What is a class in C++?**
💬 **Question:** What is a class in C++ and why do we use it?  

✅ **Answer:**  
A **class** is a **user-defined data type** that encapsulates **data (attributes) and behavior (methods)** together. It follows the principles of **Object-Oriented Programming (OOP)**, promoting **encapsulation, reusability, and abstraction**.

**Example:**
```cpp
class Car {
    string brand;
    int speed;
public:
    void setBrand(string b) { brand = b; }
    void setSpeed(int s) { speed = s; }
};
```
**🔹 Why use classes?**
- **Encapsulation**: Data hiding
- **Code reusability**: Objects can be reused
- **Modularity**: Better code organization  

---

### **2️⃣ What is the difference between a class and an object?**
💬 **Question:** Explain the difference between a class and an object in C++.  

✅ **Answer:**  
- **Class** → A **blueprint/template** for creating objects.  
- **Object** → An **instance** of a class with actual values.  

**Example:**
```cpp
class Car {  // Class definition
    string brand;
public:
    void setBrand(string b) { brand = b; }
};

int main() {
    Car myCar;  // Object created
    myCar.setBrand("Tesla");
}
```

---

### **3️⃣ What is a constructor?**
💬 **Question:** What is a constructor in C++?  

✅ **Answer:**  
A **constructor** is a **special function** that gets called **automatically** when an object is created. It initializes the object’s attributes.

**Example:**
```cpp
class Car {
public:
    Car() { cout << "Car Created"; }  // Constructor
};

int main() {
    Car c;  // Constructor called automatically
}
```
✅ **Output:** `Car Created`

---

### **4️⃣ What is a destructor? When is it called?**
💬 **Question:** What is a destructor in C++?  

✅ **Answer:**  
A **destructor** (`~ClassName()`) is a special function that is **automatically called when an object goes out of scope**. It is used for **cleaning up resources** like dynamic memory, file handles, etc.

**Example:**
```cpp
class Car {
public:
    ~Car() { cout << "Car Destroyed"; }  // Destructor
};

int main() {
    Car c;  // Destructor is called automatically at the end of `main`
}
```
✅ **Output:** `Car Destroyed`

---

## **🟠 Intermediate-Level Questions**  

### **5️⃣ What is the difference between a constructor and a destructor?**
| Feature        | Constructor (`ClassName()`) | Destructor (`~ClassName()`) |
|---------------|-------------------|--------------------|
| **Purpose**   | Initializes object | Cleans up resources |
| **Called when?** | Object is created | Object is destroyed |
| **Can be overloaded?** | ✅ Yes | ❌ No |
| **Can take arguments?** | ✅ Yes | ❌ No |

---

### **6️⃣ What is a copy constructor?**
💬 **Question:** What is a copy constructor? How does it work?  

✅ **Answer:**  
A **copy constructor** creates a new object as an **exact copy** of another object.

**Example:**
```cpp
class Car {
    string brand;
public:
    Car(string b) { brand = b; }
    Car(const Car& c) { brand = c.brand; }  // Copy constructor
};
```
✅ **Usage:**
```cpp
Car car1("BMW");
Car car2 = car1;  // Calls copy constructor
```

---

### **7️⃣ What is a move constructor? (C++11)**
💬 **Question:** What is a move constructor and why is it useful?  

✅ **Answer:**  
A **move constructor** transfers resources from a temporary object **instead of copying**. It improves performance by avoiding unnecessary deep copies.

**Example:**
```cpp
class Car {
public:
    Car(Car&& c) { cout << "Move Constructor"; }  // Move constructor
};

Car tempCar() {
    return Car();
}

int main() {
    Car c = tempCar();  // Move constructor called
}
```
🚀 **Faster than a copy constructor for large objects!**

---

### **8️⃣ What is an explicit constructor?**
💬 **Question:** What is the `explicit` keyword in constructors?  

✅ **Answer:**  
An **explicit constructor** prevents **implicit conversions**, ensuring the constructor is only used when explicitly called.

**Example (Without `explicit` - Implicit Conversion Allowed)**:
```cpp
class Car {
public:
    Car(int speed) { cout << "Speed: " << speed; }
};

Car c = 100;  // Implicit conversion allowed
```
**Example (With `explicit` - Prevents Implicit Conversion)**:
```cpp
class Car {
public:
    explicit Car(int speed) { cout << "Speed: " << speed; }
};

Car c = 100;  // ❌ ERROR: Implicit conversion not allowed
Car c2(100);  // ✅ Allowed
```

---

## **🔴 Advanced-Level Questions**  

### **9️⃣ What is the difference between shallow copy and deep copy?**
💬 **Question:** What is the difference between a shallow copy and a deep copy?  

✅ **Answer:**  
| Type | Description | Example |
|------|------------|---------|
| **Shallow Copy** | Copies pointer addresses, but both objects share the same memory | `Car obj2 = obj1;` |
| **Deep Copy** | Creates a new copy of memory instead of sharing | Implement **custom copy constructor** |

---

### **🔟 What are friend functions in C++?**
💬 **Question:** What is a `friend` function and when should we use it?  

✅ **Answer:**  
A **friend function** can **access private members** of a class without being a member itself.

**Example:**
```cpp
class Car {
    int speed;
    friend void showSpeed(Car c);
};

void showSpeed(Car c) { cout << c.speed; }  // Access private member
```

---

### **1️⃣1️⃣ What is the difference between struct and class in C++?**
💬 **Question:** What is the difference between a `struct` and a `class` in C++?  

✅ **Answer:**  
| Feature | `struct` | `class` |
|---------|---------|--------|
| Default Access Modifier | `public` | `private` |
| Usage | Simple data structures | Encapsulated objects with OOP |

---

### **1️⃣2️⃣ How do nested classes work in C++?**
💬 **Question:** How do you create an object of a nested class in C++?  

✅ **Answer:**  
```cpp
class Outer {
public:
    class Inner {
    public:
        void show() { cout << "Inside Inner Class"; }
    };
};

int main() {
    Outer::Inner obj;  // Creating object of nested class
    obj.show();
}
```

---

## **🔴 Ultra-Advanced Question (Bonus 🔥)**
💬 **Question:** What are the **five special member functions** in C++?  

✅ **Answer:**  
1. **Default Constructor** `ClassName();`
2. **Destructor** `~ClassName();`
3. **Copy Constructor** `ClassName(const ClassName&);`
4. **Copy Assignment Operator** `ClassName& operator=(const ClassName&);`
5. **Move Constructor & Move Assignment Operator** (C++11)  

---

## **🚀 Final Thoughts**
This **interview Q&A** covers **beginner to advanced** topics from **Chapter 16: Classes** in Stroustrup’s book.  

