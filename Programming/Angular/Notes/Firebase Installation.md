---

---
---
#### Крок 1: Створення Firebase Проекту та Конфігурація Angular
---
**Створи новий проект у Firebase Console:**

- Перейди на [Firebase Console](https://console.firebase.google.com/).
- Натисни **"Add project"** (Додати проект).
- Введи **назву проекту** (наприклад, "MyAngularNotes" або щось подібне).
- **Відключи Google Analytics** для цього проекту (для простоти, оскільки він не потрібен для твого завдання).
- Натисни **"Create project"** (Створити проект). Дочекайся його створення.
---
**Додай веб-додаток до свого Firebase Проекту:**

- Після створення проекту в консолі Firebase, ти побачиш екран огляду проекту.
- Натисни на іконку **веб-додатку** (виглядає як `</>`).
- Зареєструй свій додаток, дай йому нікнейм (наприклад, "Angular App"). **Не став галочку "Also set up Firebase Hosting"** поки що.
- Натисни "Register app".
- Ти отримаєш об'єкт JavaScript-конфігурації (`firebaseConfig`). **Скопіюй його**. Він містить ключі доступу до твого проекту Firebase.

---
**Встанови AngularFire у своєму Angular Проекті:**

- Відкрий термінал у кореневій папці твого Angular-проекту.
- Виконай команду:
```bash
ng add @angular/fire
```

---
Ця команда запитає тебе:

**Which Firebase features would you like to setup?** 
Вибери "Firestore" (використай пробіл, щоб вибрати, Enter, щоб продовжити).

**Enable Gemini in Firebase features?** 
No

**Allow Firebase to collect CLI and Emulator Suite usage and error reporting information?** 
No

**Enter authorisation code:**

**Would you like to setup a proxy for the Firebase Emulator Suite?** 
Можеш відповісти `No` для простоти зараз.

**Please provide your Firebase project id. (Found in project settings)** 
Введи ID свого проекту Firebase (ти можеш знайти його в консолі Firebase: `Project settings` -> `Project ID`).

**Please paste the content of your Firebase web config object here.**  
Встав сюди скопійований раніше `firebaseConfig` об'єкт, включаючи фігурні дужки `{}`.

`ng add @angular/fire` автоматично:
- Встановить необхідні npm-пакети (`firebase`, `@angular/fire`).
- Додасть конфігурацію Firebase у твій файл `src/environments/environment.ts`.
- Імпортує та ініціалізує необхідні модулі (`provideFirebaseApp`, `provideFirestore`) у твоєму `app.module.ts` або `main.ts` (залежно від версії Angular та того, чи використовуєш ти standalone компоненти).

---

Після виконання цих кроків, твій Angular-додаток буде знати, як підключитися до твого проекту Firebase. Ти зможеш почати взаємодіяти з Cloud Firestore.