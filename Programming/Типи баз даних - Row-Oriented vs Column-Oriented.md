
#### **1. Row-Oriented Databases (Рядково-орієнтовані БД)**
- **Зберігання:** дані зберігаються по рядках.
- **Переваги:**
    - Швидкі вставки, оновлення та пошук повних записів.
    - Добре підходять для OLTP-систем (Online Transaction Processing).
- **Недоліки:**
    - Неефективні при аналітичних запитах, де потрібна лише частина стовпців.
- **Типові завдання:** обробка транзакцій, CRM, банківські системи.
- **Популярні приклади:** PostgreSQL, MySQL, Oracle, Microsoft SQL Server.
#### **2. Column-Oriented Databases (Стовпцево-орієнтовані БД)**
- **Зберігання:** дані зберігаються по стовпцях.
- **Переваги:**
    - Ефективні при аналітичних запитах (читання вибіркових стовпців).
    - Добре підходять для OLAP-систем (Online Analytical Processing).
- **Недоліки:**
    - Неоптимальні для частих вставок і оновлень окремих записів.
- **Типові завдання:** бізнес-аналітика, звітність, прогнозування.
- **Популярні приклади:** Snowflake, Google BigQuery, Amazon Redshift.

### **Порівняння OLTP vs OLAP**

| Критерій             | OLTP                      | OLAP                     |
| -------------------- | ------------------------- | ------------------------ |
| Призначення          | Обробка транзакцій        | Аналітика та звітність   |
| Тип бази даних       | Row-oriented              | Column-oriented          |
| Операції             | Вставка, оновлення, пошук | Вибірка даних, агрегації |
| Завантаження даних   | По запису                 | Пакетно                  |
| Прикладне середовище | CRM, ERP, онлайн-сервіси  | BI-системи, звітність    |
