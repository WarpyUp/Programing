
Angular Pipes – це простий спосіб трансформувати значення в шаблонах Angular. 

Їх можна використовувати для форматування даних, таких як дати, валюта, текст тощо, перед відображенням. 
Наприклад, можна використати Pipe для перетворення дати на певний формат або для переведення тексту у верхній регістр.

### Вбудовані Pipes

Існують Angular [Buit-In Pipes](https://angular.dev/guide/templates/pipes)

Наприклад вбудований `UpperCasePipe`:
```html
<p>{{ value_expression | uppercase }}<p/>
```
Перед використанням потрібно імпортувати в компоненту

### Створення свого Pipe
```bash
ng g pipe pipes/filter-todos
```

```ts title:pipe.ts
@Pipe({  
  name: 'filterTodos'  
})  
export class FilterTodosPipe implements PipeTransform {  
  
    transform(todos: Todo[], searchTerm: string): Todo[] {  
        if (!searchTerm) {  
            return todos;  
        }  
        const text = searchTerm.toLowerCase();  
  
        return todos.filter((todo) => {  
            return todo.title.toLowerCase().includes(text);  
        });  
    }  
}
```
Функція трансформ - це функція яка виконує основну логіку pipe. Перший аргумент в функції - це те на що ми накладаємо пайп, і далі ми можемо добавляти інші аргументи.

Виклик Pipe:
```ts title:.html
@for (todo of todoItems() | filterTodos : searchTerm() : "other args"; track todo.id){

}
```
Аргументи перелічуємо через `:`

