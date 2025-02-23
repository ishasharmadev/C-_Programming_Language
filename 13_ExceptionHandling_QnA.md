Sure! I'll ask **beginner** and **medium-level** questions about **C++ exception handling** and provide detailed answers.  

---

# **Beginner-Level Questions & Answers**

### **1. What is an exception in C++, and why do we use exception handling?**  
**Answer:**  
An **exception** is an error condition that disrupts the normal flow of execution. C++ provides **exception handling** to separate error-handling logic from regular code, making programs more readable and maintainable.  

Without exception handling, error handling relies on return codes, making code cluttered and harder to maintain. Exception handling ensures that errors are managed centrally and cleanly.

---

### **2. What are the three keywords used in C++ exception handling, and what are their roles?**  
**Answer:**  
The three main keywords are:  
- `try` – Defines a block of code where exceptions might be thrown.  
- `throw` – Generates (throws) an exception.  
- `catch` – Defines a block that handles the thrown exception.

Example:  
```cpp
try {
    throw std::runtime_error("An error occurred!");
} catch (const std::exception& e) {
    std::cout << "Caught exception: " << e.what() << '\n';
}
```
This catches and handles an exception of type `std::runtime_error`.

**Follow-up:** Can a `try` block exist without a `catch` block?  
**Answer:** Yes, but only if there’s a matching handler in a higher function in the call stack. Otherwise, `std::terminate()` is called.

---

### **3. Explain the syntax for throwing and catching an exception in C++.**  
**Answer:**  
To **throw** an exception:  
```cpp
throw std::runtime_error("Something went wrong!");
```
To **catch** an exception:  
```cpp
try {
    throw std::runtime_error("Error");
} catch (const std::runtime_error& e) {
    std::cout << "Caught: " << e.what() << '\n';
}
```
This catches `std::runtime_error` and prints the error message.

---

### **4. What happens if an exception is thrown but not caught?**  
**Answer:**  
If an exception is thrown and not caught, the program calls `std::terminate()`, which usually ends the program abruptly.

Example:
```cpp
void f() {
    throw std::runtime_error("Uncaught exception!");
}
int main() {
    f(); // No try-catch, program terminates
}
```
This program will terminate because there is no `catch` block.

---

### **5. Can we catch all exceptions using a single catch block? If yes, how?**  
**Answer:**  
Yes, we can catch all exceptions using `catch(...)`.  

Example:
```cpp
try {
    throw 42; // Throwing an int
} catch (...) {
    std::cout << "Caught an exception of unknown type.\n";
}
```
This will catch **any** exception, but the type cannot be determined.

**Follow-up:** What are the downsides of catching all exceptions this way?  
**Answer:** It prevents handling specific exceptions differently and makes debugging harder.

---

### **6. What is the base class of all standard exceptions in C++?**  
**Answer:**  
The base class for all standard exceptions is `std::exception`.

**Follow-up:** Name at least three derived classes and their use.  
**Answer:**  
1. `std::runtime_error` – Used for runtime errors (e.g., division by zero).  
2. `std::logic_error` – Used for logic errors (e.g., invalid arguments).  
3. `std::bad_alloc` – Thrown when `new` fails to allocate memory.

---

### **7. Explain the purpose of `std::exception::what()`.**  
**Answer:**  
`what()` is a virtual function in `std::exception` that returns a description of the error.

Example:
```cpp
try {
    throw std::runtime_error("File not found");
} catch (const std::exception& e) {
    std::cout << "Error: " << e.what() << '\n';
}
```
Output:  
```
Error: File not found
```

---

### **8. Can you throw an object of any type as an exception?**  
**Answer:**  
Yes, any type can be thrown as an exception.

Example:
```cpp
throw 5;   // Throwing an int
throw "Error";  // Throwing a string
throw std::runtime_error("Runtime error"); // Throwing a standard exception
```

**Follow-up:** Why is it recommended to throw objects derived from `std::exception`?  
**Answer:**  
Because they provide useful information via `what()`, improving debugging.

---

### **9. What is meant by "stack unwinding" in C++ exception handling?**  
**Answer:**  
When an exception is thrown, C++ **destroys local objects** as it moves up the call stack looking for a handler.

Example:
```cpp
struct X {
    ~X() { std::cout << "X destroyed\n"; }
};
void f() {
    X x;
    throw std::runtime_error("Error");
} // x is destroyed before exiting f()
```
Output:
```
X destroyed
```

---

### **10. What is RAII (Resource Acquisition Is Initialization) and how does it help with exceptions?**  
**Answer:**  
RAII ensures that resources are released when objects go out of scope, preventing leaks.

Example:
```cpp
class FileHandler {
    std::ofstream file;
public:
    FileHandler(const std::string& filename) { file.open(filename); }
    ~FileHandler() { file.close(); } // Ensures cleanup
};
```
Even if an exception occurs, the destructor closes the file automatically.

---

# **Medium-Level Questions & Answers**

### **11. What is meant by "exception safety," and what are the three levels of exception safety guarantees?**  
**Answer:**  
Exception safety means ensuring a program remains in a valid state when exceptions occur. The three levels are:

1. **Basic Guarantee** – No resource leaks, but program state may be inconsistent.
2. **Strong Guarantee** – Either operation completes successfully or has no effect.
3. **No-Throw Guarantee** – The operation is guaranteed to never throw.

Example:
- `std::vector::push_back()` provides the **basic guarantee** (may leave vector in inconsistent state if allocation fails).
- `std::swap()` provides the **strong guarantee** (either swaps successfully or nothing changes).

---

### **12. What is the difference between `throw;` and `throw e;` inside a `catch` block?**  
**Answer:**  
- `throw;` **rethrows** the current exception **without modifying it**.
- `throw e;` **creates a copy** of `e` and throws a new exception.

Example:
```cpp
try {
    throw std::runtime_error("Original");
} catch (const std::exception& e) {
    throw; // Preserves original exception
}
```
`throw;` preserves the original exception type and stack trace.

---

### **13. How does `noexcept` affect exception handling in C++?**  
**Answer:**  
`noexcept` specifies that a function does not throw exceptions.

Example:
```cpp
void f() noexcept { /* No exceptions allowed */ }
```
If an exception is thrown inside `f()`, `std::terminate()` is called.

---

### **14. How can smart pointers (`std::unique_ptr` and `std::shared_ptr`) help with exception safety?**  
**Answer:**  
They automatically manage memory, preventing leaks when exceptions occur.

Example:
```cpp
std::unique_ptr<int> ptr(new int(10)); // Auto-deletes if exception occurs
```

---

### **15. Why is catching exceptions by reference recommended?**  
**Answer:**  
Catching by reference (`catch (const std::exception& e)`) prevents object slicing and avoids unnecessary copies.

---

That covers **beginner** and **medium** levels! Want to try answering some **advanced** questions next? 😊
