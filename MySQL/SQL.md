```
SELECT *
FROM  customer;

SELECT customer_id, last_name AS Фамилия, first_name AS Имя -- (alias-псевданимы) изменение названий в выводе.
from customer;

SELECT *
FROM  film;

SELECT f.title, c.name, f.rental_rate/f.rental_duration AS cost_per_day  -- (alias-псевданимы для таблиц)
From film f
JOIN film_category fc ON fc.film_id = f.film_id
JOIN category c ON c.category_id = fc.category_id;

SELECT title, rental_rate/rental_duration  as cost_per_day
from film
Order by cost_per_day asc, title desc;                              -- оператор сортировки ASC > < DESC < > по умолчанию ASC

SELECT  title, rental_rate/rental_duration  as cost_per_day
from film
order by cost_per_day desc, title asc
limit 100      -- вывести 100 записей с верху
offset 10;      -- начиная с 10 строки

SELECT DISTINCT store_id, last_name, first_name -- выводит уникальные значения
from customer;

SELECT amount, staff_id, CAST(payment_date as DATE)  -- меняет тип данных
FROM  payment p
WHERE p.amount > 7 AND staff_id = 2 OR  p.amount < 5 AND staff_id =1  -- задает условие AND (*) OR (+) NOT (отрицание)
ORDER BY amount ;

SELECT payment_id, payment_date, CAST(payment_date as DATE)  -- меняет тип данных 3-е задание сначала преобразовать а потом стравнивать.
FROM payment;

SELECT ROUND(100.576);        -- округляет до целого 101
SELECT ROUND(100.576, 2);      -- округляет до целого числа, до какого символа 100.58
SELECT TRUNCATE(100.576, 2);   -- отсекает дробную часть
SELECT FLOOR(100.576);         -- округление в пол
SELECT CEIL (100.576);         -- округление в потолок
SELECT  ABS(-100.576);         -- модуль числа (длинна вектора) 

SELECT title, ROUND(rental_rate/rental_duration, 2) as cost_per_day  -- округление выражений
from film
order by cost_per_day DESC , title;

SELECT POWER(2, 3);                    -- возведение в степень
SELECT SQRT(64);                       -- корень
SELECT 64 div 6;                       -- целочисленное деление
SELECT 64%6;                           -- остаток от деления
SELECT greatest(17, 5, 18, 21, 16);    -- большее числов массиве
SELECT LEAST(17, 5, 18, 21, 16);       -- меньшее число в массиве
SELECT RAND();                         -- генерация псевдослучайного значения

SELECT  rental_rate, rental_duration,
                rental_rate + rental_duration a,           -- сложение 
                rental_rate - rental_duration b,           -- вычитание
                rental_rate * rental_duration c,           -- умножение
                rental_rate / rental_duration d,           -- деление
                rental_rate % rental_duration e,           -- остаток от деления
                rental_rate DIV rental_duration f,         -- целочисленное деление
                POWER(rental_rate, rental_duration) g,     -- возведение в степень
                Cos(rental_rate) h, SIN(rental_duration) j -- косинус, синус
from film f;


-- work string


SELECT CONCAT(last_name, '    ', first_name, '    ', email)                    -- объединение значений из нескольких ячеек
from customer;

SELECT CONCAT_WS('  ---  ', last_name, first_name, email)                      -- можно задать разделитель
from customer c ;


SELECT  LENGTH(last_name), CHAR_LENGTH(last_name),                             -- LENGTH возвращает длинну строки в байтач
                LENGTH ('hallo'), CHAR_LENGTH('hallo')                         -- CHAR_LENGTH возвращает длинну строки в симвалах
FROM customer ;


SELECT last_name, POSITION('D' IN last_name), SUBSTR(last_name, 2 , 3),        -- POSITION возвращает позицию первого вхождения подстроки в строку
                LEFT(last_name, 3), RIGHT(last_name, 3)                        -- SUBSTR  извлекает подстроку из строки
from customer c ;                                                              -- LEFT\RIGHT извлекает ряд символов из строки начиная слева.справа

SELECT UPPER('ssss'), LOWER(last_name), INSERT (last_name, 1, 5, 'MAX'),       -- UPPER\LOWER преобразует строку в верхний\нижний регистр
                lower(replace(last_name, 'A', 'X'))                            -- INSERT вставляет подстроку в строку в указанной позиции и для определенного количества символов
from customer;

 SELECT *
 FROM customer c ;

SELECT  last_name , INSERT (last_name, 2, 1, 'MAX')                          -- INSERT вставляет подстроку в строку в указанной позиции и для определенного количества символов
FROM customer c ;

SELECT CONCAT(last_name, '  ', first_name)                                  -- CONCAT объединяет значения в одну ячейку
FROM customer c
WHERE first_name LIKE '%jam%';                                              -- LIKE (имя содержит сочетание jam) % любое количество символов, 1 _ означает 1 символ.

SELECT DATE_ADD(NOW(), INTERVAL 3 day);                          -- прибавить количество дней            

SELECT DATE_SUB(CURDATE(), INTERVAL  3 day);                      -- вычесть количество дней

SELECT YEAR(NOW()), MONTH(NOW()), WEEK(NOW()), DAY(NOW());         -- вывести год, месяц, неделя, день

SELECT EXTRACT(HOUR FROM NOW()), extract(DAY_MINUTE FROM NOW()),    -- часы, минуты прошедшие с начала дня
        extract(day from now());

SELECT DATEDIFF(return_date, rental_date), QUARTER(return_date)      -- возвращает временной промежуток
from rental r ;

SELECT DATE_FORMAT(payment_date, '%D-%M-%Y'), TIME_FORMAT(time(payment_date), '%T') -- изменить формат даты и времиени
from payment p

SELECT * FROM payment p WHERE amount BETWEEN 5 AND 7;




SQL -- Часть 2




-- JOIN and UNION


SELECT f.title , CONCAT(a.last_name, ' ', a.first_name) AS actor_name 
FROM film f 
JOIN film_actor fa ON fa.film_id = f.film_id 
JOIN actor a ON a.actor_id = fa.actor_id ;

SELECT CONCAT(c.last_name, ' ', c.first_name), c2.city
FROM customer c
LEFT JOIN address a ON a.address_id = c.address_id
LEFT JOIN city c2 ON c2.city_id = a.city_id ;

SELECT *
FROM customer c 

SELECT CONCAT(c.last_name, ' ', c.first_name), c2.city
FROM customer c 
JOIN address a ON a.address_id = c.address_id 
JOIN city c2 ON c2.city_id = a.city_id ;

SELECT f.title, r.rental_date 
FROM film f 
LEFT JOIN inventory i ON i.film_id = f.film_id 
LEFT JOIN rental r ON r.inventory_id = i.inventory_id 
WHERE r.rental_id is NOT  NULL ;

SELECT CONCAT(c.last_name, ' ', c.first_name), c2.city
FROM customer c 
RIGHT JOIN address a ON a.address_id = c.address_id 
RIGHT JOIN city c2 ON c2.city_id = a.city_id 
WHERE CONCAT(c.last_name, ' ', c.first_name) is NULL ;

SELECT r.rental_id, r.rental_date , p.payment_id, p.payment_date,  p.amount  
FROM rental r 
FULL JOIN payment p  ON  p.rental_id = r.rental_id ;                             -- в MySQL не применяется

SELECT c.name, fc.category_id, fc.category_id 
FROM category c 
Cross JOIN film_category fc ON fc.category_id = c.category_id ;

SELECT customer_id, first_name, address_id 
FROM customer c 
UNION all
select staff_id, first_name , address_id 
FROM staff s 

-- Агрегатые функции
SELECT COUNT(1)
From film f 
-- WHERE LOWER(LEFT(title,1)) = 'a'; -- посчитать все фильмы начинающиеся на 'a'
where title LIKE 'A%';               -- посчитать все фильмы начинающиеся на 'a'

SELECT c.first_name, COUNT(payment_id), SUM(amount), AVG(amount), min(amount), max(amount)  
from payment p 
JOIN customer c ON c.customer_id = p.customer_id
Group by c.first_name                  -- GROUP BY - группирующий оператор.
;


SELECT c.first_name, MONTH (payment_date), COUNT(payment_id), SUM(amount)  
FROM payment p 
jOIN customer c ON c.customer_id = p.customer_id
GROUP BY c.first_name  , MONTH (payment_date);

SELECT  f.title, f.release_year, f.length, COUNT(fa.actor_id) 
FROM film f 
Join film_actor fa ON fa.film_id = f.film_id
WHERE f.length > 48
GROUP BY f.film_id
-- Order by f.length asc
HAVING COUNT(fa.actor_id) > 4  -- аналог WHERE , но выполняется после группировки.
;


SELECT COUNT(1) from payment p   -- посчитать количество строк в таблице payment


-- ПОДЗАПРОСЫ

SELECT MONTH (payment_date) AS Месяц,
		COUNT(payment_id) / 
		(SELECT COUNT(1) from payment) * 100 AS "%"
FROM payment p 
GROUP BY MONTH (payment_date);





SELECT f.title ,c.name
FROM film f 
join film_category fc ON fc.film_id = f.film_id 
JOIN category c ON c.category_id = fc.category_id 
WHERE c.category_id IN 
					(SELECT category_id                 -- подзапрос возвращает массив значений
					From category 
					WHERE name LIKE 'Cl%')
ORDER BY f.title ;

SELECT CONCAT(s.last_name, ' ', s.first_name), cp / cr 
FROM staff s 
join 
	(select staff_id, COUNT(payment_id) AS cp
	From payment p 
	GROUP BY staff_id) t1 ON s.staff_id = t1.staff_id
JOIN 
	(select staff_id, COUNT(rental_id) AS cr
	From rental r
	GROUP BY staff_id) t2 ON s.staff_id = t2.staff_id;

SELECT staff_id, COUNT(payment_id) as cp
FROM payment p 
Group by staff_id 

SELECT staff_id , COUNT(rental_id) as cr 
FROM rental r 
Group by staff_id 



-- УСЛОВИЯ

SELECT  customer_id, SUM(amount), 
case
		when sum(amount) > 200 then 'Good user'
		when sum(amount) < 150 then 'Bad user'
		ELSE 'Average user' end AS good_or_bad
FROM payment p 
Group by customer_id
ORDER BY sum(amount) DESC 
LIMIT 100;

SELECT CONCAT(c.last_name, ' ', c.first_name) AS user, IFNULL(SUM(p.amount), 0)  -- подменяет значение NULL на любое другое
from customer c 
left join (select * FROM payment p
				WHERE  date(payment_date) = '2005-06-18') p 
				ON p.customer_id = c.customer_id 
GROUP BY c.customer_id ;

SELECT  rental_id,
		COALESCE (                                  -- убирает из вывода значение NULL (убрали аренды которые вернули в тотже день)
		DATEDIFF(RETURn_date, rental_date),
		DATEDIFF(NOW(), return_date),
		DATEDIFF(NOW(), rental_date)
		) AS diff
		from rental r 


SELECT CONCAT(first_name, ' ', last_name) AS ФИО  , store_id 
FROM staff s 

	
select COUNT(store_id) AS Клиентов
	From customer c  
GROUP BY store_id


-- ДЗ SQL часть 2

SELECT *
FROM customer c  

SELECT CONCAT(first_name, ' ', last_name) AS ФИО  , c.city, Клиентов 
FROM staff s 
join 
	(select store_id , COUNT(store_id) AS Клиентов
	 From customer c  
		GROUP BY store_id) AS  t1 ON s.store_id = t1.store_id
join
	address a on s.address_id = a.address_id 
JOIN 
	city c ON a.city_id = c.city_id
		
		
	
---------------------------
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

SELECT  COUNT(title) as oll, AVG(length), MIN(length), MAX(length), SUM(length) 
FROM film f 



SELECT MONTH (payment_date) AS Месяц,
		COUNT(payment_id) / 
		(SELECT COUNT(1) from payment) * 100 AS "%"
FROM payment p 
GROUP BY MONTH (payment_date); 


SELECT  customer_id, SUM(amount), 
case
		when sum(amount) > 200 then 'Good user'
		when sum(amount) < 150 then 'Bad user'
		ELSE 'Average user' end AS good_or_bad
FROM payment p 
Group by customer_id
ORDER BY sum(amount) DESC 
LIMIT 100;



SELECT c.first_name, COUNT(payment_id), SUM(amount), AVG(amount), min(amount), max(amount)  
from payment p 
JOIN customer c ON c.customer_id = p.customer_id
Group by c.first_name                  -- GROUP BY - группирующий оператор.
;



```































