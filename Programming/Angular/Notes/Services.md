
Сервіси Angular використовуються для інкапсуляції даних, здійснення HTTP-запитів або виконання будь-якого завдання, яке не пов'язане безпосередньо з відображенням даних (на думку індуса).

Створення Angular Service:
```bash
ng g service services/todos
```

Сервіс не створює для себе окрему папку, а просто створює два файла: `service.ts` і `service.spec.ts`.

Для сервісів використовується декоратор `@Injectable`.

```ts title:todo.service.ts
@Injectable({  
	providedIn: 'root'  
})  
export class Todos {  
	constructor() { }  
}
```

Ми можемо використовувати сервіс в одному з компонентів, або в багатьох. Якщо ми хочемо використовувати сервіс тільки в одному з компонентів ми:
- добавляємо в декоратор компонента(`@Component`) `providers: [TodosService]`
- Можемо забрати `providedIn: 'root'` з `@Injectable`

Для того щоб використати сервіс його потрібно заінджектити в компонент:
```ts title:todos.component.ts
export class TodosComponent {  
    todoService = inject(TodosService);   
}
```

потім його можна ініціалізувати за допомогою `OnInit` і використати через сигнал:
```ts title:todos.component.ts
export class TodosComponent implements OnInit {  
    todoService = inject(TodosService);  
  
    todoItems = signal<Array<Todo>>([]);  
  
    ngOnInit(): void {  
        console.log(this.todoService.todoItems);  
        this.todoItems.set(this.todoService.todoItems);  
    }  
}
```
