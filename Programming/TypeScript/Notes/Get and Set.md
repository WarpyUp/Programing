### Get
Для створення гетера використовується ключове слово `get`.
```typeScript
//метод
get balance(): number {
	return this._balance;
}
//виклик
console.log(account.balance);

accout.balance = 1; //помилка
```

Для статичних змінних метод Get повинен бути статичним.
```typeScript
static get activeRides (){
	return Ride-_activeRides;
	}
```

### Set
Для створення гетера використовується ключове слово `set`.
```typeScript
set balance(value: number){
	if (value < 0)
		throw new Error('Invalid value');
	this._balance = value; |
}
```
