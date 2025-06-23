
```typeScript
interface Result<T> {
	data: T | null,
	error: string | null
}

function fetch<T>(url: string): Result<T> {
	return {data: null, error: null };
}
```
Якщо в функції використовуємо Generic Return тоді і сама функція має бути Generic.