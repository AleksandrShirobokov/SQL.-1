# «SQL. Часть 1»
# Александр Широбоков
## Задание 1
**Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.**
![Снимок экрана (220)](https://github.com/AleksandrShirobokov/SQL.-1/assets/69298696/7a4d8a03-c13e-4a82-9150-294e972a7442)
```
SELECT DISTINCT district 
FROM address a
WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
```
## Задание 2
**Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.**
![Снимок экрана (226)](https://github.com/AleksandrShirobokov/SQL.-1/assets/69298696/8761930c-4785-4e44-a9ec-c8c7b9768ade)
```
SELECT *
FROM payment
WHERE payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59'
  AND amount > 10.00;
```
## Задание 3
**Получите последние пять аренд фильмов.**
![Снимок экрана (222)](https://github.com/AleksandrShirobokov/SQL.-1/assets/69298696/49acbb8a-a353-4554-8402-dfb0ac9fbb0d)
```
SELECT *
FROM rental
ORDER BY rental_date DESC
LIMIT 5;
```
## Задание 4
**Одним запросом получите активных покупателей, имена которых Kelly или Willie.**
 - **Сформируйте вывод в результат таким образом:**
 - *все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр*
 - *замените буквы 'll' в именах на 'pp'.*
![Снимок экрана (223)](https://github.com/AleksandrShirobokov/SQL.-1/assets/69298696/004e52f3-513f-4540-8f1b-ea25ee2f25b0)
```
SELECT REPLACE(LOWER(first_name), 'll', 'pp') AS first_name, LOWER(last_name) AS last_name
FROM customer
WHERE (first_name = 'Kelly' OR first_name = 'Willie')
  AND active = 1;
```
## Задание 5
**Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.**
![Снимок экрана (224)](https://github.com/AleksandrShirobokov/SQL.-1/assets/69298696/353816bd-5599-4e33-937c-d996ea1b85be)
```
SELECT
  SUBSTRING_INDEX(email, '@', 1) AS email_before_at,
  SUBSTRING_INDEX(email, '@', -1) AS email_after_at
FROM customer;
```
## Задание 6
**Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.**
![Снимок экрана (225)](https://github.com/AleksandrShirobokov/SQL.-1/assets/69298696/35d58cb8-cb25-477b-9dab-0d20c1de82b1)
```
SELECT
  CONCAT(UCASE(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)), LOWER(REPLACE(SUBSTRING_INDEX(email, '@', 1), LEFT(SUBSTRING_INDEX(email, '@', 1), 1), ''))) AS email_before_at,
  CONCAT(UCASE(LEFT(SUBSTRING_INDEX(email, '@', -1), 1)), LOWER(REPLACE(SUBSTRING_INDEX(email, '@', -1), LEFT(SUBSTRING_INDEX(email, '@', -1), 1), ''))) AS email_after_at
FROM customer;
```
## Код всех заданий:
```
/*Задание 1*/
SELECT DISTINCT district 
FROM address a
WHERE district LIKE 'K%a' AND district NOT LIKE '% %';

/*Задание 2*/
SELECT *
FROM payment
WHERE payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59'
  AND amount > 10.00;

/*Задание 3*/ 
SELECT *
FROM rental
ORDER BY rental_date DESC
LIMIT 5;

/*Задание 4*/
SELECT REPLACE(LOWER(first_name), 'll', 'pp') AS first_name, LOWER(last_name) AS last_name
FROM customer
WHERE (first_name = 'Kelly' OR first_name = 'Willie')
  AND active = 1;

/*Задание 5*/ 
SELECT
  SUBSTRING_INDEX(email, '@', 1) AS email_before_at,
  SUBSTRING_INDEX(email, '@', -1) AS email_after_at
FROM customer;

/*Задание 6*/
SELECT
  CONCAT(UCASE(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)), LOWER(REPLACE(SUBSTRING_INDEX(email, '@', 1), LEFT(SUBSTRING_INDEX(email, '@', 1), 1), ''))) AS email_before_at,
  CONCAT(UCASE(LEFT(SUBSTRING_INDEX(email, '@', -1), 1)), LOWER(REPLACE(SUBSTRING_INDEX(email, '@', -1), LEFT(SUBSTRING_INDEX(email, '@', -1), 1), ''))) AS email_after_at
FROM customer;

```
