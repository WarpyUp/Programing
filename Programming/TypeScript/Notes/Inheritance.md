Наслідування

**Батьківський клас:**
```typeScript
class Person{
	constructor(public firstName: string, public lastName: string){}
	
	get fullName(){
		return this.firstName + ' ' + this.lastName;
	}
	walk(){
		console.log("walking");
	}
}
```

**Дочірній клас**
Для доступу до конструктора батьківського класу використовуємо `super()`.
```typeScript
class Student extends Person {
	constructor(
	firstName: string,
	lastName: string, 
	public studentId: number){
		super(fisrtName, lastName);
	}
	takeTest(){
		//some code
	}
}
```

Важливо звернути увагу що при написання дочірнього конструктора ми не використовуємо [[Access Control Keywords]] (private, public), бо ми не створюємо нові поля в дочірньому класі а просто беремо дані і передаємо їх в батьківський.

Якщо ми не створюємо конструктор в дочірньому класі то по стандарту викликається конструктор батьківського класу.
```typeScript
class Teacher extends Person {}
let teacher = new Teacher ('John', 'Smith');
```

**Method Overriding**
Для перевизначення методів використовується ключове слово `override`.
```typeScript
class Teacher extends Person {
	override get fullName(){
		return 'Profesor' + 
		this.firstName + ' ' 
		+ this.lastName;
	}
}
```
В цьому прикладі ми добавляємо слово 'Profesor' перед виводом імені.

Але цей код можна спростити, бо код для виводу імені ми писали в батьківському класі тому можемо до нього звернутись за допомогою `super`.
```typeScript
class Teacher extends Person {
	override get fullName () {
		return 'Professor' + super.fullName;
	}
}
```

Ми можемо перевизначити методи без ключового слова `override`, але це погана практика. Чому скажуть пізніше

