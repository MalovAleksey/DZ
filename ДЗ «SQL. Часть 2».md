# Домашнее задание к занятию «SQL. Часть 2»

## Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.

## Ответ
```SQL

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
WHERE Клиентов > 300;

```

![скрин](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-28_13-46-49.png)

## Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.


## Ответ

```SQL

SELECT COUNT(1)
FROM film f
where length > (SELECT AVG(length) FROM film f);

```

![скрин](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-27_17-33-47.png)

## Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

## Ответ

```SQL

SELECT MONTH(payment_date) as месяц , sum(amount) as сумма, SUM(rental_id) as аренд 
FROM payment p 
GROUP BY MONTH (payment_date)
ORDER BY сумма DESC

```

![скрин](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-27_18-23-31.png)
