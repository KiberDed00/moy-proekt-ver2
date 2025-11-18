#tea
``` mermaid
graph TD
    A[Начало] --> B[Кипячение воды]
    B --> C{Есть ли чай?}
    C -->|Да| D[Заварить чай]
    C -->|Нет| E[Купить чай]
    E --> D
    D --> F[Пить чай]
    F --> G[Конец]
```
---
#taxi
``` mermaid
sequenceDiagram
    title Процесс "Заказ такси"
    participant Клиент
    participant Приложение
    participant Сервер
    participant Водитель

    Клиент->>Приложение: Вызывает такси (запрос)
    activate Приложение
    Приложение->>Сервер: Отправляет запрос
    activate Сервер
    Сервер->>Сервер: Ищет свободного водителя
    Сервер-->>Водитель: Принимает заказ (уведомление)
    activate Водитель
    Водитель->>Сервер: Принимает заказ (подтверждение)
    Сервер-->>Приложение: Уведомление о водителе
    deactivate Сервер
    Note right of Приложение: Отобразить информацию о водителе
    Приложение->>Клиент: Уведомление (Водитель едет)
    deactivate Приложение
    Водитель->>Клиент: Забирает клиента
    deactivate Водитель
```
---
#Mid
```mermaid
classDiagram
    class Book {
        +String title
        +String author
        +String ISBN
        -Boolean isAvailable
    }

    class User {
        +String name
        +Integer userId
        -List~Book~ borrowedBooks[]
    }

    class Library {
        -List~Book~ books[]
        -List~User~ users[]
        +borrowBook(userId, isbn)
        +returnBook(userId, isbn)
    }

    User  *--  Book : Агрегация
    Library  o--  Book : Композиция
    Library  o--  User : Композиция
```
---
# Диаграмма Ганта
```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title Разработка мобильного приложения
    
    section Основные этапы
    Подготовка      :a1, 2025-11-20, 5d
    Дизайн          :a2, after a1, 7d
    Фронтенд-разработка :a3, after a2, 10d
    Бэкенд-разработка   :a4, after a1, 12d
    Тестирование    :after a3, after a4, 5d
```
---
# Продвинутый
```mermaid
graph LR
    subgraph Frontend
        F1[React] --> F2[Redux]
        F1 --> F3[Router]
    end

    subgraph Backend
        B1[Node.js] --> B2[Express]
        B1 --> B3[MongoDB]
    end

    subgraph External Services
        E1[Stripe]
        E2[(SendGrid)]
    end

    F1 -- API Calls --> B2
    B2 -- Data Read/Write --> B3
    B2 -- Initiate Payment --> E1
    B2 -- Send Notification --> E2
```
---
#   Диаграмма состояний
```mermaid
stateDiagram-v2
    direction LR
    
    [*] --> Новый
    
    Новый --> Подтвержденный : Инициализация заказа
    Подтвержденный --> Отмененный : Отмена клиентом
    
    Подтвержденный --> Оплата
    
    state Оплата {
        direction TB
        [*] --> Ожидает_платежа
        Ожидает_платежа --> Платеж_провален : Ошибка / Отказ
        Ожидает_платежа --> Платеж_успешен : Успешная транзакция
        Платеж_провален --> Подтвержденный : Повторить оплату
        Платеж_успешен --> [*]
    }
    
    Оплата --> Оплаченный : Платеж_успешен
    Платеж_провален --> Отмененный : Исчерпаны попытки оплаты
    
    Оплаченный --> Отправленный : Отгрузка со склада
    Отправленный --> Доставленный : Успешная доставка
    
    Доставленный --> Возвращенный : Инициировать возврат
```
---
# Экспертный
```mermaid
journey
    title Путь пользователя: Покупка билетов в кино

    section Поиск фильма
      Пользователь: 1: Поиск фильма
      Пользователь: 2: Просмотр трейлера

    section Выбор сеанса
      Пользователь: 3: Фильтр по дате и времени
      Пользователь: 4: Выбор кинотеатра
      
    section Выбор мест
      Пользователь: 5: Выбор места на схеме
      Пользователь: 4: Добавление в корзину

    section Оплата
      Пользователь: 2: Ввод данных карты
      Пользователь: 1: Ожидание подтверждения

    section Получение билетов
      Пользователь: 5: Получение QR-кода на почту
```
---
# ER-диаграмма базы данных
```mermaid
erDiagram
    USERS ||--o{ POSTS : "имеет"
    USERS ||--o{ COMMENTS : "автор"
    POSTS ||--o{ COMMENTS : "содержит"
    POSTS ||--o{ LIKES : "получает"
    USERS ||--o{ LIKES : "ставит"
    USERS ||--o{ SUBSCRIPTIONS : "подписан_на"
    SUBSCRIPTIONS }|--|{ USERS : "подписчик"

    USERS {
        int id PK
        varchar name
        varchar email
    }

    POSTS {
        int id PK
        varchar content
        int author_id FK
    }

    COMMENTS {
        int id PK
        varchar content
        int post_id FK
        int author_id FK
    }

    LIKES {
        int user_id FK
        int post_id FK
        PRIMARY KEY user_id post_id)
    }

    SUBSCRIPTIONS {
        int follower_id FK
        int followed_id FK
        PRIMARY KEY follower_id followed_id)
    }
```
---
