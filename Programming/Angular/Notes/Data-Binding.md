
**Data Binding** (зв'язування даних) є однією з фундаментальних концепцій в Angular, яка дозволяє синхронізувати дані між компонентом (логікою вашого додатку) та його шаблоном (HTML, що відображається користувачеві).

### Data-Binding with Signals
```ts
import { Component, signal } from '@angular/core';
@Component({
	・・・,
	template:`
		‹p> Var's value: {{ myVar() }}</p>
	`
})
class MyComponent {
	myVar = signal('some value');
	//або вказати явно за допомогою [[Generic Classes|generic]]
	myVar = signal<string>('some value');
	//set value
	myVar.set("new value");
}
```
Індус рекомендує користуватися тільки сигналами
### Data-Binding without Signal(traditional way)
```ts
import { Component } from '@angular/core';
@Component({
	・・・,
	template:`
		‹p> Var's value: {{ myVar }}</p>
	`
})
class MyComponent {
	myVar = 'some value';
}
```
Не рекомендується на нових версіях ангуляр.

### Види передавання даних

#### Інтерполяція (Interpolation): 
Використовується для відображення строкових значень змінних або результатів виразів у HTML. Синтаксис:
```ts
 ⁠{{ expression }}
```

#### Зв'язування властивостей (Property Binding): 

Використовується для встановлення значень властивостей HTML-елементів або директив. Синтаксис: ⁠
```ts
[property]="expression"
//наприклад
<button [disabled]="isDisabled">Натисни мене</button>
```

#### Двостороннє звязування(ngModel)

ngModel - це директива в Angular, яка використовується для реалізації двостороннього зв'язування даних у формах. 

Це означає, що зміни в елементі введення (наприклад, в текстовому полі або чекбоксі) автоматично оновлюють відповідну властивість у вашому компоненті, і навпаки, зміни у властивості компонента автоматично оновлюють відображення в елементі введення.
```html title:.html
<input type="checkbox" [checked]="isChecked" [(ngModel)]="isChecked">
```
```ts title:.ts
export class TodoItemComponent {  
    isChecked: boolean = false;  
}
```

#### Табличка

| Тип зв'язування          | Напрямок             | Синтаксис              | Призначення                                               |
| ------------------------ | -------------------- | ---------------------- | --------------------------------------------------------- |
| Інтерполяція             | Компонент -> Шаблон  | ⁠`{{ ... }}`           | Вивід текстових значень/виразів                           |
| Зв'язування властивостей | Компонент -> Шаблон  | ⁠`[prop]="value"`      | Встановлення властивостей елементів/директив              |
| Зв'язування атрибутів    | Компонент -> Шаблон  | ⁠`[attr.attr]="value"` | Встановлення атрибутів елементів (особливо нестандартних) |
| Зв'язування подій        | Шаблон -> Компонент  | ⁠`(event)="handler()"` | Реагування на події DOM, виклик методів                   |
| Двостороннє зв'язування  | Компонент <-> Шаблон | ⁠`[(ngModel)]="prop"`  | Синхронізація даних в обох напрямках (часто для форм)     |



### Передавання інформації з одного компоненту в інший

Greeting очікує інпут
```ts title:greetings.ts
export class Greeting {  
  message = input('Default Input');  
  // or can be
  message = input.required();
}
```
і виводить його
```html title:greeting.html 
<p>{{message()}}</p>
```

Home створює сигнал на передачу
```ts title:home.ts
export class Home {  
  messageHome = signal("Message from Home to Greetings");  
}
```
і передає його 
```html title:home.html 
<app-greeting [message] = "messageHome()" />
```

