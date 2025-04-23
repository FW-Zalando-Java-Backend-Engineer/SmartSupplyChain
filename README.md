# 🚛 Mega Java Assignment: SmartSupplyChain – Mastering Generics, OOP & Collections

## 🌍 Background: The SmartSupplyChain Initiative

Welcome to **SmartSupplyChain**, a futuristic logistics platform that aims to optimize how products move across suppliers, warehouses, and customers. You’ve been hired as a **Java Systems Engineer** on the core platform team to architect and implement a **type-safe, extensible, and maintainable backend**.

The project must support:

- Inventory systems for various types of products
- Flexible storage and packaging
- Supplier and customer management
- Support for perishables, electronics, documents, etc.

But here’s the twist: your system needs to be **fully generic**, **object-oriented**, and support **future expansion**. That means:

- Using **Java Generics** everywhere
- Applying solid **OOP principles** (Encapsulation, Inheritance, Polymorphism)
- Leveraging **Collections** (Lists, Maps)
- Designing **abstract classes** and **interfaces** to future-proof everything

---

## 🎯 What You’ll Practice

This assignment is an advanced simulation of real-world backend system design. You will:

- Create and implement **Generic Classes**, **Interfaces**, and **Methods**
- Apply **Bounded Type Parameters** for perishable goods
- Use **Wildcards** to safely access and manipulate collections
- Work with **inheritance trees** for suppliers and items
- Practice **encapsulation and polymorphism** through proper design
- Utilize **ArrayList** and **Map** collections
- Understand how **Type Erasure** affects runtime behavior

---

## 🧱 Project Structure (Suggestion)

```
SmartSupplyChain/
├── src/
│   ├── main/
│   │   └── SmartSupplyChainApp.java
│   ├── items/
│   │   ├── Product.java (abstract)
│   │   ├── Perishable.java
│   │   ├── Document.java
│   │   ├── Electronic.java
│   ├── inventory/
│   │   ├── StorageUnit<T>
│   │   ├── Package<T>
│   │   ├── Inventory<T>
│   ├── people/
│   │   ├── Person.java (abstract)
│   │   ├── Supplier.java
│   │   ├── Customer.java
│   ├── system/
│   │   ├── SupplyChainUtils.java (generic methods)
│   │   ├── ProductRepository<T> (generic interface)
├── README.md
```

---

## 📚 Assignment Story & Tasks

### 🚦 Task 1: Model the Core Product Hierarchy

#### Background:

Products vary in type. Some expire (like milk), some don't (like documents), and some are electronic. All share some common behavior, but their implementation differs.

#### Instructions:

1. Create an **abstract class **`` with properties like `name`, `id`, and `getType()`.
2. Create the following concrete subclasses:
   - `Document`
   - `Electronic`
   - `Perishable` (add field: `expirationDate` and method `isExpired()`)
3. Use **encapsulation** for fields and provide accessors.
4. Override `toString()` for pretty logging.

#### Concepts Practiced:

- Inheritance
- Abstract classes
- Encapsulation

---

### 🏪 Task 2: Build a Generic Storage Unit

#### Background:

Each warehouse stores items differently. You must create flexible, type-safe containers.

#### Instructions:

1. Create a **generic class **`` with:
   - `addItem(T item)`
   - `T getItem()`
2. Add a version of `StorageUnit<T>` that stores **lists of items**, e.g., `ArrayList<T>`.
3. Support bulk addition and retrieval.

#### Concepts Practiced:

- Generic classes
- ArrayList usage

---

### 📦 Task 3: Create Packages and Inventory

#### Background:

Products are packaged into boxes, and multiple boxes make up inventory.

#### Instructions:

1. Create a ``** generic class** to wrap multiple products.
2. Create a ``** class** with a `Map<String, Package<T>>` to map package IDs to their contents.
3. Use wildcards to support printing inventory with `printInventory(List<? extends Product>)`

#### Concepts:

- Wildcards in collections
- Map usage

---

### 👩‍💼 Task 4: Create People Hierarchy

#### Background:

Suppliers provide products, customers receive them.

#### Instructions:

1. Create an **abstract class **`` with `id`, `name`, and a `getRole()` method.
2. Implement `Supplier` and `Customer` classes.
3. Suppliers have a `List<Package<? extends Product>> packagesSupplied`
4. Customers have a method to receive a `Package<?>`

#### Concepts:

- Abstract classes
- Inheritance
- Polymorphism with wildcards

---

### 🧠 Task 5: Supply Chain Utilities (Generic Methods)

#### Background:

We want reusable utilities for printing, filtering, and processing inventory.

#### Instructions:

Create a class `SupplyChainUtils` with:

1. A **generic method** to print any object: `<T> void displayItem(T item)`
2. A method to **filter expired perishables**: `<T extends Perishable> List<T> getExpired(List<T> items)`
3. A method to find packages by product type with wildcards

#### Concepts:

- Generic methods
- Bounded type parameters
- Wildcards in method params

---

### 🧪 Task 6: Demonstrate Type Erasure

#### Background:

Your manager wants proof that type info is erased at runtime.

#### Instructions:

1. In your `main` class, create two storage units:
   - `StorageUnit<Electronic>`
   - `StorageUnit<Document>`
2. Use reflection or `instanceof` to demonstrate that type `T` is not preserved.

#### Concepts:

- Type erasure theory

---

### 🧩 Task 7: Bring it All Together in `SmartSupplyChainApp`

#### Background:

You need a working simulation to demo to stakeholders.

#### Instructions:

1. In `SmartSupplyChainApp`:

   - Create products and suppliers
   - Package items and add to inventory
   - Print reports using wildcard methods
   - Call utility functions to filter expired items

2. Use collections (ArrayList, Map) properly throughout

3. Use `toString()` and clean output to present data

#### Concepts:

- Application architecture
- System testing
- Clean coding practices

---

## 💎 Bonus Challenges (Optional)
Create a **CLI** to interact with suppliers and inventory

---

## 📤 Submission

Push your entire project to a **public GitHub repo** named: `SmartSupplyChain-YourName`

- Include a clear `README.md`
- Include sample data in your `main` method
- Submit the link on Slack

---

## 🧠 Final Advice

- Write clear and maintainable code
- Stick to Java best practices
- Focus on relationships and reusability, not just completing the checklist
- This project simulates what real enterprise backends look like — **design it like you mean it!**

Good luck, engineer! 💼

