Створюємо тип які має всі параметри інтерфейсу, але замінює їх на `readonly`.
```typeScript
interface Product {
	name: string;
	price: number;
}

type ReadOnlyProduct = {
	readonly [K in keyof Product]: Product [K];
}
```

Це можна зробити використовуючи Generic
```typeScript
type ReadOnly<T> = {
	readonly [K in keyof T]: T[K];
}

type Optional<T> = {
	[K in keyof T]?: T[K];
}

type Nullable<T> = {
	[K in keyof T]: T[K] | null;
}
```

Ці типи дуже корисні тому вони вбудовані в TypeScript під назвою [[Utility Types]]. 