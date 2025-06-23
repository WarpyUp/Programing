`Subject` є особливим типом `Observable`. Він одночасно є:

1. **Observable**: Ви можете підписуватися на нього, як на будь-який інший Observable.
2. **Observer**: Ви можете передавати йому значення (за допомогою `next()`), помилки (`error()`) та сигнали про завершення (`complete()`), як до звичайного Observer.

Його головна відмінність від звичайного `Observable` полягає в тому, що `Subject` є **мультикастним**. Це означає, що всі підписники на `Subject` отримують одні й ті ж значення від одного і того ж виконання `Subject`. Звичайний `Observable` за замовчуванням є унікастним, тобто кожна нова підписка запускає власне, незалежне виконання `Observable`.

```ts
// RxJS v6+  
import { Subject } from 'rxjs';  
  
const sub = new Subject<number>();  
  
sub.next(1);  
sub.subscribe(x => {  
	console.log('Subscriber A', x);  
});  
sub.next(2); // OUTPUT => Subscriber A 2  
sub.subscribe(x => {  
	console.log('Subscriber B', x);  
});  
sub.next(3); // OUTPUT => Subscriber A 3, Subscriber B 3 (logged from both subscribers)
```

---
### BehaviourSubject і ReplaceSubject

**BehaviourSubject** — це `Subject`, який завжди випускає поточне значення (або початкове, якщо його ще не було) для нових підписників. Це означає, що нова підписка одразу отримає останнє значення, яке було надіслано, або значення, з яким `BehaviourSubject` був ініціалізований. Як дошка оголошень.

```ts
const subject = new BehaviorSubject(0);// 0 is the initial value
```

**ReplaySubject** — це `Subject`, який зберігає в буфері певну кількість останніх значень. Коли на нього підписується новий спостерігач, він миттєво отримує всі ці буферизовані значення. Розмір буфера задається в конструкторі
```ts
const subject = new ReplaySubject(3); // buffer 3 values for new subscribers
```

Ви також можете вказати часове вікно у мілісекундах, окрім розміру буфера, щоб визначити, наскільки старими можуть бути записані значення. 
```ts
const subject = new ReplaySubject(100, 500/*windowTime*/);
```

У цьому прикладі ми використовуємо великий розмір буфера 100, але параметр часового вікна лише 500 мілісекунд.
### AsyncSubject

**AsyncSubject** — це `Subject`, який передає лише останнє значення зі свого потоку, і робить це тільки після того, як потік завершиться (`complete()`). Якщо потік завершується з помилкою до того, як було надіслано будь-яке значення, або якщо `complete()` ніколи не викликається, жодне значення не буде випущено.

```ts
const subject = new AsyncSubject();
```

