**Декоратори** — це спеціальний синтаксис (починається з `@`), який дозволяє анотувати або модифікувати класи та їхні члени (методи, властивості, аксесори, параметри) під час розробки/компіляції. 
По суті, це функції, які "обгортають" інший код, додаючи до нього додаткову поведінку або метадані без зміни його оригінального вигляду.

Декоратори в TypeScript є експериментальною функцією. Для їх використання потрібно ввімкнути опцію `experimentalDecorators` у `tsconfig.json`.

### Class Decorator

Наслідуваний клас не отримує характеристик декоратора батьківського.

```TypeScript
function Component (constructor: Function) {
    console.log ('Component decorator called');
    constructor.prototype.uniqueld = Date.now();
    constructor.prototype.insertInDOM = () => {
        console.log( 'Inserting the component in the DOM');
    };
}

@Component
class ProfileComponent {
}
```
За допомогою декоратора ми додаємо в клас нове поле і метод. 

Ми могли би це зробити за допомогою наслідування, але декоратор це ще один метод.

### Parametrized Decorators

Ми можемо загорнути декоратор в функцію якій передати параметри і використати всередині.
```TypeScript
//Decorator factory
function Component(value: number){
	return (constructor: Function) => {
		constructor.prototype.options = value;
		constructor.prototype.uniqueld = Date.now();
		constructor.prototype.insertInDOM = () => {
			console. log('Inserting the component');
		}
	}
}

@Component(1)
class ProfileComponent {}
```

### Decorator Composition
```TypeScript
@Component
@Pipe
class ProfileComponent{}
```

Порядок виклику декораторів буде протилежний, перше викликається `Pipe`, потім `Component`.

### Method Decorators

Цей приклад показує як можна замінити метод за допомогою декоратора.
*target* - батьківський клас
*methodName* - назва методу
descriptor - сам метод, це просто поле обєкту, як має значення функції, тому descriptor.value - це сама функція

```TypeScript
function Log(target: any, methodName: string, descriptor: PropertyDescriptor){
	descriptor.value = function() {
		console.log('New Implementation');
	}
}

class Person {
	@Log
	say (message: string) {
		console.log('Person says ' + message);
	}
}
```


Цей метод показує як можна доповнити метод за допомогою декоратора, а посередині викликати оригінальну функцію.
```TypeScript
function Log (target: any, methodName: string, descriptor: PropertyDescriptor){
	const original = descriptor.value as Function;
	descriptor.value = function() {
		console.log('Before');
		original.call(this, "Message");
		console.log('After');
	}
}
```
Але тут є одна проблема - в даному випадку ми захардкодили передачу повідомлення "Message" в метод `say`. Якщо ми захочемо вручну передавати повідомлення при виклику функції то потрібно зробити так:
```TypeScript
function Log (target: any, methodName: string, descriptor: PropertyDescriptor){
	const original = descriptor.value as Function;
	descriptor.value = function(message: string) {
		console.log('Before');
		original.call(this, message);
		console.log('After');
	}
}
```
Для запуску цього коду `noUnusedParameters` має бути `false`.

Є ще одна проблема, з цьою імплементацією ми можемо використати цей декоратор тільки на методах які мають один параметр `function(message: string)`. 

Щоб зробити його універсальним потрібно написати таким чином: `function(...args: any)`. 
І викликати: `original.call(this, ...args);`

Важливо підмітити що для модифікації методів ми можемо використовувати запис тільки `function(...args: any)`, але не `(...args: any) => {}` .

### Acessor(Get, Set) Decorator 

```TypeScript
class Person {
	constructor(public firstName: string, 
	public lastName: string){}
	
	@Capitalize
	get fullName() {
		return `${this.firstName} ${this.lastName}`;
	}
}
```

`${this.firstName} ${this.lastName}` - це [[Template String]]

Визначимо декоратор `@Capitalize`:

Для цього потрібно такі ж 3 параметра `target: any, mathodName: string, descriptor: PropertyDescriptor`.

Для передачі оригінального метода використовуємо не `.value` а `.get`.

```TypeScript
function Capitalize(target: any, mathodName: string, descriptor: PropertyDescriptor){
	const original = descriptor.get;
	descriptor.get = function() {
		const result = original?.call(this);
		//some code
		return result;
	}
}
```

### Property Decorators

Напишемо декоратор до поля, який буде перевіряти мінімальну довжину пароля. Створимо клас:
```TypeScript
class User {
	@MinLength(4)
	password: string;
	
	constructor (password: string) {
		this. password = password;
	}
}
```

Створимо декоратор, потрібно тільки 2 параметра - `target: any, propertyName: string` :

```TypeScript
function MinLength(length: number){
	return (target: any, propertyName: string) => {
		let value: string;
		
		const descriptor: PropertyDescriptor = {
			get() { return value;}
			set(newValue: string){
				if(newValue.length < length)
					throw new Error('error');
				value = new Value;
			}
		};
		Object defineProperty(target, propertyName, descriptor); 
	}
}
```

### Parameter Decorator

В цьому коді ми збираємо інформацію про параметри і записмуємо її в масив.
```TypeScript
type WatchedParameter = {
	methodName: string,
	parameterIndex: number
}

const watchedParameters: WatchedParameter[] = [];

function Watch(target: any, methodName: string, parameterIndex: number){
	watchedParameters.push({
		methodName, parameterIndex
	});
}

class Vehicle {
	move(@Watch speed: number)
}
```



