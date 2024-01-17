# Домашнее задание к занятию «SQL. Часть 1»

## Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

### Ответ.

```SQL

SELECT DISTINCT district
FROM address a
WHERE district LIK 'K%a' AND district NOT LIKE '% %';

```

![скрин](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-16_11-00-09.png)

## Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

### Ответ.

```SQL

SELECT amount, CAST(payment_date AS DATE)
FROM payment p
WHERE amount > 10 AND DATE(payment_date) >= '2005-06-15' AND DATE(payment_date) <= '2005-06-18';

```

![скрин](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-16_12-26-42.png)

## Задание 3
Получите последние пять аренд фильмов.

### Ответ.

```SQL

SELECT *
FROM rental r
ORDER BY rental_id DESC
LIMIT 5;

```

![скрин](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-16_13-58-27.png)

## Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
замените буквы 'll' в именах на 'pp'.

### Ответ.

```SQL

SELECT LOWER(INSERT(first_name, 3, 2, 'pp')) AS first_name, LOWER(last_name) AS last_name, active
FROM customer c
WHERE first_name LIKE 'Kelly' OR first_name LIKE 'Willie' AND active = 1;

```

![скрин](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-17_09-42-50.png).


