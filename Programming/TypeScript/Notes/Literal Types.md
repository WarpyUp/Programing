
Дає можливість використати тип який буде містити тільки певні значення.

`let quantity: 50 | 100 = 50;`

дає можливість записати значення 50 або 100.

Також можна створити новий тип:
```typeScript
type Quantity = 50 | 100;  
let quantity: Quantity = 50;  
  
type Metric = "cm" | "inch";  
let metric: Metric = "cm";
```

Можуть бути різні типи:
`type Example = 50 | "cm";`