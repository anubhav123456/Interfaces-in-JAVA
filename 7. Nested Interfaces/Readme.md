
---

# 📌 Nested Interfaces in Java

## 🔹 What is a Nested Interface?

A **nested interface** is an interface **declared inside another interface or class**.

👉 When an interface is inside **another interface**, it is **implicitly `public` and `static`**.

```java
interface Outer {
    interface Inner {
        void method();
    }
}
```

---

## 🔹 Why Nested Interfaces?

Nested interfaces are used to:

1. **Logically group related contracts**
2. **Improve API readability**
3. **Restrict scope (namespacing)**
4. **Design clean frameworks & libraries**

---

## 🔹 Key Rules

* Nested interface inside an interface is:

  * `public`
  * `static`
* Can be implemented by **any class**
* Accessed using:
  👉 `OuterInterface.NestedInterface`

---

# ✅ Use Case 1: Multiple Roles Related to One Concept

### 🧠 Idea

A **Payment** has:

* payment action
* validation
* logging

Instead of creating **3 unrelated interfaces**, we group them under **Payment**.

---

### 📌 Code Example

```java
interface Payment {

    void pay();

    interface Validator {
        boolean validate();
    }

    interface Logger {
        void log();
    }
}
```

---

### 📌 Implementing All Roles

```java
class CreditCardPayment
        implements Payment, Payment.Validator, Payment.Logger {

    @Override
    public void pay() {
        System.out.println("Payment done using Credit Card");
    }

    @Override
    public boolean validate() {
        System.out.println("Validating credit card...");
        return true;
    }

    @Override
    public void log() {
        System.out.println("Payment logged successfully");
    }
}
```

---

### 📌 Main Class

```java
public class Main {
    public static void main(String[] args) {

        CreditCardPayment payment = new CreditCardPayment();

        if (payment.validate()) {
            payment.pay();
            payment.log();
        }
    }
}
```

---

### 🖥 Output

```
Validating credit card...
Payment done using Credit Card
Payment logged successfully
```

---

### 🎯 Why Nested Interface Here?

✔ Clear responsibility
✔ Better API design
✔ Easy to extend
✔ Avoids cluttering global namespace

---

# ✅ Use Case 2: Framework / Library Design (Real Java Example)

### 🧠 Best Example: `Map` Interface

```java
interface Map<K, V> {
    interface Entry<K, V> {
        K getKey();
        V getValue();
    }
}
```

---

### 📌 Usage

```java
Map.Entry<String, Integer> entry;
```

👉 `Entry` makes sense **ONLY** with `Map`, so it is nested.

---

# 🚀 Complete Working Example (Realistic + Clean)

### 📌 Scenario

We are designing a **FileProcessor framework**.

* Process file
* Validate file
* Log operations

---

### 📌 Interface Design

```java
interface FileProcessor {

    void process();

    interface Validator {
        boolean validateFile();
    }

    interface Logger {
        void logOperation(String message);
    }
}
```

---

### 📌 Implementation

```java
class PdfFileProcessor
        implements FileProcessor, FileProcessor.Validator, FileProcessor.Logger {

    @Override
    public void process() {
        System.out.println("Processing PDF file...");
    }

    @Override
    public boolean validateFile() {
        System.out.println("Validating PDF file...");
        return true;
    }

    @Override
    public void logOperation(String message) {
        System.out.println("LOG: " + message);
    }
}
```

---

### 📌 Main Class

```java
public class MainApp {
    public static void main(String[] args) {

        PdfFileProcessor processor = new PdfFileProcessor();

        if (processor.validateFile()) {
            processor.process();
            processor.logOperation("PDF processed successfully");
        }
    }
}
```

---

### 🖥 Output

```
Validating PDF file...
Processing PDF file...
LOG: PDF processed successfully
```

---

# 🧠 Interview One-Line Answers

### ❓ Why use nested interfaces?

👉 To **group related contracts**, improve **API clarity**, and **limit scope**.

### ❓ Are nested interfaces static?

👉 **Yes**, implicitly static when inside an interface.

### ❓ Can a class implement a nested interface?

👉 **Yes**, using `OuterInterface.InnerInterface`.

---

# 🧠 When NOT to use nested interfaces?

❌ If interfaces are **independent**
❌ If reuse is required across many unrelated modules

---
