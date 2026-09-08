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
  Результат: Отримано 8 записiв спiвробiтникiв з прiзвищем, iменем, номером телефону та електронною поштою.
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
  Результат: Отримано 4 записи за мiстом Київ, з назвою компанiї, iменем контактної особи, адрессою, мiсто, поштовым iндексом, номером телефону, електронною поштою та типом клієнта.
  <img width="1438" height="170" alt="image" src="https://github.com/user-attachments/assets/ca6f7fe8-3264-41a2-8488-615f4f9aa9fc" />

  ```sql
    -- Вивести товари, які коштують більше 25000 грн. --
    SELECT
      product_name AS Назва_товару,
      quantity_per_unit AS Кiлькiсть_в_упаковцi,
      unit_price AS Цiна,
      units_in_stock AS У_наявностi,
      units_on_order AS В_доставцi,
      discontinued AS Знято_з_виробництва,
      description AS Опис,
      picture_url AS Посилання_на_зображення
    FROM products
    WHERE unit_price > 25000;
  ```
  Результат: Отримано 13 записiв за цiною бiльше 25000, з назвою товару, кiлькiстью в упаковцi, цiною, у наявностi, в доставцi, чи знято з виробництва, описом та посилання на зображення. 
  <img width="1554" height="441" alt="image" src="https://github.com/user-attachments/assets/a39dc367-9c48-49bf-b5a7-8a4d2e38767d" />

  ```sql
    -- Показати всі замовлення зі статусом 'delivered'. --
  SELECT
    order_date AS Дата_замовлення,
    required_date AS Потрібна_дата,
    shipped_date AS Дата_відправки,
    ship_via AS Спосіб_доставки,
    freight AS Вартість_доставки,
    ship_name AS Назва_отримувача,
    ship_address AS Адресса_доставки,
    ship_city AS Мiсто_доставки,
    ship_postal_code AS Поштовий_індекс_доставки,
    order_status AS Статус_замовлення
  FROM orders
  WHERE order_status = 'delivered';
  ```
  Результат: Отримано 26 записiв за виконаним статусом доставкi, з датами замовлення, вiдправкi та приблизною датою прибуття; спосiбом, адрессою, мiстом, поштовим iндексом та вартicтю доставкi; назвою отримувача, статусом.
  <img width="807" height="479" alt="image" src="https://github.com/user-attachments/assets/073d5386-0ea8-459b-aad4-f43194a5dbae" />

  ```sql
    -- Знайти співробітників, які працюють у відділі продажів (посада містить слово "продаж"). --
  SELECT
    last_name AS Прiзвище,
    first_name AS Iмя,
    middle_name AS По_батькові,
    title AS Посада,
    birth_date AS Дата_народження,
    hire_date AS Дата_найму,
    address AS Адресса,
    city AS Мiсто,
    phone AS Телефон,
    email AS Електронна_пошта,
    salary AS Зарплата
  FROM employees
  WHERE title LIKE '%продаж%';
  ```
  Результат: Отримано 3 записи спiвробiтникiв за посадою що мiстить 'продаж', прiзвище, iмя, по батьтковi, посада, дата народження, дата найму, адресса, мiсто, телефон, електронна пошта, зарплата.
  <img width="1089" height="115" alt="image" src="https://github.com/user-attachments/assets/045ecc80-6534-4a98-ab13-fcbf47da351e" />





## Висновки

**Самооцінка**: [ваша оцінка роботи, 3-5]

**Обгрунтування**: [обґрунтування самооцінки]
