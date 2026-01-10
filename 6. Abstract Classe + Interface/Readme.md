Below are **clean, exam-ready + interview-ready notes** for your code.
I’ll explain **concept → pattern → flow → output**, with **code snippets** included.

---

# 📌 Abstract Class + Interface (with Example)

## 🔹 Core Idea

> **Interface** defines *what* a class **can do** (capability / contract)
> **Abstract class** defines *how much* is **already done** (partial implementation)

Using **both together** gives:

* ✅ Loose coupling
* ✅ Code reuse
* ✅ Flexibility to change implementations
* ✅ Clean & scalable architecture

---

## 🔹 Complete Code

```java
interface Payment
{
    // Mandatory and Template Method
    void pay(int amount);
}

abstract class BasePayment implements Payment
{
    // Common Validation Method
    void validate(int amount)
    {
        if (amount <= 0)
        {
            System.out.println("Amount can not be negative : " + amount);
            return;
        }

        System.out.println("Amount validated");
    }

    // common security check
    void securityCheck()
    {
        System.out.println("Security check passed");
    }

    // common logging
    void logTransaction(int amount)
    {
        System.out.println("Transaction logged for amount: " + amount);
    }
}

class UPIPayment extends BasePayment
{
    @Override
    public void pay(int amount)
    {
        validate(amount);
        securityCheck();
        logTransaction(amount);
        System.out.println("Paid " + amount + " using UPI");
    }
}

class CardPayment extends BasePayment
{
    @Override
    public void pay(int amount)
    {
        validate(amount);
        securityCheck();
        logTransaction(amount);
        System.out.println("Paid " + amount + " using Card");
    }
}

public class Main
{
    public static void main(String[] args)
    {
        Payment p1 = new UPIPayment();
        p1.pay(500);

        System.out.println("------------");

        Payment p2 = new CardPayment();
        p2.pay(1000);
    }
}

```

---

## 🔹 Why use Interface here?

```java
interface Payment
{
    // Mandatory method (contract)
    void pay(int amount);
}
```

### Purpose:

* Forces **all payment types** (UPI, Card, NetBanking, etc.) to implement `pay()`
* Allows **polymorphism**

```java
Payment p = new UPIPayment();
```

👉 You can switch implementations **without changing client code**

---

## 🔹 Why use Abstract Class?

```java
abstract class BasePayment implements Payment
{
    void validate(int amount) { ... }
    void securityCheck() { ... }
    void logTransaction(int amount) { ... }
}
```

### Purpose:

* Avoids **code duplication**
* Keeps **common logic** in one place
* Subclasses only focus on **specific payment logic**

---

## 🔹 Is this Template Method Pattern?

### ❌ Not strictly (but **close**)

### Why?

* In **pure Template Method**, the **abstract class controls the sequence**
* Here, **child classes control the flow**

👉 To make it **true Template Method**, you would do:

```java
abstract class BasePayment implements Payment
{
    // Template method
    public final void pay(int amount)
    {
        validate(amount);
        securityCheck();
        logTransaction(amount);
        doPay(amount);
    }

    protected abstract void doPay(int amount);
}
```

But your version is **conceptually inspired**, not strict.

---

## 🔹 Concrete Implementations

### ✅ UPI Payment

```java
class UPIPayment extends BasePayment
{
    @Override
    public void pay(int amount)
    {
        validate(amount);
        securityCheck();
        logTransaction(amount);
        System.out.println("Paid " + amount + " using UPI");
    }
}
```

### ✅ Card Payment

```java
class CardPayment extends BasePayment
{
    @Override
    public void pay(int amount)
    {
        validate(amount);
        securityCheck();
        logTransaction(amount);
        System.out.println("Paid " + amount + " using Card");
    }
}
```

---

## 🔹 Main Class (Polymorphism in Action)

```java
public class Main
{
    public static void main(String[] args)
    {
        Payment p1 = new UPIPayment();
        p1.pay(500);

        System.out.println("------------");

        Payment p2 = new CardPayment();
        p2.pay(1000);
    }
}
```

### What’s happening?

* `Payment` reference → different implementations
* Runtime decides **which `pay()` to execute**
* This is **runtime polymorphism**

---

## 🔹 Program Output

```
Amount validated
Security check passed
Transaction logged for amount: 500
Paid 500 using UPI
------------
Amount validated
Security check passed
Transaction logged for amount: 1000
Paid 1000 using Card
```

---

## 🔹 Why not ONLY Abstract Class?

### ❌ Problem with only abstract class:

* Java allows **single inheritance only**
* You lose flexibility

### ✅ Interface solves this:

* Multiple inheritance of behavior via interfaces
* Better for **API design**
* Clean separation between **what** and **how**

---

## 🔹 Final Interview Summary (💯 important)

> **Interface + Abstract Class together provide a powerful design**
> Interface defines the **contract**, abstract class provides **shared behavior**, and concrete classes provide **specific implementations**.
> This approach improves **maintainability, extensibility, and loose coupling**.

---
