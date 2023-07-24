#### Домашнее задание к занятию «SQL. Часть 1» -"Сергей Шульга"

#### Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```
SELECT DISTINCT district 
FROM address 
WHERE district  LIKE 'k%a' and district not LIKE  '% %';

```
![alt text]

#### Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

```
SELECT *
FROM payment
WHERE payment_date BETWEEN  CAST('2005-06-15' AS DATE) AND CAST('2005-06-19' AS DATE)
AND amount > 10;
```
![alt]

#### Задание 3
Получите последние пять аренд фильмов.

```
SELECT *  
FROM rental   
ORDER by rental_date DESC 
LIMIT 5
```
![alt]
#### Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
замените буквы 'll' в именах на 'pp'.
```
SELECT LOWER(REPLACE(first_name, 'L', 'p')), LOWER(last_name) 
FROM customer
WHERE first_name LIKE 'Willie' OR first_name  LIKE 'Kelly'
```
![alt]

Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

#### Задание 5*
Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.
```
SELECT email, SUBSTRING_INDEX(email , '@', 1), SUBSTRING_INDEX(email , '@', -1)
FROM customer;
```
![alt]

#### Задание 6*
Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

```
SELECT email  , SUBSTRING_INDEX(email  , '@', 1), 
CONCAT ( LEFT(UPPER(SUBSTRING_INDEX(email  , '@', 1)), 1), LOWER(SUBSTR((SUBSTRING_INDEX(email , '@',1)),2))) as '1' ,  
SUBSTRING_INDEX(email  , '@', -1) ,
CONCAT(LEFT(UPPER(SUBSTRING_INDEX(email  , '@', -1)), 1), LOWER(SUBSTR((SUBSTRING_INDEX(email , '@',-1)),2))) as '2'
FROM customer c ;
```
![alt]
