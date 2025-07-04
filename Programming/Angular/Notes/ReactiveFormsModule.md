**ReactiveFormsModule** — це частина фреймворку Angular, яка дозволяє створювати та керувати формами у [[Реактивне Програмування|реактивному]] стилі. Він надає розробникам повний контроль над станом, структурою та валідацією форм.

Уявіть, що ваша HTML-форма — це телевізор, а Reactive Form — це пульт дистанційного керування.

Замість того, щоб підходити до телевізора і натискати кнопки на ньому (`<input>`, `<textarea>`), ви керуєте всім з одного місця — з вашого "пульта" в TypeScript-коді. Ви з пульта кажете, які "канали" (поля) існують, яка в них "гучність" (значення), і чи працюють вони взагалі (валідація).

Це "модельно-орієнтований" підхід: ви створюєте модель форми в коді, а HTML-шаблон просто відображає цю модель.

#### Чому їх варто використовувати?

- **Контроль у TypeScript:** Вся логіка (значення, валідація, стан) знаходиться в одному місці — у вашому `.ts` файлі. Це робить код чистим і передбачуваним.
- **Легке тестування:** Ви можете тестувати логіку вашої форми, не запускаючи користувацький інтерфейс.
- **Динамічність:** Дуже легко додавати або видаляти поля форми програмно.
- **Чітка валідація:** Правила валідації (наприклад, "це поле обов'язкове" або "має бути email") пишуться як прості функції в коді.
- **Масштабованість:** Ідеально підходять для великих і складних форм.

---
## Основні будівельні блоки

### FormControl — Одне поле вводу.

Це найменша одиниця. Вона представляє один елемент керування: `<input>`, `<textarea>`, `<select>`.

Створюється так: 
```ts
new FormControl('початкове значення', [правила валідації]);
```

Приклад: 
```ts
title: new FormControl('', Validators.required)
```
 — ми створили контроль для заголовка, сказали, що він спочатку порожній і є обов'язковим.

### FormGroup — Група полів.

Це об'єкт, який об'єднує кілька `FormControl` під одним дахом. Він представляє всю форму або її частину (наприклад, групу полів "адреса").

Створюється так: 
```ts
new FormGroup({ 
	title: new FormControl('', Validators.required), 
	content: new FormControl('')
});
```

має властивість .invalid, можна використати в html:
```html
<button [disabled]="newForm.invalid">
```
Якщо форма не валідна, тоді кнопка не активна

### FormArray — Динамічний список полів.

Це масив, який може містити `FormControl` або `FormGroup`. Ідеально підходить, коли ви не знаєте наперед, скільки полів у вас буде (наприклад, "додати ще один номер телефону" або "додати ще один інгредієнт").

### **FormBuilder**

FormBuilder в Angular – це допоміжний сервіс в рамках модуля Reactive Forms, який спрощує створення та керування елементами керування (контролами) та групами форм. Він надає більш лаконічний та читабельний спосіб створення складних форм порівняно з ручним створенням екземплярів класів FormControl, FormGroup та FormArray.

Найкраще можна показати що це таке на прикладі.

#### Впровадження formBuilder
```ts
constructor(private fb: FormBuilder) {}
```

#### Без formBuilder:
```ts
this.newNoteForm = new FormGroup({ 
	title: new FormControl('', Validators.required), 
	content: new FormControl('') });
```

#### з formBuilder:
```ts
this.newNoteForm = this.fb.group({
	title: ['', Validators.required], 
	content: [''] 
	// Замість new FormControl('') 
	});
```

Як бачите, `this.fb.group()` дозволяє описати форму значно компактніше, використовуючи масиви `['початкове значення', валідатори]` замість постійного виклику `new FormControl()`. 


---
## Як впровадити

### Створити модель в TypeScript

У вашому компоненті ви створюєте екземпляр `FormGroup` або `FormControl`. Це ваша "модель" або "пульт керування".

```ts
this.newForm = new FormGroup({ ... });
```

### Зв'язати з HTML

У шаблоні ви використовуєте спеціальні директиви, щоб зв'язати HTML-елементи з вашою моделлю.
- `[formGroup]="newForm"` — для всієї форми.
- `formControlName="title"` — для конкретного поля вводу.

```html
<form [formGroup]="newForm" class="create-form">
	<input formControlName="title">
</form>
```

Для окремого вільного поля
```html
<input [formControl]="searchControl">
```
### Отримати дані

Коли користувач натискає кнопку "Зберегти", ви просто берете всі значення з вашої моделі:

```ts
const data = this.newForm.value; // Отримає об'єкт { title: '...', content: '...' }
```

### Слухати зміни (це і є "реактивність")

Ви можете в реальному часі підписатися на зміни будь-якого поля і реагувати на них.

```ts
this.newForm.get('title')?.valueChanges
	.subscribe(newTitle => {
    console.log('Заголовок змінився на:', newTitle);
});
```

