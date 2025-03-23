# Mission 3

## Part 1
  
[Buildship endpoint URL 1](https://43geom.buildship.run/me)

**Screenshot**

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6a7a9983-1fb0-4caf-890f-892ea19ecc9c" />

---
  
## Part2

[Buildship endpoint URL 2](https://43geom.buildship.run/message)

**Screenshot**

<img width="507" alt="image" src="https://github.com/user-attachments/assets/7aa46abb-b088-4f9f-80b4-db05fba91c8a" />


---

## Part3

- **Список юзернеймов пользователей**
  ```
  SELECT username
  FROM users
  ```


- **Количество отправленных каждым пользователем сообщений**
  ```
  SELECT users.username, COUNT(messages.id) AS sent_messages_count
  FROM users
  JOIN messages ON users.id = messages.from
  GROUP BY users.username
  ```

  
- **Пользователь с самым большим количеством полученных сообщений и само количество**
  ```
  SELECT users.username, COUNT(messages.id) AS received_messages_count
  FROM users
  JOIN messages ON users.id = messages.to
  GROUP BY users.username
  HAVING COUNT(messages.id) = (
    SELECT MAX(received_messages_count)
    FROM (
      SELECT COUNT(messages.id) AS received_messages_count
      FROM users
      JOIN messages ON users.id = messages.to
      GROUP BY users.id
    ) AS counts
  )
  ```


- **Среднее количество сообщений, отправленных каждым пользователем**
  ```
  SELECT AVG(sent_messages_count) AS average_sent_messages
  FROM (
    SELECT COUNT(messages.id) AS sent_messages_count
    FROM users
    JOIN messages ON users.id = messages.from
    GROUP BY users.id
  ) AS message_counts
  ```
