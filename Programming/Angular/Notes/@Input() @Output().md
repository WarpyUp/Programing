
#### **@Input() (Батько до Дитини)**

@Input() - це декоратор, який дозволяє дочірньому компоненту отримувати дані від свого батьківського компонента.

Коли батьківська властивість змінюється, `Input` оновлюється. Це односпрямований потік даних, який проходить "зверху вниз" по дереву компонентів.

Батьківський компонент "дає" дані дочірньому.
```ts title:child.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>Привіт, {{ userName }}!</p>`
})
export class ChildComponent {
  @Input() userName: string = ''; // Дочірній очікує дані
}
```

HTML
```html
<app-child [userName]="'Іван'"></app-child>
```

---
#### **@Output() (Дитина до Батька)**

@Output() - це декоратор, який дозволяє дочірньому компоненту повідомляти свого батьківського компонента про події, що відбулися всередині дитини.

Дочірній компонент випромінює подію за допомогою `EventEmitter`, а батьківський компонент "слухає" цю подію. Це односпрямований потік даних "знизу вгору".

Дочірній компонент "каже" батькові про подію.
```ts title:child.component.ts
// 
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="notifyParent()">Натисни</button>`
})
export class ChildComponent {
  @Output() buttonClicked = new EventEmitter<number>(); // Оголошуємо подію

  notifyParent(): void {
    this.buttonClicked.emit(1); // Випромінюємо подію
  }
}
```

HTML
```html
<app-child (buttonClicked)="onChildButtonClicked()"></app-child>
```

В батьківському класі визначаємо `onChildButtonClicked()`.