
Це сучасний, рекомендований спосіб взаємодіяти з базою даних Firestore. Ви імпортуєте окремі функції.

Це стиль, який використовується в AngularFire версії 7 і новіших. Його ще називають "tree-shakable" API.

Ключова ідея — використання окремих функцій замість методів одного великого об'єкта. Це робить код чистішим і значно ефективнішим.

---
### Процес роботи

Детальніше про считування написано [[Считування з Firebase|тут]]
#### Інєкція

Щоб сервіс міг взаємодіяти з базою даних [[Firestore]], йому потрібен доступ до екземпляра **`Firestore`**. Angular має механізм для цього, який називається [[Dependency Injection]] (DI) – впровадження залежностей.

У конструкторі вашого компонента чи сервісу ви отримуєте доступ до основного сервісу `Firestore`.

```ts
constructor(private firestore: Firestore) {}
```

#### Імпорт функцій

Ви імпортуєте лише ті функції, які вам потрібні в даному файлі (`collection`, `doc`, `addDoc` тощо).

```ts
import { collection, doc, addDoc, collectionData } from '@angular/fire/firestore';
```

#### Виклик функцій

Ви викликаєте імпортовану функцію, передаючи їй ваш екземпляр `firestore` як перший аргумент. 

```ts
const notesRef = collection(this.firestore, 'notes'); // Повертає посилання на колекцію
```

Таким чином ми отримуємо посилання на колекція. Щоб получити [[DocumentReference|посилання на окремий документ]] потрібно використати `doc`.

```ts
// doc(firestore, 'колекція/ID_документа')
const noteRef = doc(this.firestore, `notes/${id}`);
```

Для конвертації даних можна використати [[FirestoreDataConverter]].

---
### Считування даних(CollectionData, docData)

Для читання даних, які оновлюються в реальному часі, використовуються спеціальні функції (`collectionData`, `docData`), які повертають `Observable` з бібліотеки RxJS.

За замовчуванням, функція `collectionData` і `docData` не додає ID документа до об'єктів. Щоб отримати ID, потрібно передати спеціальну опцію: `{ idField: 'id' }`.

```ts
collectionData(notesRef, { idField: 'id' });
```

Повертає `Observable`, який буде видавати масив об'єктів з колекції при будь-яких змінах.

```ts
docData(noteRef, { idField: 'id' });
```

Повертає `Observable`, який видає один об'єкт документа при його зміні.

---
### Запис та зміна даних

**Операції запису повертають [[Promise]]**: Додавання, оновлення та видалення — це одноразові дії. Вони не є потоком даних, тому повертають `Promise`, який ви можете обробити через `.then()` або `async/await`.

#### addDoc()

Додає новий документ в колекцію з автоматично згенерованим ID.

Використання з [[async, await|async/await]]

```ts
async createNote(title: string) { 
	const newDoc = await addDoc(notesCollection, { title: title, content: '' }); 
}
```

Використання з `.then` 

```ts
addDoc(notesCollection, { title: title, content: '' }) .then((newDoc) => { 
	console.log('Нотатка створена з ID:', newDoc.id); }) .catch((error) => { 
	console.error("Помилка створення нотатки: ", error); });
```

Далі буде тільки з async/await

Повертає [[DocumentReference]]

#### setDoc()

Створює або повністю перезаписує документ. Якщо документа не існує, він буде створений. Якщо існує — всі його старі дані будуть видалені і замінені новими.

```ts
// Цей запис повністю замінить вміст документа 'user123'
const userDoc = doc(this.firestore, 'users/user123');
await setDoc(userDoc, note);
```

Можна передати цілий обєкт, наприклад `note`, в параметри і перезаписати обєкт повністю.

Опція `{ merge: true }` зробить його більш похожим на updateDoc() - він оновить поля, а не перезапише весь документ.

```ts
await setDoc(userDoc, note, { merge: true });
```
#### updateDoc()

Частково оновлює існуючий документ. Якщо документа не існує, поверне помилку.

```ts
// Це оновить тільки поле 'lastLogin', не чіпаючи інші 
const userDoc = doc(this.firestore, 'users/user123'); await updateDoc(userDoc, { lastLogin: new Date() });
```

Не можна передати обєкт, наприклад`note`, в параметри, бо updateDoc не дає змінити id навіть на те саме.
`{ts}updateDoc(userDoc, note)` видасть помилку.

Потрібно надати обєкт без `id`. Для цього можна використати [[Деструктуризація Обєкта|деструктуризацію]].
#### deleteDoc()

Видаляє документ.

```ts
async deleteNote(id: string) { 
	const noteDoc = doc(this.firestore, `notes/${id}`); 
	await deleteDoc(noteDoc); 
}
```

---
### Фільтрація

`query(посилання, ...умови)` Дозволяє робити складні запити: фільтрувати, сортувати, обмежувати кількість результатів. Використовується разом з `collectionData` або `getDocs`.

```ts
const tasksCollection = collection(this.firestore, 'tasks');

const q = query(tasksCollection, 
	where('isActive', '==', true), 
	orderBy('createdAt', 'desc'), limit(10) 
);

this.activeTasks$ = collectionData(q, { idField: 'id' });
```
