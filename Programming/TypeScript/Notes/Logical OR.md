Оператор `||` перевіряє чи значення не falsy.

Використовується так
`let a = number || 0;`

In JavaScript, the following values are considered falsy:
- `false`
- `0` (the number zero)
- `-0` (negative zero)
- `0n` (BigInt zero)
- `""` (empty string)
- `null`
- `undefined`
- `NaN` (Not-a-Number)

Якщо потрібно перевірити чи значення не null або undefined тоді використовуємо [[Nullish Coalescing Operator]].