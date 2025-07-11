
**Control Flow Blocks** - це новий синтаксис у шаблонах, який спрощує умовне відображення та повторення елементів без використання структурних директив на кшталт `*ngIf`, `*ngFor` та `*ngSwitch`.

Вони пропонують більш читабельний синтаксис, кращу продуктивність та нові можливості порівняно зі [[Структурні Директиви|структурними директивами]].

Вони не є [[Directives|директивами]] в традиційному сенсі, а спеціальними синтаксичними конструкціями шаблонів, які обробляються компілятором Angular набагато ефективніше. Вони не використовують `<ng-template>` і не потребують імпортів модулів (наприклад, `CommonModule`).
## **@for**

Новий шаблон для циклу:
```html
@for (item of items; track item.id) {
  <div>{{ item.name }}</div>
}
```

#### track 

track — це інструкція для Angular, яка допомагає йому ефективно оновлювати списки. Замість того, щоб руйнувати і створювати заново весь список у HTML при будь-якій зміні, Angular використовує `track`, щоб зрозуміти, які елементи залишились, які зникли, а які додалися. 

1. Найкращий варіант - це надати в track унікальний ідентифікатор, наприклад `id`.

2. Якщо ваші об'єкти не мають унікального `id`, але вони є незмінними (immutable), ви можете відстежувати їх за посиланням на сам об'єкт.

3. Крайній випадок який можна використати це `$index`.

`$index` — це спеціальна змінна циклу, що містить порядковий номер елемента (0, 1, 2...).

## **@if**

Нова шаблон для умов (аналог ngIf):
```html
@if (isVisible) {
  <p>Hello</p>
}@else {
  <p>Bye</p>
}
```

## **@switch, @case, @default**

для умов з багатьма варіантами (аналог ngSwitch):
```html
@switch (status) {
  @case ('loading') { <p>Завантаження...</p> }
  @case ('error') { <p>Помилка!</p> }
  @default { <p>Готово!</p> }
}
```
