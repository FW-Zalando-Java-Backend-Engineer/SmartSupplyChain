# 🚛 Mega Java Assignment: **SmartSupplyChain**  
### Mastering Generics, OOP, Collections & Exception Handling  
*A real-world systems engineering challenge*

---

## 🧠 Project Overview

You're tasked with building the core of **SmartSupplyChain**, a Java-powered logistics system that handles the flow of products — from suppliers, through warehouses, to customers — **safely**, **scalably**, and **fault-tolerantly**.

Each module should reflect best practices in:
- OOP (encapsulation, abstraction, inheritance)
- Generics (type safety, bounded types, wildcards)
- Exception handling (custom exceptions, input validation)
- Collections (List, Map)
- System simulation (via `main()`)

---

## 🗂️ **SmartSupplyChain – Full Project Structure**

```
SmartSupplyChain/
├── README.md                       # Project overview and setup instructions
├── src/
│   ├── main/
│   │   └── SmartSupplyChainApp.java        # Entry point: simulation, flow orchestration
│
│   ├── items/                              # Product domain layer
│   │   ├── Product.java                    # Abstract base for all products
│   │   ├── Perishable.java                 # Extends Product, includes expiration logic
│   │   ├── Document.java                   # Concrete non-perishable product
│   │   ├── Electronic.java                 # Concrete electronic product
│
│   ├── inventory/                          # Inventory and packaging logic
│   │   ├── StorageUnit.java                # Generic container for items
│   │   ├── MultiStorageUnit.java           # Generic container that stores a list
│   │   ├── Package.java                    # Wraps a group of items
│   │   ├── Inventory.java                  # Maps package IDs to packages
│
│   ├── people/                             # Actors interacting with inventory
│   │   ├── Person.java                     # Abstract person class
│   │   ├── Supplier.java                   # Supplies packages
│   │   ├── Customer.java                   # Receives packages
│
│   ├── system/                             # Utility functions for logic & validation
│   │   ├── SupplyChainUtils.java          # Generic methods, validation, expiration checks
│
│   ├── exception/                          # Custom exception handling
│   │   ├── ExpiredProductException.java    # Thrown when expired items are used
│   │   ├── EmptyStorageException.java      # Thrown when accessing empty storage
│   │   ├── InvalidInputException.java      # Thrown when user/product input is invalid
```

---

## 🧾 What's in each folder?

### `items/`
All product-related classes, forming the inheritance hierarchy. This includes perishable items that may throw exceptions if expired.

### `inventory/`
Logic related to how products are stored, grouped, and managed. It also handles generic containers and inventory mapping.

### `people/`
Classes for users of the system: suppliers (who provide packages) and customers (who receive them). These classes interact with inventory safely.

### `system/`
Contains reusable tools like item printers, expiration checkers, and input validators.

### `exception/`
Custom exceptions that enforce safe and robust code:
- **ExpiredProductException**: for expired item handling.
- **EmptyStorageException**: for attempting to retrieve from empty storage.
- **InvalidInputException**: for catching invalid user or object input early.

### `main/`
The heart of the simulation — here, you'll glue everything together, simulate operations, and catch exceptions gracefully.

---

## 📚 Task Breakdown

---

### 🚦 **Task 1: Model the Core Product Hierarchy**

#### 🔍 Background
You're modeling diverse types of products. Some can expire (e.g., milk), others are non-perishable (e.g., documents). All products share common identity fields but differ in behavior.

#### 🪜 Steps
1. Define a base abstract class `Product` with common fields like `id`, `name`, and an abstract method `getType()`.
2. Create 3 subclasses:
   - `Document`: represents paperwork or forms.
   - `Electronic`: devices like phones, routers.
   - `Perishable`: anything that expires. Add an integer field (e.g., `expirationDay`) and a method `isExpired(int today)`.
3. In `Perishable`, if an expired item is processed, it should trigger an `ExpiredProductException`.
4. Use encapsulation (private fields + public getters/setters).
5. Override `toString()` in each subclass to display clean info.

#### 🧠 Concepts
- Abstract classes & polymorphism
- Domain-specific behavior
- Exception triggering from domain logic

---

### 🏪 **Task 2: Build a Generic Storage Unit**

#### 🔍 Background
Warehouses need containers for storing different item types. These containers must be generic, so they can hold any type, and must prevent invalid use (e.g., adding null, or retrieving when empty).

#### 🪜 Steps
1. Create a generic class `StorageUnit<T>`.
2. Add:
   - `addItem(T item)`: If `item` is `null`, throw an `InvalidInputException`.
   - `getItem()`: If nothing is stored, throw an `EmptyStorageException`.
3. Add another version that holds multiple items in a `List<T>` (like a shelf).
4. Implement basic bulk operations like adding a list of items and retrieving the whole list.

#### 🧠 Concepts
- Generic types
- Exception safety
- Defensive programming
- Collection use

---

### 📦 **Task 3: Create Packages and Inventory System**

#### 🔍 Background
Items are grouped into packages, and packages are mapped in inventory by ID. These structures must handle bulk data, type diversity, and potential data issues (like expired items).

#### 🪜 Steps
1. Design a generic class `Package<T>` that holds a collection of products.
2. Create an `Inventory<T>` class containing a `Map<String, Package<T>>` to associate package IDs to their contents.
3. Add methods to:
   - Add new packages.
   - Retrieve packages by ID.
   - Print inventory using a method that accepts wildcards (`List<? extends Product>`).
4. Ensure any invalid or expired product in a package triggers an exception during validation or reporting.

#### 🧠 Concepts
- Map-based indexing
- Generic and wildcard methods
- Data integrity enforcement
- Exception-driven control flow

---

### 👩‍💼 **Task 4: Create People Hierarchy (Supplier/Customer)**

#### 🔍 Background
People in the supply chain either provide products (suppliers) or receive them (customers). Each role must interact with the system in a safe, validated manner.

#### 🪜 Steps
1. Create an abstract class `Person` with shared fields like `id`, `name`, and method `getRole()`.
2. Implement:
   - `Supplier`: Owns a list of `Package<? extends Product>`. Can add products to packages.
   - `Customer`: Can `receivePackage(Package<?>)`. If a package includes expired items, throw `ExpiredProductException`.
3. Ensure that no person is created with a blank or null ID/name. Use `InvalidInputException` to enforce this.

#### 🧠 Concepts
- Abstract class + inheritance
- Polymorphic roles
- Wildcards in method parameters
- Runtime input validation

---

### 🧠 **Task 5: Utility Methods (with Exception Handling)**

#### 🔍 Background
Utility classes provide reusable functionality, and they should be defensive. These methods will validate, filter, and display data safely.

#### 🪜 Steps
1. Create a class `SupplyChainUtils`.
2. Add:
   - A generic method `displayItem(T item)` to print any item.
   - A method `<T extends Perishable> List<T> getExpired(List<T> items, int today)` that returns expired items.
     - If any are expired, consider throwing `ExpiredProductException` or logging a warning.
   - A method `validateInput(String value)` that throws `InvalidInputException` for null/empty strings.
3. Use these utility methods across your entire app.

#### 🧠 Concepts
- Generic methods
- Input validation
- Bounded types and exceptions
- Centralized error prevention

---

### 🧪 **Task 6: Demonstrate Type Erasure**

#### 🔍 Background
Generic types are erased at runtime — that’s Java’s type erasure. Proving it shows your understanding of the limits of generics.

#### 🪜 Steps
1. Create two storage units: `StorageUnit<Electronic>` and `StorageUnit<Document>`.
2. Use reflection to print their class names and show they're the same type at runtime.
3. Handle potential reflection exceptions in a try-catch block.

#### 🧠 Concepts
- Type erasure demonstration
- Reflection API
- Safe introspection

---

### 🧩 **Task 7: SmartSupplyChainApp – The Simulation**

#### 🔍 Background
This is your system's big demo. Simulate an end-to-end flow from supplier to customer, ensuring all exception handling paths are covered.

#### 🪜 Steps
1. In your `main()` method:
   - Create a supplier and add valid + expired products to packages.
   - Add packages to inventory.
   - Have a customer receive a package.
   - Catch any exceptions and print clear logs.
2. Add simulations of:
   - Getting from empty storage
   - Creating a product with invalid input
   - Receiving a package with expired items
3. Log exceptions using `System.out.println()` or optionally Java’s `Logger`.
4. Use a `finally` block to print a closing statement (e.g., `System shutting down...`).

#### 🧠 Concepts
- Application orchestration
- Multi-exception handling
- Error recovery and cleanup

---

## 💎 Bonus Challenges (Optional – 10 pts)

1. Use `Scanner` to create a basic CLI — input validation is key!
2. Replace `System.out.println()` with a proper `Logger` for exception events.
3. Add retry logic if an exception is thrown during item addition or retrieval.

---

## 📤 Submission Checklist

✅ Push to GitHub (`SmartSupplyChain-YourName`)  
✅ Include a complete README and sample outputs  
✅ Submit the link on your class portal or LMS
