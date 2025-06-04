# HW-12.2
# 12.2 Работа с данными (DDL/DML)
Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

#### *Ответ:*

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
```bash
wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.28-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.28-1_all.deb
sudo apt update
sudo apt install mysql-server
sudo systemctl status mysql
sudo systemctl enable mysql
mysql -u root -p
```
![1 1](https://github.com/user-attachments/assets/f2bd6e3f-fa4d-421a-910f-5a4144727f22)
![1 1 2](https://github.com/user-attachments/assets/35f496c8-52a7-4cf6-9274-92a1e16b5b93)


1.2. Создайте учётную запись sys_temp. 
```bash
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY '1234567';
```
![1 2](https://github.com/user-attachments/assets/6ffae2f2-5616-422b-9052-d77680a75167)


1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
```bash
SELECT user FROM mysql.user;
```
![1 3](https://github.com/user-attachments/assets/ca706895-d8cb-4511-bc3c-fba2e5cb31ae)


1.4. Дайте все права для пользователя sys_temp. 
```bash
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
```
![1 4](https://github.com/user-attachments/assets/228f82b9-e60b-4bc7-9491-2ddd2f89cd50)


1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
```bash
SELECT * FROM information_schema.user_privileges WHERE GRANTEE="'sys_temp'@'localhost'";
```
![1 5](https://github.com/user-attachments/assets/f4e1bbff-37af-417d-9d83-ca5e90e42d0f)
![1 5 2](https://github.com/user-attachments/assets/94365355-b15a-4893-920c-c50a186ecaec)


1.6. Переподключитесь к базе данных от имени sys_temp.
```bash
SYSTEM mysql -u sys_temp -p
SELECT user();
```
![1 6](https://github.com/user-attachments/assets/142c40b1-11f1-4e8d-86ac-d6a407ff01df)


Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.
```bash
wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
```
![1 7](https://github.com/user-attachments/assets/57e2eb39-a399-4ef0-bd4e-a991ddba341e)
![1 7-2](https://github.com/user-attachments/assets/32b01c82-183b-403b-961b-b4b1e5c17384)

1.8. Восстановите дамп в базу данных.
```bash
source /home/tverdyakov/sakila-db/sakila-schema.sql
source /home/tverdyakov/sakila-db/sakila-data.sql
SHOW DATABASES;
```
![1 8-1](https://github.com/user-attachments/assets/9868b64d-e348-4bad-91e9-047fdb8fe54e)
![1 8-2](https://github.com/user-attachments/assets/df7da8a2-4e25-4170-a0d1-9be73c296716)
![1 8-3](https://github.com/user-attachments/assets/bc796efa-2266-43b2-a5e2-0f270a36fb77)

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
```bash
SHOW TABLES;
```
![1 9-1](https://github.com/user-attachments/assets/d4d3388f-1c74-4c0c-a481-b95798b9780b)
![Задание 1 9-2](https://github.com/user-attachments/assets/fab9c912-2fa2-4338-9c39-f4ea8896100b)


*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

#### *Ответ:*
```bash
+---------------+--------------+
| TABLE_NAME    | COLUMN_NAME  |
+---------------+--------------+
| actor         | actor_id     |
| address       | address_id   |
| category      | category_id  |
| city          | city_id      |
| country       | country_id   |
| customer      | customer_id  |
| film          | film_id      |
| film_actor    | actor_id     |
| film_actor    | film_id      |
| film_category | film_id      |
| film_category | category_id  |
| film_text     | film_id      |
| inventory     | inventory_id |
| language      | language_id  |
| payment       | payment_id   |
| rental        | rental_id    |
| staff         | staff_id     |
| store         | store_id     |
+---------------+--------------+
```
![2-2](https://github.com/user-attachments/assets/8389d257-1b21-41e8-a690-a2f4ace4fee4)


---

