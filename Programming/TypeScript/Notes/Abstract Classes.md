Абстрактний клас - це "креслення" (blueprint) для інших класів. Він не може бути створений безпосередньо (ви не можете зробити `new AbstractClass()`). 
Його основна мета – бути базовим класом для успадкування.

Може містити `abstract` методи, які не мають реалізації в самому абстрактному класі. 
Будь-який клас, що успадковує абстрактний клас, повинен реалізувати ці `abstract` методи. 


```typeScript
abstract class Figure {
    abstract calculateArea(): number; 
    display(): void { 
	    console.log("Я фігура."); 
    } 
}

class Circle extends Figure {
    radius: number = 5;
    calculateArea(): number { 
	    return Math.PI * this.radius**2; 
    } 
}

let fig = new Figure(); // ПОМИЛКА: Не можна створити екземпляр
```
