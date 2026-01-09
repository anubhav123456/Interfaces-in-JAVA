
---

## Polymorphism

### Interfaces can be used as Data Types

---

### Key Concept

An **interface can be used as a data type** in Java.
A **reference variable of an interface type** can point to **any object whose class implements that interface**.

This enables **runtime polymorphism**.

---

## Example Code

```java
interface Bird
{
    void fly();
}

class Hen implements Bird
{
    @Override
    public void fly()
    {
        System.out.println("Hen flies");
    }
}

class Eagle implements Bird
{
    @Override
    public void fly()
    {
        System.out.println("Eagle flies");
    }
}

public class Main
{
    public static void main(String[] args)
    {
        Bird b1 = new Hen();
        b1.fly();

        Bird b2 = new Eagle();
        b2.fly();
    }
}
```

---

## Output

```text
Hen flies
Eagle flies
```

---

## Explanation

### 1. Interface as Data Type

```java
Bird b1 = new Hen();
Bird b2 = new Eagle();
```

* `Bird` → **data type**
* `b1`, `b2` → **reference variables**
* `Hen`, `Eagle` → **different concrete classes (objects)**

---

### 2. IS-A Relationship

A class that **implements an interface** establishes an **IS-A relationship**.

* `Hen implements Bird` → **Hen IS-A Bird**
* `Eagle implements Bird` → **Eagle IS-A Bird**

Because of this relationship, an interface reference can point to implementing class objects.

---

## Runtime Polymorphism

### What happens at runtime?

1. **JVM checks the actual object** (Hen or Eagle)
2. **Finds the overridden method**
3. **Calls the correct implementation**

Example:

```java
Bird b1 = new Hen();
b1.fly();   // Calls Hen's fly()
```

```java
Bird b2 = new Eagle();
b2.fly();   // Calls Eagle's fly()
```

* ✔ Method call depends on **object**, not reference
* ✔ Achieved using **Dynamic Method Dispatch**

---

## JVM + Memory Perspective (Interview Plus ⭐)

1. Interface reference stores the **address of the object**
2. JVM uses **virtual method table (v-table)**
3. Correct method is resolved **at runtime**

This is why:

* Same reference (`Bird`)
* Different behavior (`Hen flies`, `Eagle flies`)

---

## Why Interfaces Can Be Used as Data Types

✔ A reference of an interface type can refer to **multiple implementations**
✔ Enables **polymorphism**
✔ Promotes **loose coupling**
✔ Improves **flexibility and maintainability**

---

## One-Line Interview Answer

> **Interfaces can be used as data types because a reference of an interface can point to any object whose class implements that interface, enabling runtime polymorphism through dynamic method dispatch.**

---

