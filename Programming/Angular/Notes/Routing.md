Angular — це односторінковий додаток. Використовуючи Routes, ви все ще можете визначити різні сторінки, до яких користувач може перейти. 

Браузер завантажує лише пакети, пов'язані з маршрутом, до якого користувач отримав доступ.

### Створення Route для home component:
```ts title:app.routes.ts
export const routes: Routes = [{  
  path: '', // if we are at the top of root  
  pathMatch: 'full', //required for using empty route  
  loadComponent: ( ) => {  
    return import('./home/home').then(m => m.Home); 
  }  
}];
```

Потім можна забрати `import Home Component` в `app.ts` і використати `{html}<router-outlet/>`.

#### Запис з loadComponent(Lazy Loading - Ліниве завантаження):
```ts
loadComponent: ( ) => {  
    return import('./home').then(m => m.Home); 
  }
```
`loadComponent`: Це функція, яка динамічно імпортує компонент (використовуючи синтаксис `import()` ES-модулів).

`import('./components/notes/notes.component')`: Це асинхронна операція, яка завантажує JavaScript-файл з кодом `NotesComponent` лише тоді, коли він потрібен.

`.then(n => n.NotesComponent)`: Після завантаження файлу, ми вказуємо, який саме компонент потрібно використовувати з цього модуля.

#### Запис з component (Eager Loading - Жадібне завантаження):
```ts title:app.routes.ts
export const routes: Routes = [{
    path: 'about',
    component: AboutComponent
}
}];
```

`AboutComponent` (і весь його код, а також усі його залежності) буде завантажений одразу, коли додаток Angular запускається. Він є частиною початкового пакета JavaScript.

Angular збирає весь код компонента `AboutComponent` (та його імпорти) у початковий bundle JavaScript під час компіляції.

#### **Створення нового Route для todos:**
```ts title:app.routes.ts
export const routes: Routes = [  
  {  //HOME ROUTE
    path: '', // if we are at the top of root  
    pathMatch: 'full', //required for using empty route  
    loadComponent: () => {  
      return import('./home/home').then(m => m.Home);  
    }  
  },  
  {  //TODOS ROUTE
    path: 'todos',  
    loadComponent: () => {  
      return import('./todos/todos').then(m => m.Todos);  
    },  
  }  
];
```

Тепер, щоб попасти на `todos` потрібно перейти на `localhost:4200/todos`.

### Router Link

Для того щоб перейти між цими різними сторінками використовується *Router Link*.

Добавимо посилання на `todos` в `header`.
Для цього імпортуємо `RouterLink` в `header.ts`:
`{ts}imports: [RouterLink]`.

Тепер добавимо ці посилання в `header.html`:
```html title:header.html
<header>  
  <nav>
	<span routerLink="/">{{title()}}</span>  
    <ul>
	    <li routerLink="/todos">Todos</li>  
    </ul>  
  </nav>
</header>
```
