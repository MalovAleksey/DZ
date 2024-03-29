## ДЗ Работа с данными (DDL_DML).md

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

#### Ответ.
![Скриншот 1](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-12_13-18-53.png)

![Скриншот 2](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-12_15-04-24.png)

![Скриншот 3](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-12_15-29-01.png)

![Скриншот 4](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-12_15-32-24.png)

![Скриншот 5](https://github.com/MalovAleksey/DZ/blob/main/MySQL/2024-01-13_16-12-18.png)

### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

Название таблицы | Название первичного ключа
customer         | customer_id
Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

#### Ответ.

![image](https://github.com/MalovAleksey/DZ/assets/128486566/cb03555b-ce53-466c-abcd-a98aff57b3cb)


