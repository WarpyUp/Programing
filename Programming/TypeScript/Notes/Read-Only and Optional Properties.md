For a **constant** value that **never changes**, the best practice would be to make it static readonly. This approach has two benefits:
1. **static** - The property belongs to the class itself rather than each instance, saving memory because it's not duplicated across instances.
2. **readonly** - Ensures the value cannot be modified after initialization.

```typeScript
class Example {
	public static readonly placeholder: string = 'Just a placholder';

	public someFuncton(): void {
		console.log(Example.placeholder);
	}
}
```
Також не дає можливості змінити значення поля. Значення можна записати тільки в конструкторі.
```typeScript
class Account {
	readonly id: number; 
}
```


**Optional Properties**
```typeScript
class Account {
	id?: number; 
}
```

