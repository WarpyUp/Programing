**FirestoreDataConverter** — це, по суті, ваш персональний "перекладач" для Firestore. Він є об'єктом, який точно знає, як перетворити дані з формату вашого додатка (наприклад, TypeScript клас `Note` з полем `Date`) у формат, зрозумілий для Firestore (`Timestamp`), і — що найголовніше — навпаки.

Використовується тільки з [[Функціональний API]].

Конвертер — це об'єкт типу FirestoreDataConverter з двома обов'язковими методами: `toFirestore` і `fromFirestore`.

## Навіщо він потрібен? (Ключові переваги)

- **Автоматична конвертація:** Автоматично перетворює `Timestamp` в `Date`, `enum` в `string` тощо.
- **Типобезпека:** Дозволяє працювати з чітко типізованими об'єктами (`Note`) замість загального `DocumentData`.
- **Чистий код:** Прибирає логіку конвертації з ваших сервісів, роблячи методи (`getNotes`, `getNoteById`) дуже простими та читабельними.
- **Централізована логіка:** Вся логіка перетворення даних для однієї сутності знаходиться в одному місці. Не потрібно дублювати код.

Один і той самий конвертер можна використовувати для отримання колекції (`collectionData`), одного документа (`docData`) та для складних запитів (`query`).

Вказуйте тип даних для конвертера `FirestoreDataConverter<Note>`, щоб отримати повну підтримку типів від TypeScript.
## Створення

1. **Створити об'єкт конвертера:** Написати об'єкт з методами `toFirestore` та `fromFirestore`. Найкраще винести його в окремий файл, наприклад `note.converter.ts`.
2. **Імпортувати його:** Імпортувати ваш конвертер у сервісі, де ви працюєте з Firestore.
3. **Застосувати `.withConverter()`:** При створенні посилання на колекцію чи документ, викликати метод `.withConverter()` і передати йому ваш об'єкт конвертера.

### Код

```ts
export const noteConverter: FirestoreDataConverter<Note> = {  
	toFirestore(note: Note): DocumentData {
        return {  
            content: note.content,  
            createdAt: note.createdAt,  
        };  
    },  
    
    fromFirestore(snapshot: QueryDocumentSnapshot): Note{ 
        const data = snapshot.data(); 
        return {  
            id: snapshot.id, //ID зі snapshot   
            content: data['content'],  
            createdAt: data['createdAt']?.toDate(), 
            // Конвертуємо Timestamp в Date  
        } as Note;  
    }  
};
```

### toFirestore(data)

Викликається коли ви записуєте дані в Firestore (`addDoc`, `setDoc`, `updateDoc`).

Бере об'єкт вашого додатка (наприклад, екземпляр класу `Note`) і перетворює його в простий JavaScript об'єкт, який Firestore може зберегти.

Часто тут не потрібно нічого робити, оскільки Firestore сам вміє перетворювати `Date` в `Timestamp` під час запису.

### fromFirestore(snapshot)

Викликається коли ви читаєте дані з Firestore (`collectionData`, `docData`, `getDoc`).

Бере `snapshot` (знімок документа з Firestore) і перетворює його на екземпляр вашого TypeScript класу або інтерфейсу. Це найважливіша частина.

Оскільки `fromFirestore` отримує `snapshot`, який містить `.id`, вам більше не потрібно використовувати опцію `{ idField: 'id' }` у `collectionData`. Конвертер робить це за вас.

### Використання

```ts
const notesCollection = collection(this.firestore, 'notes').withConverter(noteConverter); 

return collectionData(notesCollection);
```

