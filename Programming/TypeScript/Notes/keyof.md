`keyof` — це оператор у TypeScript, який бере тип об'єкта і повертає тип, що є об'єднанням усіх публічних ключів (імен властивостей) цього об'єкта у вигляді рядкових літералів.

**Навіщо потрібен?** 
Він дозволяє створювати функції або типи, які працюють з іменами властивостей об'єкта, гарантуючи типову безпеку. Це допомагає уникнути помилок, коли ви намагаєтеся отримати доступ до неіснуючої властивості.

```typeScript
type User = {
    id: number;
    name: string;
    age: number;
};

// Тип 'UserKeys' буде 'id' | 'name' | 'age'
type UserKeys = keyof User;

function getPropertyValue<T, K extends keyof T>(obj: T, key: K) {
    return obj[key]; 
}

// --- Використання ---

let user: User = { id: 1, name: "Alice", age: 30 };

let userId = getPropertyValue(user, "id");  
let userName = getPropertyValue(user, "name");

// getPropertyValue(user, "city"); // ПОМИЛКА: 'city' не є ключем типу 'User'
```
