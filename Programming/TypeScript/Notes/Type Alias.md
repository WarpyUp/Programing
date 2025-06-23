Використовується, щоб створити власний тип, чим він відрізняється від класу поки хз.

Приклад:
```typeScript
type Employee = { 
	id: number,
	name: string,
	age?: number,
	retire: (date: Date) => void
}
```

і потім створюємо обєкт

```typeScript
let employee: Employee = {  
    id: 1,  
    name: "Josh",  
    retire: (date: Date) => {console.log(date)}  
}
```
