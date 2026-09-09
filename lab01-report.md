<img width="604" height="269" alt="image" src="https://github.com/user-attachments/assets/4ca66c2c-dc91-43e6-a139-b09306519048" /># Лабораторна робота 1. Робота з СУБД PostgreSQL та основи SQL

## Загальна інформація

**Здобувач освіти:** 
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

  ### 3. Базове сортування ORDER BY:
  ```sql
    -- Відсортувати товари за зростанням ціни. --
    SELECT 
      product_name AS Назва_товару,
      quantity_per_unit AS Кiлькiсть_в_упаковцi,
      unit_price AS Цiна,
      units_in_stock AS У_наявностi,
      description AS Опис,
      picture_url AS Посилання_на_зображення
    FROM products
    ORDER BY unit_price;
  ```
  Результат: Отримано 25 записів, відсортовані за цiною з полями product_name, quantity_per_unit, unit_price, units_in_stock, description, picture_url.
  <img width="771" height="459" alt="image" src="https://github.com/user-attachments/assets/983ee3d4-89e2-4d08-ae29-2ce652f70d79" />

  ```sql
    -- Показати клієнтів в алфавітному порядку за іменем контактної особи. --
  SELECT
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
  FROM customers
  ORDER BY contact_name;
  ```
  Результат: Отримано 15 клієнтів, відсортованих в алфавітному порядку за іменем контакту.

  ```sql
    -- Вивести замовлення від найновіших до найстаріших. --
  SELECT
    order_date AS Дата_замовлення,
    required_date AS Потрібна_дата,
    shipped_date AS Дата_відправки,
    ship_via AS Спосіб_доставки,
    freight AS Вартість_доставки,
    ship_name AS Назва_отримувача,
    ship_address AS Адресса_доставки,
    ship_city AS Мiсто_доставки,
    ship_region_id AS ID_регiону_доставки,
    ship_postal_code AS Поштовий_індекс_доставки,
    order_status AS Статус_замовлення
  FROM orders
  ORDER BY order_date DESC;
  ```
  Результат: Результат: Отримано 33 замовлення, відсортовані від найновіших до найстаріших (за датою спадаючий порядок).
  <img width="887" height="565" alt="image" src="https://github.com/user-attachments/assets/73b967a2-d3bb-43a2-80de-6e03da7e1d6b" />

  ### 4.Обмеження результатів LIMIT:
  ```sql
    -- Показати перші 10 найдорожчих товарів. --
  SELECT
    product_name AS Назва_товару,
    quantity_per_unit AS Кiлькiсть_в_упаковцi,
    unit_price AS Цiна,
    units_in_stock AS У_наявностi,
    units_on_order AS В_доставцi,
    reorder_level AS Рiвень_перезамовлення,
    discontinued AS Знято_з_виробництва,
    description AS Опис,
    picture_url AS Посилання_на_зображення
  FROM products
  ORDER BY unit_price DESC LIMIT 10;
  ```
  Результат: Отримано 10 найдорожчих товарів з максимальною ціною 95000 грн.
  <img width="949" height="201" alt="image" src="https://github.com/user-attachments/assets/2c0b2481-8ffd-4c85-a570-a71910b6ab86" />

  ```sql
    -- Вивести 5 останніх замовлень (за датою). --
  SELECT
    order_date AS Дата_замовлення,
    required_date AS Потрібна_дата,
    shipped_date AS Дата_відправки,
    ship_via AS Спосіб_доставки,
    freight AS Вартість_доставки,
    ship_name AS Назва_отримувача,
    ship_address AS Адресса_доставки,
    ship_city AS Мiсто_доставки,
    ship_region_id AS ID_регiону_доставки,
    ship_postal_code AS Поштовий_індекс_доставки,
    order_status AS Статус_замовлення
  FROM orders
  ORDER BY order_date DESC LIMIT 5;
  ```
  Результат: Отримано 5 останніх замовлень за датою з інформацією про доставку.
  <img width="809" height="114" alt="image" src="https://github.com/user-attachments/assets/083584ec-0945-4958-b449-66fc4216ae15" />

  ```sql
    -- Отримати перших 8 клієнтів в алфавітному порядку. --
  SELECT
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
  FROM customers
  ORDER BY contact_name LIMIT 8;
  ```
  Результат: Отримано 8 перших клієнтів в алфавітному порядку.
  <img width="910" height="162" alt="image" src="https://github.com/user-attachments/assets/26c2b2b1-4cad-4720-9ecf-a9ce537391ea" />

  ## Рівень 2
  ### 1. Пошук за зразком з LIKE:
  ```sql
    -- Знайти всіх клієнтів, чиї імена починаються на "Іван". --
  SELECT
    contact_name AS Iмя_контактної_особи,    -- основний фільтр
    company_name AS Назва_компанiї,          -- хто це
    phone AS Телефон,                        -- контакт
    email AS Електронна_пошта,               -- контакт
    city AS Мiсто                            -- геолокація
  FROM customers
  WHERE contact_name LIKE 'Іван%';  -- імена що починаються з "Іван"
  ```
  Результат:.
  <img width="345" height="41" alt="image" src="https://github.com/user-attachments/assets/4c6db35b-488c-4312-bf91-ef54ecca4f36" />

  ```sql
    -- Вивести товари, в назві яких є слово "phone" або "телефон". --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- основна інформація
    unit_price AS Цiна,                   -- важливо для продажів
    units_in_stock AS У_наявностi,        -- наявність на складі
    category_id AS ID_категорiї            -- категоризація
  FROM products
  WHERE product_name ILIKE '%phone%' 
     OR product_name ILIKE '%телефон%';
  ```
  Результат:.
  <img width="594" height="75" alt="image" src="https://github.com/user-attachments/assets/cb551d10-8e00-48c4-83ce-2162f11a5115" />

  ```sql
    -- Самостійно: Придумати та виконати 3 власні запити з використанням LIKE для пошуку за різними зразками (початок, кінець, містить). --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор товару
    product_name AS Назва_товару,         -- назва продукту
    unit_price AS Цiна,                   -- цінова політика
    units_in_stock AS У_наявностi,        -- наявність для замовлення
    category_id AS ID_категорiї            -- тип електроніки
  FROM products
  WHERE product_name LIKE 'Samsung%';
  ```
  Результат: .
  <img width="686" height="143" alt="image" src="https://github.com/user-attachments/assets/6fd786b5-36eb-4555-ab01-3bf8cc3127d7" />

  ```sql
    -- Самостійно: Придумати та виконати 3 власні запити з використанням LIKE для пошуку за різними зразками (початок, кінець, містить). --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- модель з обсягом
    unit_price AS Цiна,                   -- вартість
    units_in_stock AS У_наявностi,        -- наявність на складі
    category_id AS ID_категорiї            -- тип пристрою
  FROM products
  WHERE product_name ILIKE '%128GB%';  -- товари що містять "128GB"
  ```
  Результат:.
  <img width="706" height="179" alt="image" src="https://github.com/user-attachments/assets/978eb13c-ef58-41cb-ab5d-48be63d81f3c" />


  ```sql
    -- Самостійно: Придумати та виконати 3 власні запити з використанням LIKE для пошуку за різними зразками (початок, кінець, містить). --
  SELECT
    contact_name AS Iмя_контактної_особи,   -- основний контакт
    company_name AS Назва_компанiї,         -- компанія
    phone AS Телефон,                       -- зв'язок
    email AS Електронна_пошта,              -- комунікація
    city AS Мiсто                           -- геолокація
  FROM customers
  WHERE contact_title ILIKE '%директор';  -- пошук посад що закінчуються на "директор"
  ```
  Результат:.
  <img width="828" height="148" alt="image" src="https://github.com/user-attachments/assets/cfe2960c-78ba-4b14-bc69-717c305ba61c" />

  ```sql
    -- Знайти товари дорожчі за 15000 грн і дешевші за 50000 грн. --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва продукту
    unit_price AS Цiна,                   -- вартість для порівняння
    units_in_stock AS У_наявностi,        -- наявність на складі
    category_id AS ID_категорiї            -- категорія товару
  FROM products
  WHERE unit_price > 15000 
    AND unit_price < 50000;  -- середній ціновий сегмент для масового ринку
  ```
  Результат:.
  <img width="624" height="539" alt="image" src="https://github.com/user-attachments/assets/0c05182c-d1f0-45ca-bb1f-7fc2df24c7b6" />

  ```sql
    -- Вивести клієнтів з Києва або Львова, які є юридичними особами. --
  SELECT
    company_name AS Назва_компанiї,         -- назва клієнта
    contact_name AS Iмя_контактної_особи,   -- основний контакт
    phone AS Телефон,                       -- комунікація
    email AS Електронна_пошта,              -- комунікація
    city AS Мiсто                           -- геолокація
  FROM customers
  WHERE customer_type = 'company'  -- тільки юридичні особи
    AND (city = 'Київ' OR city = 'Львів');
  ```
  Результат:.
  <img width="736" height="132" alt="image" src="https://github.com/user-attachments/assets/e71dbd82-e4bf-4c59-a260-ed778ccda1df" />

  ```sql
    -- Самостійно: Створити 4 власні запити з комбінаціями логічних операторів для різних таблиць. --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва смартфона
    unit_price AS Цiна,                   -- вартість
    units_in_stock AS У_наявностi,        -- наявність
    supplier_id AS ID_постачальника       -- постачальник
  FROM products
  WHERE category_id = 1
    AND (supplier_id = 1 OR supplier_id = 3);
  ```
  Результат:.
  <img width="657" height="127" alt="image" src="https://github.com/user-attachments/assets/9d330930-6cf1-4640-b980-b49d8ffc2c62" />

  ```sql
    -- Самостійно: Створити 4 власні запити з комбінаціями логічних операторів для різних таблиць. --
  SELECT
    order_id AS ID_замовлення,           -- ідентифікатор
    order_date AS Дата_замовлення,       -- коли замовлено
    ship_city AS Мiсто_доставки,         -- геолокація
    freight AS Вартість_доставки,        -- вартість послуги
    ship_via AS Спосіб_доставки          -- кур'єр
  FROM orders
  WHERE ship_via = 'Нова Пошта'
    AND (ship_city = 'Київ' OR ship_city = 'Львів');
  ```
  Результат:.
  <img width="555" height="223" alt="image" src="https://github.com/user-attachments/assets/b7889821-567d-4fd3-979f-dafdc5f330ba" />

  ```sql
    -- Самостійно: Створити 4 власні запити з комбінаціями логічних операторів для різних таблиць. --
  SELECT
    employee_id AS ID_спiвробiтника,      -- ідентифікатор
    first_name AS Iмя,                    -- менеджер
    last_name AS Прiзвище,                -- менеджер
    city AS Мiсто,                        -- геолокація
    salary AS Зарплата                    -- оплата праці
  FROM employees
  WHERE title LIKE 'Менеджер%'  -- посада містить "Менеджер"
    AND (city = 'Київ' OR city = 'Львів');
  ```
  Результат:.
  <img width="486" height="163" alt="image" src="https://github.com/user-attachments/assets/e6c1b664-0ee3-463e-bd4d-84ca76eab90b" />

  ```sql
    -- Самостійно: Створити 4 власні запити з комбінаціями логічних операторів для різних таблиць. --
  SELECT
    company_name AS Назва_компанiї,       -- назва клієнта
    contact_name AS Iмя_контактної_особи, -- контакт
    phone AS Телефон,                     -- комунікація
    email AS Електронна_пошта,            -- комунікація
    city AS Мiсто                         -- геолокація
  FROM customers
  WHERE customer_type = 'company'  -- тільки юридичні особи
    AND (company_name LIKE 'ТОВ%' OR company_name LIKE 'ПП%');
  ```
  Результат:.
  <img width="796" height="204" alt="image" src="https://github.com/user-attachments/assets/ecaf6a7d-44e1-4143-8519-0deca05e9a81" />

  ```sql
    -- Вивести клієнтів з міст Київ, Харків, Одеса, Дніпро. --
  SELECT
    company_name AS Назва_компанiї,       -- назва клієнта
    contact_name AS Iмя_контактної_особи, -- контакт
    phone AS Телефон,                     -- комунікація
    email AS Електронна_пошта,            -- комунікація
    city AS Мiсто                         -- геолокація
  FROM customers
  WHERE city IN ('Київ', 'Харків', 'Одеса', 'Дніпро');
  ```
  Результат:.
  <img width="824" height="422" alt="image" src="https://github.com/user-attachments/assets/bd290267-3458-44ae-bfdb-d0c9b1d7d8cb" />

  ```sql
    -- Знайти товари в ціновому діапазоні від 10000 до 30000 грн. --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва товару
    unit_price AS Цiна,                   -- вартість
    units_in_stock AS У_наявностi,        -- наявність на складі
    category_id AS ID_категорiї            -- категорія
  FROM products
  WHERE unit_price BETWEEN 10000 AND 30000;  -- середній ціновий сегмент
  ```
  Результат:.
  <img width="633" height="448" alt="image" src="https://github.com/user-attachments/assets/e4e80db6-c0d5-4aca-9c1b-af4dc0948d22" />

  ```sql
    -- Придумати та виконати по 2 запити для кожного оператора (IN, BETWEEN, IS NULL/IS NOT NULL). --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва товару
    units_in_stock AS У_наявностi,        -- поточні запаси
    reorder_level AS Рiвень_перезамовлення,  -- рівень перезамовлення
    category_id AS ID_категорiї            -- категорія
  FROM products
  WHERE units_in_stock BETWEEN 10 AND 50;
  ```
  Результат:.
  <img width="711" height="508" alt="image" src="https://github.com/user-attachments/assets/860b0034-5cfb-4275-b8cc-c79967c46391" />

  ```sql
    -- Придумати та виконати по 2 запити для кожного оператора (IN, BETWEEN, IS NULL/IS NOT NULL). --
  SELECT
    order_id AS ID_замовлення,            -- ідентифікатор
    order_date AS Дата_замовлення,        -- дата замовлення
    freight AS Вартість_доставки,         -- вартість послуги
    ship_city AS Мiсто_доставки,          -- геолокація
    order_status AS Статус_замовлення     -- стан замовлення
  FROM orders
  WHERE freight BETWEEN 100 AND 500;
  ```
  Результат:.
  <img width="317" height="478" alt="image" src="https://github.com/user-attachments/assets/3e64e6f8-6a99-4f79-9f2d-be1a08310aa7" />

  ```sql
    -- Придумати та виконати по 2 запити для кожного оператора (IN, BETWEEN, IS NULL/IS NOT NULL). --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва товару
    unit_price AS Цiна,                   -- вартість
    category_id AS ID_категорiї,          -- категорія товару
    units_in_stock AS У_наявностi         -- наявність на складі
  FROM products
  WHERE category_id IN (1, 2, 3);
  ```
  Результат:.
  <img width="524" height="400" alt="image" src="https://github.com/user-attachments/assets/bc8237c2-670b-40e3-a3a1-c6626854ffd1" />

  ```sql
    -- Придумати та виконати по 2 запити для кожного оператора (IN, BETWEEN, IS NULL/IS NOT NULL). --
  SELECT
    order_id AS ID_замовлення,            -- ідентифікатор
    order_date AS Дата_замовлення,        -- дата замовлення
    order_status AS Статус_замовлення,    -- статус
    customer_id AS ID_клієнта,            -- покупець
    freight AS Вартість_доставки          -- витрати
  FROM orders
  WHERE order_status IN ('delivered','shipped');
  ```
  Результат:.
  <img width="311" height="496" alt="image" src="https://github.com/user-attachments/assets/912d03a6-5044-4266-863d-f78f020bfd00" />

  ```sql
    -- Придумати та виконати по 2 запити для кожного оператора (IN, BETWEEN, IS NULL/IS NOT NULL). --
  SELECT
    customer_id AS ID_клієнта,            -- ідентифікатор
    contact_name AS Iмя_контактної_особи, -- контакт
    phone AS Телефон,                     -- комунікація
    email AS Електронна_пошта,            -- комунікація
    city AS Мiсто                         -- геолокація
  FROM customers
  WHERE company_name IS NULL;
  ```
  Результат:.
  <img width="604" height="269" alt="image" src="https://github.com/user-attachments/assets/e3f67b44-f80b-43b7-8a3c-086afc06345c" />

  ```sql
    -- Придумати та виконати по 2 запити для кожного оператора (IN, BETWEEN, IS NULL/IS NOT NULL). --
  SELECT
    customer_id AS ID_клієнта,            -- ідентифікатор
    contact_name AS Iмя_контактної_особи, -- контакт
    contact_title AS Посада_контактної_особи,  -- посада (ключова інформація)
    phone AS Телефон,                     -- комунікація
    email AS Електронна_пошта             -- комунікація
  FROM customers
  WHERE contact_title IS NOT NULL;
  ```
  Результат:.
  <img width="655" height="191" alt="image" src="https://github.com/user-attachments/assets/88ca6212-5e9d-418e-b18a-8fe9658920a5" />

  ```sql
    -- Самостійно: Створити 5 складних запитів, які поєднують різні типи умов (LIKE + AND/OR, BETWEEN + IN, тощо). --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва моделі
    unit_price AS Цiна,                   -- вартість
    units_in_stock AS У_наявностi,        -- наявність
    category_id AS ID_категорiї            -- категорія
  FROM products
  WHERE product_name ILIKE '%phone%'
    AND unit_price BETWEEN 5000 AND 50000;
  ```
  Результат:.
  <img width="433" height="58" alt="image" src="https://github.com/user-attachments/assets/78c608ed-c5cb-4d12-9783-70e30e1655b1" />

  ```sql
    -- Самостійно: Створити 5 складних запитів, які поєднують різні типи умов (LIKE + AND/OR, BETWEEN + IN, тощо). --
  SELECT
    company_name AS Назва_компанiї,       -- назва організації
    contact_name AS Iмя_контактної_особи, -- контакт
    phone AS Телефон,                     -- комунікація
    email AS Електронна_пошта,            -- комунікація
    city AS Мiсто                         -- геолокація
  FROM customers
  WHERE company_name LIKE '%ТОВ%'  -- товариства з обмеженою відповідальністю
    OR company_name LIKE '%ПП%'    -- приватні підприємства
    OR company_name LIKE '%ПАТ%';  -- публічні акціонерні товариства
  ```
  Результат:.

  ```sql
    -- Самостійно: Створити 5 складних запитів, які поєднують різні типи умов (LIKE + AND/OR, BETWEEN + IN, тощо). --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва товару
    unit_price AS Цiна,                   -- вартість
    units_in_stock AS У_наявностi,        -- наявність
    category_id AS ID_категорiї            -- категорія
  FROM products
  WHERE unit_price BETWEEN 5000 AND 50000
    AND category_id IN (1, 2, 5);
  ```
  Результат:.
  <img width="530" height="269" alt="image" src="https://github.com/user-attachments/assets/b4277b07-9362-489f-bb71-b6c68e18727d" />

  ```sql
    -- Самостійно: Створити 5 складних запитів, які поєднують різні типи умов (LIKE + AND/OR, BETWEEN + IN, тощо). --
  SELECT
    employee_id AS ID_спiвробiтника,      -- ідентифікатор
    first_name AS Iмя,                    -- ім'я менеджера
    last_name AS Прiзвище,                -- прізвище менеджера
    city AS Мiсто,                        -- місцезнаходження офісу
    salary AS Зарплата                    -- оплата праці
  FROM employees
  WHERE title LIKE 'Менеджер%'  -- посада містить "Менеджер"
    AND city IN ('Київ', 'Львів');
  ```
  Результат:.
  <img width="402" height="135" alt="image" src="https://github.com/user-attachments/assets/0e37ec5c-4d2c-409f-b5a2-be99502878ce" />

  ```sql
    -- Самостійно: Створити 5 складних запитів, які поєднують різні типи умов (LIKE + AND/OR, BETWEEN + IN, тощо). --
  SELECT
    order_id AS ID_замовлення,            -- ідентифікатор
    order_date AS Дата_замовлення,        -- дата замовлення
    ship_city AS Мiсто_доставки,          -- геолокація
    order_status AS Статус_замовлення,    -- статус доставки
    customer_id AS ID_клієнта,            -- покупець
    freight AS Вартість_доставки          -- витрати на доставку
  FROM orders
  WHERE ship_city != 'Київ'
    AND order_status IN ('delivered', 'shipped');
  ```
  Результат:.
  <img width="488" height="520" alt="image" src="https://github.com/user-attachments/assets/fb7d0769-e525-4f0d-b14b-c71c20f49975" />

  ```sql
    -- Самостійно: Написати 3 запити з сортуванням за кількома полями та 2 запити з використанням OFFSET для пагінації. --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва товару
    category_id AS ID_категорiї,          -- категорія (первинна сортування)
    unit_price AS Цiна,                   -- ціна (вторинна сортування)
    units_in_stock AS У_наявностi         -- наявність
  FROM products
  ORDER BY category_id ASC, unit_price ASC;
  ```
  Результат:.
  <img width="359" height="460" alt="image" src="https://github.com/user-attachments/assets/26738f9e-6247-466d-8872-a333403aae00" />

  ```sql
    -- Самостійно: Написати 3 запити з сортуванням за кількома полями та 2 запити з використанням OFFSET для пагінації. --
  SELECT
    customer_id AS ID_клієнта,            -- ідентифікатор
    company_name AS Назва_компанiї,       -- назва клієнта
    contact_name AS Iмя_контактної_особи, -- контакт (вторинна сортування)
    city AS Мiсто,                        -- місто (первинна сортування)
    phone AS Телефон                      -- комунікація
  FROM customers
  ORDER BY city ASC, contact_name ASC;
  ```
  Результат:.
  <img width="380" height="285" alt="image" src="https://github.com/user-attachments/assets/fa0b08c0-b29d-4c8f-b5be-5a3e52f09c2b" />

  ```sql
    -- Самостійно: Написати 3 запити з сортуванням за кількома полями та 2 запити з використанням OFFSET для пагінації. --
  SELECT
    order_id AS ID_замовлення,            -- ідентифікатор
    order_date AS Дата_замовлення,        -- дата (вторинна сортування)
    order_status AS Статус_замовлення,    -- статус (первинна сортування)
    ship_city AS Мiсто_доставки,          -- геолокація
    freight AS Вартість_доставки          -- витрати
  FROM orders
  ORDER BY order_status ASC, order_date DESC;
  ```
  Результат:.
  <img width="319" height="565" alt="image" src="https://github.com/user-attachments/assets/0626c6db-79b0-43d4-8b2b-24eba5f63054" />

  ```sql
    -- Самостійно: Написати 3 запити з сортуванням за кількома полями та 2 запити з використанням OFFSET для пагінації. --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва товару
    unit_price AS Цiна,                   -- вартість
    units_in_stock AS У_наявностi,        -- наявність
    category_id AS ID_категорiї            -- категорія
  FROM products
  ORDER BY product_id ASC
  LIMIT 10 OFFSET 0;
  ```
  Результат:.
  <img width="352" height="196" alt="image" src="https://github.com/user-attachments/assets/108d555e-801d-4ee8-bb30-cece13ba40b7" />

  ```sql
    -- Самостійно: Написати 3 запити з сортуванням за кількома полями та 2 запити з використанням OFFSET для пагінації. --
  SELECT
    product_id AS ID_товару,              -- ідентифікатор
    product_name AS Назва_товару,         -- назва товару
    unit_price AS Цiна,                   -- вартість
    units_in_stock AS У_наявностi,        -- наявність
    category_id AS ID_категорiї            -- категорія
  FROM products
  ORDER BY product_id ASC
  LIMIT 10 OFFSET 10;
  ```
  Результат:.
  <img width="360" height="199" alt="image" src="https://github.com/user-attachments/assets/e14109dc-c156-4cd0-bf99-13ca04ab9364" />

  
## Висновки

**Самооцінка**: [3]

**Обгрунтування**: [Виконав 1й та 2й рiвень я б сказав без креативностi i бiзнес логiкi.]
