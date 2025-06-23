
**Event Listener** - це спеціальний механізм (або функція) у вашому коді, який "слухає" або "чекає" на певну дію (подію), що відбувається на конкретному елементі веб-сторінки.

Коли подія, на яку ми "слухаємо", відбувається, цей обробник автоматично запускається і виконує код (функцію), який ми йому вказали.

В Angular, зв'язування подій `{ts}(event)="statement()"` є способом додавання таких обробників подій до елементів у вашому шаблоні.

### Code
Коли натиснута люба кнопка всередині `input` викликається функція `keyUpHandler`.
```html title:html
<!-- call a function on key up -->
<input type="text" (keyup)="keyUpHandler()">
```
```ts title:ts
class MyComponent {
	keyUpHandler () {
		console. log('user typed something in the input');
}
```

Але якщо ми хочемо передати `event` в функцію, щоб дізнатись натиснуту кнопку то робимо ось так:

```html title:html
<!-- call a function on key up with the even -->
<input type="text" (keyup)="keyUpHandler($event)">
```
```ts title:ts
class MyComponent {
	keyUpHandler (event: KeyboardEvent) {
		console. log(`user typed ${event.key}`);
}
```

Важливо замітити, що при виводі використовуються косі лапки, а не звичайні, через [[Template String]]. Як знати що цей івент іменно `KeyboardEvent` хз.
