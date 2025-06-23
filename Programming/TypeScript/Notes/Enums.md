
Це перелік іменованих значень (Назав, значення).

```TypeScript
enum Size {
		Small = 's',
		Medium = 'm',
		Large = 'l'
	};
	let MySize: Size = Size.Small;
```

Якщо використовувати `const enum`  тоді компілятор буде оптимізованіше це компілювати.

By default, enums begin numbering their members starting at 0. 
You can change this by manually setting the value of one of its members. For example, we can start the previous example at 1 instead of 0

Ми можемо написати отак:

```TypeScript
enum Size {
		Small = 1,
		Medium,
		Large
	};
```

тоді компілятор автоматично призначить `Medium = 2, Large = 3.` 