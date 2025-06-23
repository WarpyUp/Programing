**Generic клас** — це клас, який може працювати з різними типами даних, не знаючи їх заздалегідь.

Він використовує змінні типу (часто позначаються як `T`, `K`, `V` тощо) як параметри, дозволяючи створювати гнучкіші та багаторазово використовувані компоненти. 
Це як функція, яка приймає не значення, а _тип_ як аргумент.

Оголошується з параметрами типу в кутових дужках (`<>`) після імені класу.
```typeScript
class Storage<T> {
    private items: T[] = []; // Масив елементів типу T
    
    addItem(item: T): void {
        this.items.push(item);
    }
    
    getItem(index: number): T | undefined {
        return this.items[index];
    }
    
    getAllItems(): T[] {
        return this.items;
    }
}
```

Можна використати декілька параметрів - `class Storage<T, V>`

Про наслідування Generic Classes - [[Extending Generic Classes]]
