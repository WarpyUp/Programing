
Це застарілий спосіб взаємодіяти з базою даних Firestore, який використовувався у старих версіях AngularFire. Використовувався в AngularFire версії 6 і раніше.

Ключова ідея — використання одного великого сервісу `AngularFirestore`, який має всі необхідні методи. Ви будуєте свій запит, викликаючи методи ланцюжком один за одним.

Сервіс `AngularFirestore` є "швейцарським ножем" — він вміє все. Це зручно, але менш продуктивно, оскільки весь його код включається у ваш додаток.

---
### Процес

#### Імпорт

Ви імпортуєте один універсальний сервіс `AngularFirestore`.

```ts
import { AngularFirestore } from '@angular/fire/firestore';
```

#### Інєкція

У конструкторі ви отримуєте доступ до цього сервісу, часто називаючи його `afs`.

```ts
constructor(private afs: AngularFirestore) {}
```

#### Виклик методів ланцюжком

Ви починаєте з `this.afs`, потім викликаєте `.collection()`, потім `.doc()` (якщо потрібно), і в кінці — метод для отримання даних, наприклад `.valueChanges()`.

```ts
this.afs.collection('notes').valueChanges(); // Отримати дані колекції
```

Вся робота побудована на виклику методів по черзі: `afs.collection(...).doc(...).update(...)`.

---

### Створення посилань

#### asf.collection()

Повертає об'єкт `AngularFirestoreCollection` — спеціальний об'єкт AngularFire для роботи з колекцією.

```ts
const itemsCollection = this.afs.collection('items');
```

#### asf.doc()

Повертає об'єкт `AngularFirestoreDocument`.

```ts
const itemDoc = this.afs.doc('items/unique-id');
```

### Читання даних

Ці методи викликаються **після** створення посилання.
#### valueChanges()

Отримує лише дані. ID втрачається.

```ts
getNotes() {
  // Повертає Observable<any[]>
  return this.afs.collection('notes').valueChanges();
}
```
#### snapshotChanges()

Отримує дані разом з ID та іншою метаінформацією. Потребує додаткової обробки через `.pipe(map(...))`.

```ts
import { map } from 'rxjs/operators';

getNotesWithIds() {
  // Повертає Observable з метаданими
  return this.afs.collection('notes')
  .snapshotChanges()
  .pipe(
    map(actions => {
      return actions.map(a => {
        const data = a.payload.doc.data() as any; 
        // Витягуємо дані
        const id = a.payload.doc.id;             
        // Витягуємо ID
        return { id, ...data };                  
        // Об'єднуємо їх
      });
    })
  );
}
```

#### valueChanges() vs snapshotChanges()

`valueChanges()`: Простий спосіб. Повертає `Observable` з масивом даних (`Observable<Note[]>`). Але ви втрачаєте ID документа та іншу метаінформацію.

`snapshotChanges()`: Просунутий спосіб. Повертає `Observable`, де кожен елемент містить не тільки дані, але й ID документа та іншу метаінформацію. Це найчастіший вибір, якщо вам потрібен ID для подальших операцій (оновлення, видалення).

#### get()

Для одноразового читання даних (не в реальному часі). Повертає `Observable`, який завершується після першого отримання даних.

### Запис та зміна даних

**Операції запису повертають [[Promise]]**: Додавання, оновлення та видалення — це одноразові дії. Вони не є потоком даних, тому повертають `Promise`, який ви можете обробити через `.then()` або [[async, await|async/await]].

#### add()

Додає новий документ в колекцію з автоматично згенерованим ID. Викликається на об'єкті колекції.

```ts
async createNote(title: string) {
  const itemsCollection = this.afs.collection('notes');
  const newDoc = await itemsCollection.add({ title: title, content: '' });
}
```

#### set()

Створює або повністю перезаписує документ. Викликається на об'єкті документа. Якщо документа не існує, він буде створений. Якщо існує — всі його старі дані будуть видалені і замінені новими.

```ts
const userDoc = this.afs.doc('users/user123');
await userDoc.set({ name: 'Jane', role: 'admin' });
```

#### update()

Частково оновлює існуючий документ. Якщо документа не існує, поверне помилку.

```ts
const userDoc = this.afs.doc('users/user123');
await userDoc.update({ lastLogin: new Date() });
```

#### delete()

Видаляє документ.

```ts
async deleteNote(id: string) {
  const noteDoc = this.afs.doc(`notes/${id}`);
  await noteDoc.delete();
}
```

