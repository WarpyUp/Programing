Це обєкт, результат виклику методу `subscribe()` на [[Observable]]. Вона представляє активне виконання Observable.

Підписка має один важливий метод, `unsubscribe`, що не приймає аргументів і просто звільняє ресурс, утримуваний підпискою.
Це критично важливо для запобігання витоків пам'яті (memory leaks), особливо в Angular (наприклад, при переході на іншу сторінку, коли HTTP-запит все ще виконується).

```ts
const subscription = observable.subscribe(x => console.log(x)); 

subscription.unsubscribe();
```

За допомогою методу `add` можна додати підписку одну до одної, щоб потім разом для них викликати `unsubscribe()`.
```ts
subscription.add(childSubscription);
```

Підписки також мають метод `{ts}.remove(childSubscription)`, щоб скасувати додавання дочірньої підписки.

