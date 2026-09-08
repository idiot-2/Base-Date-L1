# Лабораторна робота 1. Робота з СУБД PostgreSQL та основи SQL

## Загальна інформація

**Здобувач освіти:** [Терещук Дмитро Олександрович]
**Група:** [31]
**Обраний рівень складності:** [1/2]

## Виконання завдань

### Список таблиць

```sql
-- Запит для отримання списку таблиць
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public'
ORDER BY table_name;
```

Результат: У базі даних створено 8 основних таблиць: categories, customers, employees, order_items, orders, products, regions, suppliers.

<img width="167" height="407" alt="image" src="https://github.com/user-attachments/assets/02f30301-8e4b-4765-90bb-7b4124149cc8" />
...

### Рівень 1
#### 1. Основні SELECT запити:
  ```sql
    -- Отримати всі записи з таблиці customers.
    SELECT
      customer_id AS ID_клієнта,
      company_name AS Назва_компанiї,
      contact_name AS Iмя_контактної_особи,
      contact_title AS Посада_контактної_особи,
      address AS Адресса,
      city AS Мiсто,
      region_id AS ID_регiону,
      postal_code AS Поштовий_індекс,
      phone AS Телефон,
      email AS Електронна_пошта,
      registration_date AS Дата_регiстрацiї,
      customer_type AS Тип_клієнта
    FROM customers;
  ```
  Результат: Отримано 15 записів клієнтів, включаючи як фізичних осіб, так і юридичні особи з різних міст України.
  <img width="1572" height="506" alt="image" src="https://github.com/user-attachments/assets/07d2ccee-506d-4557-bdca-b1eb6846b403" />

  ```sql
    -- Вивести тільки назви товарів і їхні ціни з таблиці products. --
    SELECT 
      product_name AS Назва_товару,
      unit_price AS Цiна
    From products;
  ```
  Результат: Отримано 25 записiв з назвою та цiною товарiв.
  <img width="214" height="458" alt="image" src="https://github.com/user-attachments/assets/4432a72d-11ee-4b73-a935-9fdb6c04f7ba" />

  ```sql
    -- Показати контактні дані всіх співробітників (ім'я, прізвище, телефон, email). --
    SELECT
      last_name AS Прiзвище,
      first_name AS Iмя,
      phone AS Телефон,
      email AS Електронна_пошта
    FROM employees;
  ```
  Результат: Отримано 8 записiв спiвробiтникiв з прiзвищем, iмям, номером телефону та електронною поштою.
  <img width="511" height="323" alt="image" src="https://github.com/user-attachments/assets/06bd953f-d0b6-4f92-8581-d6d875543b28" />

#### 2. Прості умови WHERE:
  ```sql
    -- Знайти всіх клієнтів з міста Київ. --
    SELECT 
      company_name AS Назва_компанiї,
      contact_name AS Iмя_контактної_особи,
      contact_title AS Посада_контактної_особи,
      address AS Адресса,
      city AS Мiсто,
      postal_code AS Поштовий_індекс,
      phone AS Телефон,
      email AS Електронна_пошта,
      customer_type AS Тип_клієнта
    FROM customers
    WHERE 
      city = 'Київ';
  ```
  Результат:




## Висновки

**Самооцінка**: [ваша оцінка роботи, 3-5]

**Обгрунтування**: [обґрунтування самооцінки]
