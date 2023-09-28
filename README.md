# DMnDBMS
### Функциональные требования
1. **Управление пользовательскими аккаунтами:**
   - Пользователи могут регистрироваться, указывая свои данные.
   - Пользователи могут войти в систему, используя электронную почту и пароль.
   - Пользователи могут резервировать книги и просматривать историю своих заказов.
   - Каждый пользователь сатус членства: либо является членом библиотеки, либо нет.
   - Администраторы могут управлять пользователями и менять статус их членства.
  
2. **Управление книгами:**
   - Администраторы могут добавлять, редактировать и удалять книги.
   - Книги можно просматривать по жанрам и авторам.

3. **Уведомления и обратная связь:**
   - Пользователи получают уведомления о статусе своих резервирований.
   - Пользователи могут оставлять рецензии на книги.
   
4. **Журнал действий:**
   - Система фиксирует все действия пользователей (например, резервирование книги, оставление рецензии).

### Сущности базы данных
1. **Пользователи (Users):**
   - UserID (Primary Key, INT, AUTOINCREMENT)
   - Имя (VARCHAR(255))
   - Фамилия (VARCHAR(255))
   - Email (VARCHAR(255), Уникальный)
   - Пароль (VARCHAR(255))
   - КатегорияID (Foreign Key, связь с UserCategories.CategoryID)

2. **Категории пользователей (UserCategories):**
   - CategoryID (Primary Key, INT, AUTOINCREMENT)
   - Название категории (VARCHAR(255))

3. **Книги (Books):**
   - BookID (Primary Key, INT, AUTOINCREMENT)
   - Название (VARCHAR(255))
   - АвторID (Foreign Key, связь с Authors.AuthorID)
   - ЖанрID (Foreign Key, связь с Genres.GenreID)
   - ИздательID (Foreign Key, связь с Publishers.PublisherID)

4. **Авторы (Authors):**
   - AuthorID (Primary Key, INT, AUTOINCREMENT)
   - Имя (VARCHAR(255))
   - Фамилия (VARCHAR(255))

5. **Жанры (Genres):**
   - GenreID (Primary Key, INT, AUTOINCREMENT)
   - Название жанра (VARCHAR(255))

6. **Издатели (Publishers):**
   - PublisherID (Primary Key, INT, AUTOINCREMENT)
   - Название издательства (VARCHAR(255))

7. **Выдачи (Checkouts):**
   - CheckoutID (Primary Key, INT, AUTOINCREMENT)
   - UserID (Foreign Key, связь с Users.UserID)
   - BookID (Foreign Key, связь с Books.BookID)
   - Дата выдачи (DATE)
   - Дата возврата (DATE)

8. **Рецензии (Reviews):**
   - ReviewID (Primary Key, INT, AUTOINCREMENT)
   - UserID (Foreign Key, связь с Users.UserID)
   - BookID (Foreign Key, связь с Books.BookID)
   - Текст рецензии (TEXT)
   - Дата создания (DATE)

9. **Уведомления (Notifications):**
   - NotificationID (Primary Key, INT, AUTOINCREMENT)
   - UserID (Foreign Key, связь с Users.UserID)
   - Содержание (TEXT)
   - Дата отправки (DATE)

10. **Журнал действий (UserActions):**
    - ActionID (Primary Key, INT, AUTOINCREMENT)
    - UserID (Foreign Key, связь с Users.UserID)
    - Описание действия (TEXT)
    - Дата и время (DATETIME)

11. **Резервации (Reservations):**
    - ReservationID (Primary Key, INT, AUTOINCREMENT)
    - UserID (Foreign Key, связь с Users.UserID)
    - BookID (Foreign Key, связь с Books.BookID)
    - Дата резервации (DATE)
    - Статус резервации (ENUM: 'Pending', 'Approved', 'Declined')

12. **История уведомлений (NotificationHistory):**
    - HistoryID (Primary Key, INT, AUTOINCREMENT)
    - NotificationID (Foreign Key, связь с Notifications.NotificationID)
    - Статус (ENUM: 'Sent', 'Read')
    - Дата чтения (DATE)

13. **Избранное (Favorites):**
    - FavoriteID (Primary Key, INT, AUTOINCREMENT)
    - UserID (Foreign Key, связь с Users.UserID)
    - BookID (Foreign Key, связь с Books.BookID)

### Виды связей:
- **Users** и **UserCategories**: Один ко многим. Один тип пользователя может соответствовать множеству пользователей.
- **Books**, **Authors**, **Genres** и **Publishers**: Множество-ко-множеству. Одна книга может иметь много авторов, и один автор может написать много книг. То же самое относится к жанрам.
- **Checkouts**, **Users** и **Books**: Один ко многим. Один пользователь может брать много книг, и одна книга может быть выдана множеству пользователей.
- **Reviews**, **Users** и **Books**: Один ко многим. Один пользователь может оставлять множество рецензий, и одна книга может иметь много рецензий.
- **Notifications** и **Users**: Один ко многим. Один пользователь может получать множество уведомлений.
- **UserActions** и **Users**: Один ко многим. Один пользователь может совершать много действий.
