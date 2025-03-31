# Web Mission 3 - Решение
##Часть 1 - Авторизация
- **Эндпоинт:** 
[https://6ym9hq.buildship.run/me](https://6ym9hq.buildship.run/me) 
- **Логика:** 
[https://app.buildship.com/remix/acd558b8-cb54-41c0-9e08-b5175f4fd9d3](https://app.buildship.com/remix/acd558b8-cb54-41c0-9e08-b5175f4fd9d3)
##Часть 2 - Отправка сообщений
- **Эндпоинт:** 
[https://6ym9hq.buildship.run/message](https://6ym9hq.buildship.run/message) 
- **Логика:** 
[https://app.buildship.com/remix/030dcfd4-253e-431b-a14d-a1f6e9ecf7a4](https://app.buildship.com/remix/030dcfd4-253e-431b-a14d-a1f6e9ecf7a4)
##Часть 3 - SQL-запросы
### 1. Получить список юзернеймов пользователей
```sql SELECT username FROM users; ```
### 2. Получить количество отправленных сообщений 
### каждым пользователем
```sql SELECT 
users.username, COUNT(messages.id) AS 
number_of_sent_messages FROM users LEFT JOIN messages 
ON users.id = messages.from GROUP BY users.username; 
```
### 3. Получить пользователя с самым большим 
### количеством полученных сообщений и само 
### количество
```sql SELECT 
users.username, COUNT(messages.id) AS 
number_of_received_messages FROM users JOIN messages 
ON users.id = messages.to GROUP BY users.username 
ORDER BY number_of_received_messages DESC LIMIT 1; 
```
### 4. Получить среднее количество сообщений, 
### отправленных каждым пользователем
```sql SELECT 
AVG(sent_messages.number_of_sent_messages) AS 
average_sent_messages FROM (
    SELECT from, COUNT(*) AS number_of_sent_messages 
    FROM messages GROUP BY from
) AS sent_messages; ```
