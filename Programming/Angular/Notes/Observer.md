Observere -  це об'єкт з набором функцій зворотного виклику (callback functions), які Observable буде викликати, коли випромінює нові дані.

**Основні методи Observer:**
- `next(value)`: Викликається щоразу, коли Observable випромінює нове значення.
- `error(err)`: Викликається, якщо Observable стикається з помилкою.
- `complete()`: Викликається, коли Observable завершив свою роботу і більше не випромінюватиме значень.

```ts
const observer = {
  next: x => console.log('next value: ' + x),
  error: err => console.error('error: ' + err),
  complete: () => console.log('complete'),
};
```

Щоб його викликати потрібно підписатись на [[Observable]] потік:
```ts
observable.subscribe(observer);
```

Спостерігачі в RxJS також можуть бути частковими. Якщо ви не надаєте один з колбеків, виконання Observable все одно відбуватиметься нормально, за винятком того, що деякі типи сповіщень будуть ігноруватися, оскільки вони не мають відповідного колбека у Спостерігачі.

```ts
observable.subscribe(x => console.log('next value: ' + x));
```
В цьому прикладі викликається тільки `next()`.
