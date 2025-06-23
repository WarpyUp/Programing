Директиви Angular дозволяють додавати додаткову поведінку до елементів у додатках Angular.

Приклади директив:
1. Components - всі компоненти є директивами.
2. Attribute directives - змінюються деякі речі в вже існуючих Html елементах.
3. Structural directives - добавляють або забирають деякі речі з DOM на основі певних умов.

[[Структурні Директиви|Вбудовані Directives]]


### Створення власних Directives:
```bash
ng g directive directives/highlight-completed-todo
```

Прописуємо клас своєї директиви:
```ts title:highlight-completed-todo.ts
@Directive({  
  selector: '[appHighlightCompletedTodo]'  
})
export class HighlightCompletedTodo {  
    isCompleted = input(false);//отримуєм значення чи ліст виконаний  
    
    el = inject(ElementRef);//отримуємо елемент на який ми наклали цю директиву за допомогою [[Services|сервісу]] ElementRef
    
    //використовуємо effect, щоб змінити стиль
    styleEffect = effect(() => {  
        if (this.isCompleted()) {  
            this.el.nativeElement.style.textDecoration . textDecoration = 'line-through';  
            this.el.nativeElement.style.backgroundColor = '#d3f9d8'  
            this.el.nativeElement.style.color = '#6c757d' ;  
        } else {  
            this.el.nativeElement.style.textDecoration = 'none';  
            this.el.nativeElement.style.backgroundColor = '#fff';  
            this.el.nativeElement.style.color = ' #000';  
        }  
    });  
}
```

Щоб застосувати цю директиву нам потрібно скопіювати її `selector` в [[Decorators|декораторі]] і вставити її в html тег(наприклад todo list). Не забути його імпортувати в компоненту.
```html
<li appHighlightCompletedTodo>
...
```

Сюда також передаємо значення `isCompleted`
```html
<li appHighlightCompletedTodo [isCompleted]="todo().completed">
```
