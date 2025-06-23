Якщо ви очікуєте, що об'єкт може мати довільні властивості з певним типом значень.

`[key: string]: any; // Дозволяє будь-яку строкову властивість з будь-яким значенням`

Таких додаткових можливостей можна додати безліч.
```typeScript
// Додавання нової властивості до існуючого об'єкта  
person.city = "Львів";  
console.log(person.city);       // Львів  
```

Також їх можна видалити
```typeScript
// Видалення властивості  
delete person.isStudent;  
console.log(person.isStudent);  // undefined
```

Можна використовувати в Класі
```typeScript
class SeatAssignment {
	[seatNumber: string]: string;
}

let seats = new SeatAssignment ()
seats. A1 = 'Mosh';
seats['A1'] = 'Mosh'; // те саме шо перед тим
seats. A2 = 'John';
```
