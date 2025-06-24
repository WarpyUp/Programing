## **Що таке Dependency Injection (DI)?**

**Dependency Injection (DI)** – це **патерн проєктування**, який дозволяє **відокремити створення залежностей від їх використання**. Іншими словами, **об’єкт не створює свої залежності самостійно**, а отримує їх ззовні.

Це підхід, коли **об’єкти не створюють залежності самостійно**, а **отримують їх зовні** (від контейнера або іншого класу).

**Чому це корисно?**
- **Легше тестувати код** → можна підставити мокові об’єкти.
- **Менше жорстких зв’язків** → компоненти не залежать напряму від конкретних реалізацій.
- **Керований життєвий цикл** → контейнер відповідає за створення та знищення залежностей.
- **З DI** – залежності передаються в клас, що робить його гнучким, тестованим і модульним.

## Аналогія з реального життя**
**Без Dependency Injection (Жорстка залежність)**

🔧 Уяви, що **автомеханік (OrderService)** сам виготовляє всі **інструменти (Database)** перед початком роботи.

Це означає, що якщо треба **замінити інструмент**, доведеться змінювати весь підхід механіка!

**З Dependency Injection (Гнучкість)**

🔧 Інструменти (залежності) **передаються** автомеханіку вже готовими. Він не залежить від їхнього способу виготовлення – може просто взяти і працювати.

# **Singleton**
The Singleton lifetime ensures that only one instance of a service is created and shared throughout the application’s lifetime. This means that whenever a request for the service is made, the same instance is returned. Singleton objects are instantiated lazily, meaning they are created only when needed.

Singleton instances are useful when you have a stateless service or a shared resource that should be accessed consistently across multiple requests. For example, consider a logging service that needs to be accessed from various parts of an application. By registering the logging service as a Singleton, you ensure that all components use the same instance, facilitating centralized logging and resource sharing.

# **Scoped**
The Scoped lifetime creates a new instance of a service for each scope or logical operation within an application. A scope represents a certain context, such as a web request or a unit of work. Any dependencies resolved within the same scope will receive the same instance.

Scoped instances are particularly useful when you have stateful services or resources that need to be shared within a specific context. For instance, when handling a web request, you may have a service that interacts with a database. In this scenario, using Scoped lifetime ensures that each request gets its own instance of the service, avoiding conflicts between multiple requests.

# **Transient**
The Transient lifetime creates a new instance of a service every time it is requested. This means that each dependency resolved will have its own unique instance.

Transient instances are suitable for lightweight and stateless services that don’t maintain any internal state or shared resources. Examples include utility classes or simple calculation services. Using Transient lifetime guarantees that each time a dependency is resolved, a fresh instance is created.

# **Choosing the Right Lifetime**
Choosing the appropriate lifetime for a service depends on the specific requirements of your application. Here are some guidelines to help you make the right decision:

# **Singleton**
- Use Singleton when you have stateless services or shared resources that need to be accessed consistently across the application.
- Be cautious when using Singleton with services that maintain mutable state, as concurrent access can lead to unexpected behavior or race conditions.

# **Scoped**
- Use Scoped when you have stateful services or resources that need to be shared within a specific context, such as a web request or unit of work.
- Scoped instances help ensure that each request or operation gets its own isolated instance, preventing interference between different contexts.

# **Transient**
- Use Transient for lightweight and stateless services that don’t maintain any internal state or shared resources.
- Transient instances are suitable for services that perform simple calculations, generate random numbers, or provide general utility functions.

To create transient service use next code.

```tsx
static di /* @__PURE__ */ = meta({ transient: true });
```

### **1. `static di` - Defining a Static Property**

- The `di` property is defined as **static**, meaning it belongs to the class itself rather than an instance of the class.
- You can access it via `MyClass.di` rather than `new MyClass().di`.

---

### **2. `/* @__PURE__ */` - Pure Annotation for Tree Shaking**

- The `@__PURE__` annotation is a special comment used by JavaScript minifiers (like Terser or UglifyJS).
- It tells the compiler that this expression has **no side effects**, meaning if the `di` property is not used, it can be safely removed during **tree shaking**.
- **Why?**
    - Without `@__PURE__`, the bundler may assume `meta({ transient: true })` has side effects and keep it in the final build, even if `di` is unused.

---

### **3. `meta({ transient: true })` - Assigning Metadata**

- `meta` is a function that takes an object (`{ transient: true }`) and simply returns it.
- So, `meta({ transient: true })` evaluates to `{ transient: true }`.
- The result is stored in the static `di` property.

This line is primarily used for **dependency injection (DI) metadata**. It helps a DI system determine how a class should be instantiated and managed.
