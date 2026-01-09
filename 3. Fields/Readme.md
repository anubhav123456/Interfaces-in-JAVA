
---

# 📌 Java Interface Fields

## 🔹 Key Rule

> **All fields (variables) declared inside a Java interface are implicitly:**

* `public`
* `static`
* `final`

Even if you don’t write these keywords, the compiler adds them automatically.

---

## ✅ Why Interface Fields Are `public static final`?

### 1️⃣ `public`

* Interfaces define **contracts**
* Constants inside interfaces must be accessible to **all implementing classes**
* Hence, fields are `public` by default

```java
PaymentGateway.MAX_LIMIT   // accessible everywhere
```

---

### 2️⃣ `static`

* Interfaces **cannot be instantiated**
* Fields must be accessed using the **interface name**
* Therefore, fields belong to the interface itself, not to objects

```java
PaymentGateway.MAX_LIMIT   // static access
```

---

### 3️⃣ `final`

* Interface fields represent **constants**
* Implementing classes **must not modify** them
* This ensures **consistency across all implementations**

❌ Not allowed:

```java
MAX_LIMIT = 200_000; // Compile-time error
```

---

## 📌 Important Compiler Truth

This:

```java
int MAX_LIMIT = 100_000;
```

Is treated by the compiler as:

```java
public static final int MAX_LIMIT = 100_000;
```

---

# 🧩 Example: Payment Gateway System

## 🔹 Interface

```java
interface PaymentGateway
{
    int MAX_LIMIT = 100_000;
    void pay(int amount);
}
```

---

## 🔹 Implementations

### UPI Payment

```java
class UPIPayment implements PaymentGateway
{
    @Override
    public void pay(int amount)
    {
        // Internal Details
        // It will scan QR code, bank API, etc
        System.out.println("Paid " + amount + " using UPI");
    }
}
```

---

### Net Banking Payment

```java
class NetBankingPayment implements PaymentGateway
{
    @Override
    public void pay(int amount)
    {
        // Internal Details
        // Login to bank portal, select bank, authorize payment, etc
        System.out.println("Paid " + amount + " using Net Banking");
    }
}
```

---

### Card Payment

```java
class CardPayment implements PaymentGateway
{
    public void pay(int amount)
    {
        // Internal Details
        // It will check CVV, OTP, gateway call etc
        System.out.println("Paid " + amount + " using Card");
    }
}
```

---

## 🔹 Service Layer (Dependency Injection)

```java
class PaymentService
{
    private PaymentGateway paymentGateway;

    public PaymentService(PaymentGateway paymentGateway)
    {
        this.paymentGateway = paymentGateway;
    }

    public void makePayment(int amount)
    {
        if(amount > PaymentGateway.MAX_LIMIT)
        {
            System.out.println(
                String.format(
                    "You can not do transaction more than %d",
                    PaymentGateway.MAX_LIMIT
                )
            );
            return;
        }
        paymentGateway.pay(amount);
    }
}
```

---

## 🔹 Main Class

```java
public class Main
{
    public static void main(String[] args)
    {
        PaymentGateway gateway1 = new UPIPayment();
        PaymentGateway gateway2 = new CardPayment();
        PaymentGateway gateway3 = new NetBankingPayment();

        var service1 = new PaymentService(gateway1);
        var service2 = new PaymentService(gateway2);
        var service3 = new PaymentService(gateway3);

        service1.makePayment(500);
        service2.makePayment(800);
        service3.makePayment(1000);
        service3.makePayment(150_000);
    }
}
```

---

# 🖨️ Program Output

```text
Paid 500 using UPI
Paid 800 using Card
Paid 1000 using Net Banking
You can not do transaction more than 100000
```

---

# 🎯 Key Takeaways (Interview Gold)

* Interface variables are **constants**
* They are shared across **all implementations**
* Cannot be overridden or reassigned
* Accessed using **InterfaceName.FIELD**
* Helps enforce **business rules** globally (e.g., `MAX_LIMIT`)

---
