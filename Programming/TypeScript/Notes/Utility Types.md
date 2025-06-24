**Utility Types** — це попередньо визначені, вбудовані "функції" TypeScript для маніпулювання типами. 
Вони дозволяють створювати нові типи на основі існуючих, трансформуючи їх різними способами.

Найпоширеніші включають: `Partial`, `Readonly`, `Pick`, `Omit`, `Exclude`, `Extract`, `NonNullable`, `Record`, `Parameters`, `ReturnType`, `Awaited`.

---

### 1. `Partial<Type>`

- **Що робить:** Робить всі властивості `Type` опціональними.
- **Коли використовувати:** Для створення об'єктів для часткового оновлення даних, де не всі поля є обов'язковими.
- **Приклад:**
```typeScript
type User = { name: string; age: number; };
type PartialUser = Partial<User>; // { name?: string; age?: number; }
let update: PartialUser = { age: 30 }; // OK
```

### 2. `Readonly<Type>`

- **Що робить:** Робить всі властивості `Type` тільки для читання.
- **Коли використовувати:** Коли потрібно забезпечити, що об'єкт не буде змінений після його створення (іммутабельність).
- **Приклад:**
```typeScript
type Product = { id: number; price: number; };
type ReadonlyProduct = Readonly<Product>; // { readonly id: number; readonly price: number; }
let p: ReadonlyProduct = { id: 1, price: 100 };
// p.price = 120; // ПОМИЛКА: Не можна переприсвоїти
```

### 3. `Pick<Type, Keys>`

- **Що робить:** Створює новий тип, вибираючи (picking) вказані `Keys` з `Type`.
- **Коли використовувати:** Щоб створити підмножину властивостей з існуючого типу.
- **Приклад:**
```typeScript
type Order = { id: number; customer: string; date: string; total: number; };
type OrderSummary = Pick<Order, "id" | "total">; // { id: number; total: number; }
let summary: OrderSummary = { id: 101, total: 250 }; // OK
```

### 4. `Omit<Type, Keys>`

- **Що робить:** Створює новий тип, виключаючи (omitting) вказані `Keys` з `Type`.
- **Коли використовувати:** Щоб створити тип, який є майже таким же, як інший, але без деяких властивостей.
- **Приклад:**
```typeScript
type FullUser = { id: number; name: string; passwordHash: string; };
type PublicUser = Omit<FullUser, "passwordHash">; // { id: number; name: string; }
let user: PublicUser = { id: 1, name: "Alice" }; // OK
```

### 5. `Record<Keys, Type>`

- **Що робить:** Створює тип об'єкта, властивості якого мають ключі з `Keys` та значення типу `Type`.
- **Коли використовувати:** Для створення об'єкта, де ви заздалегідь знаєте можливі ключі, і всі їхні значення мають однаковий тип.
- **Приклад:**
```typeScript
type Animal = "cat" | "dog" | "bird";
type AnimalSounds = Record<Animal, string>; // { cat: string; dog: string; bird: string; }
let sounds: AnimalSounds = { cat: "Meow", dog: "Woof", bird: "Chirp" }; // OK
```

### 6. `Exclude<UnionType, ExcludedMembers>`

- **Що робить:** Виключає `ExcludedMembers` з `UnionType` (для об'єднаних типів).
- **Коли використовувати:** Для створення нового об'єднаного типу без певних членів.
- **Приклад:**
```typeScript
type Colors = "red" | "green" | "blue" | "yellow";
type PrimaryColors = Exclude<Colors, "yellow">; // "red" | "green" | "blue"
let color: PrimaryColors = "red"; // OK
// let otherColor: PrimaryColors = "yellow"; // ПОМИЛКА
```

### 7. `NonNullable<Type>`

- **Що робить:** Виключає `null` та `undefined` з `Type`.
- **Коли використовувати:** Коли ви впевнені, що змінна не буде `null` або `undefined`, і хочете працювати з її "чистим" типом.
- **Приклад:**
```typeScript
type Name = string | null | undefined;
type NonNullName = NonNullable<Name>; // string
let myName: NonNullName = "John"; // OK
// let emptyName: NonNullName = null; // ПОМИЛКА
```

### 8. `Parameters<Type>`

- **Що робить:** Витягує типи параметрів функції `Type` у вигляді кортежу (tuple).
- **Коли використовувати:** Коли потрібно отримати типи аргументів функції для їх подальшого використання.
- **Приклад:**
```typeScript
function greet(name: string, age: number) { /* ... */ }
type GreetParams = Parameters<typeof greet>; // [name: string, age: number]
let args: GreetParams = ["Alice", 25]; // OK
```

### 9. `ReturnType<Type>`

- **Що робить:** Витягує тип значення, що повертається функцією `Type`.
- **Коли використовувати:** Коли потрібно отримати тип результату виконання функції.
- **Приклад:**
```typeScript
function calculateSum(a: number, b: number): number { return a + b; }
type SumResult = ReturnType<typeof calculateSum>; // number
let result: SumResult = 100; // OK
```