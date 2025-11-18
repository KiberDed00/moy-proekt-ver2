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
#Блок-схема процесса заказа
``` mermaid
graph TD
    A[Начало] --> B[Выбор ресторана и блюд]
    B --> C{Достаточно ли средств?}
    C -->|Нет| D[Пополнить баланс]
    C -->|Да| E[Оформление заказа]
    D --> E
    E --> F[Ресторан подтверждает заказ]
    F --> G{Ресторан принял заказ?}
    G -->|Нет| H[Отмена заказа]
    G -->|Да| I[Приготовление еды]
    H --> Z[Конец]
    I --> J[Поиск курьера]
    J --> K[Курьер забирает заказ]
    K --> L[Доставка клиенту]
    L --> M[Получение оплаты]
    M --> N[Оценка сервиса]
    N --> Z[Конец]
```
---
#Диаграмма последовательности
```mermaid
sequenceDiagram
    title Процесс доставки еды
    
    participant К as Клиент
    participant П as Приложение
    participant С as Сервер
    participant Р as Ресторан
    participant Кур as Курьер

    activate К
    К->>П: Выбор блюд
    П->>С: Запрос меню
    С-->>П: Данные меню
    П-->>К: Отображение меню
    
    К->>П: Оформление заказа
    П->>С: Создание заказа
    activate С
    С->>Р: Уведомление о новом заказе
    activate Р
    
    Р->>С: Подтверждение заказа
    С->>П: Статус "Принят рестораном"
    П-->>К: Уведомление о подтверждении
    
    Р->>С: Заказ готов
    С->>С: Поиск свободного курьера
    С->>Кур: Назначение заказа
    activate Кур
    
    Кур->>С: Принятие заказа
    С->>П: Данные курьера
    П-->>К: Уведомление о курьере
    
    Кур->>Р: Забор заказа
    Кур->>С: Статус "В пути"
    С->>П: Обновление статуса
    П-->>К: Уведомление "Курьер в пути"
    
    Кур->>К: Доставка заказа
    К->>П: Подтверждение получения
    П->>С: Заказ завершен
    С->>Р: Перевод оплаты
    С->>Кур: Начисление оплаты
    
    deactivate К
    deactivate С
    deactivate Р
    deactivate Кур
```
---
#Диаграмма классов системы
```mermaid
classDiagram
    class User {
        +String userId
        +String name
        +String email
        +String phone
        +String address
        +register()
        +login()
        +updateProfile()
    }
    
    class Customer {
        +List~Order~ orderHistory
        +List~Address~ addresses
        +addToCart()
        +placeOrder()
        +rateOrder()
    }
    
    class Restaurant {
        +String restaurantId
        +String name
        +String cuisine
        +String address
        +Time openingHours
        +List~Menu~ menu
        +updateMenu()
        +confirmOrder()
    }
    
    class Courier {
        +String courierId
        +String vehicleType
        +bool isAvailable
        +Location currentLocation
        +acceptOrder()
        +updateLocation()
        +completeDelivery()
    }
    
    class Order {
        +String orderId
        +Date orderDate
        +String status
        +double totalAmount
        +List~OrderItem~ items
        +updateStatus()
        +calculateTotal()
    }
    
    class Menu {
        +String menuId
        +List~MenuItem~ items
        +addItem()
        +removeItem()
    }
    
    class Payment {
        +String paymentId
        +String method
        +double amount
        +String status
        +processPayment()
        +refund()
    }
    
    User <|-- Customer
    User <|-- Courier
    Customer "1" -- "*" Order
    Restaurant "1" -- "*" Order
    Courier "1" -- "*" Order
    Order "1" -- "*" Payment
    Restaurant "1" -- "1" Menu
```
---
# ER-диаграмма базы данных
```mermaid
erDiagram
    USERS {
        string user_id PK
        string name
        string email
        string phone
        string user_type
        datetime created_at
    }
    
    CUSTOMERS {
        string customer_id PK
        string user_id FK
        json delivery_addresses
        decimal loyalty_points
    }
    
    RESTAURANTS {
        string restaurant_id PK
        string name
        string cuisine_type
        string address
        string phone
        json opening_hours
        decimal rating
    }
    
    COURIERS {
        string courier_id PK
        string user_id FK
        string vehicle_type
        boolean is_available
        json current_location
        decimal rating
    }
    
    MENU_ITEMS {
        string item_id PK
        string restaurant_id FK
        string name
        string description
        decimal price
        boolean is_available
    }
    
    ORDERS {
        string order_id PK
        string customer_id FK
        string restaurant_id FK
        string courier_id FK
        string status
        decimal total_amount
        datetime order_time
        datetime delivery_time
    }
    
    ORDER_ITEMS {
        string order_item_id PK
        string order_id FK
        string menu_item_id FK
        int quantity
        decimal price
    }
    
    PAYMENTS {
        string payment_id PK
        string order_id FK
        string payment_method
        decimal amount
        string status
        datetime payment_date
    }
    
    USERS ||--o{ CUSTOMERS : "is"
    USERS ||--o{ COURIERS : "is"
    CUSTOMERS ||--o{ ORDERS : "places"
    RESTAURANTS ||--o{ ORDERS : "receives"
    RESTAURANTS ||--o{ MENU_ITEMS : "has"
    COURIERS ||--o{ ORDERS : "delivers"
    ORDERS ||--o{ ORDER_ITEMS : "contains"
    ORDERS ||--|| PAYMENTS : "has"
```
---
#User Journey клиента
```mermaid
journey
    title Путешествие клиента сервиса доставки еды
    
    section Поиск и выбор
      Открытие приложения: 5: Клиент
      Просмотр ресторанов: 4: Клиент
      Выбор блюд: 5: Клиент
      Добавление в корзину: 4: Клиент
    
    section Оформление заказа
      Ввод данных доставки: 3: Клиент
      Выбор способа оплаты: 4: Клиент
      Подтверждение заказа: 5: Клиент
    
    section Ожидание и отслеживание
      Ожидание подтверждения: 2: Клиент
      Отслеживание статуса: 4: Клиент
      Получение уведомлений: 5: Клиент
    
    section Получение и оценка
      Встреча с курьером: 5: Клиент
      Проверка заказа: 4: Клиент
      Оценка сервиса: 3: Клиент
```
---
#Диаграмма Ганта разработки проекта
```mermaid
gantt
    title План разработки сервиса доставки еды
    dateFormat YYYY-MM-DD
    axisFormat %d/%m
    
    section Анализ и проектирование
      Сбор требований     :2025-01-01, 14d
      Проектирование БД   :2025-01-15, 14d
      Прототипирование UI :2025-01-29, 14d
    
    section Бэкенд разработка
      Базовая архитектура :2025-02-12, 21d
      Модуль пользователей:2025-03-05, 21d
      Модуль заказов      :2025-03-26, 21d
      Модуль платежей     :2025-04-16, 21d
      API интеграции      :2025-05-07, 21d
    
    section Фронтенд разработка
      Клиентское приложение:2025-02-26, 45d
      Панель ресторана     :2025-04-11, 30d
      Приложение курьера   :2025-05-11, 30d
    
    section Тестирование
      Модульное тестирование :2025-05-28, 21d
      Интеграционное тестир. :2025-06-18, 21d
      User Acceptance Testing:2025-07-09, 14d
    
    section Запуск
      Подготовка к запуску :2025-07-23, 14d
      Релиз v1.0          :2025-08-06, 1d
      Поддержка и обновления:2025-08-07, 60d
```
---
