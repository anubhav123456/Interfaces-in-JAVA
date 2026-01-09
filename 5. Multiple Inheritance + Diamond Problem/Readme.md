
---

## Multiple Inheritance in Java (via Interface)

### ❌ Why Java Does NOT Allow Multiple Inheritance with Classes

Java **does not support multiple inheritance using classes** to avoid the **Diamond Problem**.

### 🔻 Diamond Problem

When two parent classes have the **same method**, the compiler cannot decide **which one to inherit**.

### Example (NOT Allowed)

```java
class WaterAnimal {
    void canBreathe() {
        System.out.println("Breathing in water");
    }
}

class LandAnimal {
    void canBreathe() {
        System.out.println("Breathing on land");
    }
}

// ❌ Compile-time error
class Crocodile extends WaterAnimal, LandAnimal {
}
```

### ❌ Problem:

* Both parent classes have `canBreathe()`
* Compiler confusion:

  > Which `canBreathe()` should Crocodile inherit?

---

## ✔ Solution: Multiple Inheritance Using Interfaces

Java **allows multiple inheritance using interfaces** because:

* Interfaces contain **method declarations**, not implementations (till Java 7)
* Even with default methods (Java 8+), ambiguity is explicitly handled

---

## ✔ Multiple Inheritance with Interfaces (Allowed)

### Interface Definitions

```java
interface WaterAnimal {
    boolean canBreathe();
}

interface LandAnimal {
    boolean canBreathe();
}
```

### Implementing Multiple Interfaces

```java
class Crocodile implements WaterAnimal, LandAnimal {

    @Override
    public boolean canBreathe() {
        return true;
    }
}
```

---

## ✔ Why There Is NO Ambiguity Here?

* Interfaces **do not provide implementation**
* `Crocodile` **must override** the method
* Compiler knows **exactly which method is executed**

---

## ✔ Key Points to Remember (Interview Gold ⭐)

* Java ❌ **does not support multiple inheritance using classes**
* Java ✔ **supports multiple inheritance using interfaces**
* Diamond Problem occurs when:

  * Same method exists in multiple parent classes
* Interfaces avoid ambiguity because:

  * No method implementation (pre-Java 8)
  * Child class provides the implementation
* If multiple interfaces have the same method:

  * Child class **must override it**

---

## 📝 One-Line Summary

> Java avoids multiple inheritance ambiguity by allowing it only through interfaces, where the implementing class provides the method implementation.

---
