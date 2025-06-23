
```typeScript
interface Product {
	name: string;
	price: number;
}
```

Створимо клас для наслідування.
```typeScript
class Store<T> {
	
	private _objects: T[] = [];
	
	add (obj: T): void {
		this.objects.push(obj)
	}
}
```

При наслідуванні Generic класів вказуємо в дочірньому класі також Generic праметр, який буде передаватися в батьківський.
```typeScript
class CompressibleStore<T> extends Store<T> {
	compress(){} 
}

let store = new Compressible Store<Product>();
```

Також в дочірньому класі можна обмежити передавані параметри за допомогою [[Generic Constrains]].

Якщо ми чітко знаємо з яким переданим елементом ми хочемо працювати тоді в дочіньому класі можна не вказувати Generic параметр.
```
class ProductStorel extends Store<Product>{}
```
