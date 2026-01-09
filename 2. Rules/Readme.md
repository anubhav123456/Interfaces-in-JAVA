# Rules of an Interface 

### 1. Methods are `public` and `abstract` by default

* All methods declared inside an interface are **implicitly `public` and `abstract`**.
* You do **not** need to explicitly write `public abstract`.

```java
interface LivingBeing
{
    void eat(); // public abstract by default
}
```

---

### 2. Allowed access modifiers

* Only **`public`** and **default (no modifier)** are allowed for interface methods.

✔ Allowed:

```java
void eat();
public void eat();
```

---

### 3. ❌ `private` and `protected` are NOT allowed (pre-Java 9 context)

* You cannot use `private` or `protected` for abstract methods in interfaces.

❌ Not allowed:

```java
private void eat();
protected void eat();
```

> Note: From **Java 9**, private methods are allowed **only as helper methods**, not abstract ones.

---

### 4. An interface can extend multiple interfaces

* Java supports **multiple inheritance using interfaces**.
* An interface can extend **more than one interface** using `extends`.

```java
interface LivingBeing
{
    void eat();
}

interface Animal
{
    void move();
}

interface Bird extends LivingBeing, Animal
{
    void fly();
}
```

---

### 5. ❌ An interface cannot extend a class

* Interfaces can **only extend other interfaces**.
* They **cannot extend classes**.

❌ Not allowed:

```java
interface Bird extends SomeClass {}
```

---

## Implementing an Interface

* A class uses the `implements` keyword to implement an interface.
* If a class implements an interface, it **must implement all abstract methods** from:

  * That interface
  * All parent interfaces

```java
class Sparrow implements Bird
{

    @Override
    public void fly()
    {
        System.out.println("Sparrow flies");
    }

    @Override
    public void move()
    {
        System.out.println("Sparrow moves");
    }

    @Override
    public void eat()
    {
        System.out.println("Sparrow eats");
    }
}
```

---

## Main Class Execution

```java
public class Main
{
    public static void main(String[] args)
    {
        Sparrow sparrow = new Sparrow();

        sparrow.fly();
        sparrow.move();
        sparrow.eat();
    }
}
```

### Output:

```
Sparrow flies
Sparrow moves
Sparrow eats
```

---

## Key Takeaways (Interview-Friendly)

* Interface methods are **public & abstract by default**
* Interfaces support **multiple inheritance**
* A class can implement **multiple interfaces**
* Interfaces **cannot extend classes**
* Interfaces help in **loose coupling** and **contract-based design**

---
