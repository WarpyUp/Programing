Кроки щоб підключити API:
1. Provide HTTP module/providers in the app config using `provideHttpClient()`
2. Inject the `HttpClient` service
3. Use the `http` methods

`HttpClientModule` - це вбудований [[Modules Angular|модуль]].


**1.** Записуєм `HttpClient` в `providers`:
```ts title:app.component.config.ts
export const appComponentConfig: ApplicationConfig = {  
  providers: [  
      provideBrowserGlobalErrorListeners(),  
      provideHttpClient(), //ОТУТ 
      provideZoneChangeDetection({ eventCoalescing: true }),  
      provideRouter(routes)  
  ]  
};
```

**2.** Потім інджектимо його в сервіс:
```ts title:todos.service.ts
export class TodosService {  
    httpClient: HttpClient = inject(HttpClient);
}
```

**3.** Використовуємо get щоб зробити API call
```ts title:todos.service.ts
export class TodosService {  
    httpClient: HttpClient = inject(HttpClient);
	    getTodosFromAPI() {
        const url = `https://jsonplaceholder.typicode.com/todos`;
        return this.http.get<Array<Todo>>(url);
    }	
}
```

і викликаємо ту функцію в компоненті
```ts title:todos.component.ta
ngOnInit(): void {  
    this.todoService.getTodosFromAPI().pipe(  
        catchError((error: Error) => {  
            console.log(error);  
            throw error;  
        })  
    ).subscribe(todos => {  
        this.todoItems.set(todos);  
    })  
}
```
повертає [[Observable]] з [[RxJS]].




