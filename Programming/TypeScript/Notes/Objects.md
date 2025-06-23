## Literal Objects

`let employee = {id: 1};`

Так можна створити обєкт.

Також можна явно вказати всі поля обєкту:
```typeScript
let employee: {
	id: number,
	name: string,
	age?: number
} = {id: 1, name: "Josh"};
```

Використовуємо ? щоб зробити поле не обовязковим для заповнення.

Якщо ми хочемо заборонити зміну параметра обєкта потрібно використати модифікатор `readonly`.

Для того щоб добавити метод в цей вид запису обєкта потрібно:
```typeScript
let employee: {
	readonly id: number,
	name: string,
	age?: number,
	retire: (date: Date) => void
```
але потім цей метод потрібно визначити
```typeScript
} = {
	id: 1, 
	name: "Josh",
	retire: (date: Date) => {
		console.log(date);
	}
}
```

Викликати можна:
```typeScript
employee.name = "Josh";
// або
employee["name"] = "Josh";
```
