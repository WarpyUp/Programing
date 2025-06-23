Дозволяє задати декілька можливих типів для змінної, або параметра функції.
```typeScript
let a: string | number; 

a = "2";  
//or  
a = 2;
```

Також можна використати це в функції:
```typeScript
function func(b: number | string): number {  
    //Narrowing  
    if(typeof b === "number")  
        return b * 2;  
    else   
		return 0;  
}
```
Для того щоб уникнути помилок використовуєм прийом Narrowing і перевіряємо тип.

Можна використовувати в параметрах повернення функції.