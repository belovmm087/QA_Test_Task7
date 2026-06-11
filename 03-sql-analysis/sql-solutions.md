# SQL решения

## Задача 1. Вторая по величине уникальная зарплата

Условие:
Дана таблица Employee (id int PK, salary int).
Необходимо вернуть вторую по величине уникальную зарплату.
Если такой зарплаты нет, вернуть NULL.

```sql
SELECT (
    SELECT DISTINCT salary
    FROM Employee
    ORDER BY salary DESC
    OFFSET 1
    LIMIT 1
) AS SecondHighestSalary;
```

---

## Задача 2. Поиск дублирующихся email

Условие:
Дана таблица Person (id int PK, email varchar).
Необходимо найти все email-адреса, которые встречаются более одного раза.

```sql
SELECT email
FROM Person
GROUP BY email
HAVING COUNT(*) > 1;
```

---

## Задача 3. Клиенты без заказов

Условие:
Даны таблицы Customers (id int PK, name varchar)
и Orders (id int PK, customerId int FK).

Необходимо вернуть всех клиентов, которые ни разу не делали заказ.

```sql
SELECT c.name AS Customers
FROM Customers c
LEFT JOIN Orders o
    ON c.id = o.customerId
WHERE o.id IS NULL;
```
