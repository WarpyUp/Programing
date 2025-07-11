**Firebase** – це платформа для розробки мобільних і веб-додатків, розроблена Google. Це, по суті, **Backend-as-a-Service (BaaS)**.

**Він замінює потребу писати власний бекенд.** Замість того, щоб налаштовувати сервери, бази даних, API для аутентифікації тощо, Firebase надає ці готові сервіси, якими ви керуєте через консоль Firebase і взаємодієте через SDK (Software Development Kit) у своєму фронтенді.

В Angular є офіційна бібліотека, яка робить інтеграцію з Firebase дуже зручною – це **AngularFire**. Вона надає сервіси Firebase у вигляді RxJS Observables, що ідеально вписується в твої вже існуючі знання.

Для побудови додатку є таке:
- Auth 
- Cloud Storage
- Cloud Functions
- Hosting
- Cloud Firestore
- Realtime Database
- Machine Learning
- Extensions


#### **Ключові сервіси Firebase, які тобі знадобляться з Angular:**

#### **Cloud Firestore (або Realtime Database):**

Гнучка, масштабована база даних NoSQL.

Це твій основний спосіб зберігати, синхронізувати та отримувати дані для твого Angular-додатку. Вона має потужні можливості реального часу.

Дані організовані в "колекції" (collections) і "документи" (documents). Документ – це, по суті, об'єкт JSON.

#### Authentication (Firebase Auth):

Повноцінне рішення для аутентифікації користувачів.

Дозволяє користувачам реєструватися, входити в систему та керувати своїми обліковими записами за допомогою різних методів (електронна пошта/пароль, Google, Facebook, Twitter тощо). Це критично для будь-якого додатка, що працює з користувачами.

#### Hosting:

Швидкий і безпечний хостинг для твоїх веб-додатків, статичних і динамічних.

Дозволяє легко розгортати твій Angular-додаток в Інтернеті за допомогою однієї команди.

_(Інші корисні сервіси, які можна вивчити пізніше):_

**Cloud Storage:** Для зберігання файлів (зображень, відео, документів).
**Cloud Functions:** Для написання бекенд-коду, який виконується на серверах Google (бессерверні функції), і реагує на події Firebase або HTTP-запити.