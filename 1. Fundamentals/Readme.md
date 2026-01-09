# Java Interface

## What is an Interface?

An **interface** is a **contract** that allows two systems to interact **without knowing each other’s internal details**.

👉 It focuses on **what to do**, not **how to do it**.

---

## 🔹 Key Idea

* One system **exposes what it can do**
* The other system **only calls methods**
* The internal implementation is **hidden**

👉 This concept is called **Abstraction**

---

## Definition of Interface

An interface helps achieve **abstraction** by defining **what a class must do**, not **how it does it**.

---

## Interface Declaration

```java
interface PaymentGateway
{
    void pay(int amount);
}
```

### Explanation

* `PaymentGateway` is a **contract**
* Any payment system must implement `pay(int amount)`
* Interface does **not** contain implementation details

---

## Implementation 1: UPI Payment

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

### What is hidden?

* QR scanning
* Bank API calls
* UPI validation logic

---

## Implementation 2: Net Banking Payment

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

### What is hidden?

* Bank login flow
* Authorization steps
* Bank selection logic

---

## Implementation 3: Card Payment

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

### What is hidden?

* CVV validation
* OTP verification
* Payment gateway integration

---

## Client Class: PaymentService

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
        paymentGateway.pay(amount);
    }
}
```

### Key Points

* `PaymentService` depends on **interface**, not concrete classes
* This follows **Dependency Injection**
* Makes code **flexible and extensible**

---

## Main Class

```java
public class Main
{
    public static void main(String[] args)
    {
        PaymentGateway gateway1 = new UPIPayment();
        PaymentGateway gateway2 = new CardPayment();
        PaymentGateway gateway3 = new NetBankingPayment();

        new PaymentService(gateway1).makePayment(500);
        new PaymentService(gateway2).makePayment(800);
        new PaymentService(gateway3).makePayment(1000);
    }
}
```

---

## Output

```text
Paid 500 using UPI
Paid 800 using Card
Paid 1000 using Net Banking
```

---

## System Interaction Explained

### System 1: `PaymentService` (Client)

It does **NOT** know:

1. How `UPIPayment` is implemented
2. How `CardPayment` internally works
3. What steps `NetBankingPayment` follows

---

### System 2: Payment Gateways

* `UPIPayment`
* `CardPayment`
* `NetBankingPayment`

All follow **one common contract** → `PaymentGateway`

---

## Why Interface is Needed?

* To enforce a **common structure**
* To achieve **loose coupling**
* To support **multiple implementations**
* To make the system **scalable**

---

## Final Summary

* Interface = **Contract**
* Client depends on **interface**, not implementation
* Implementation details are **hidden**
* This achieves **abstraction, flexibility, and clean design**

✔️ *"HOW it pays – it does not know, and it does not care."*

---