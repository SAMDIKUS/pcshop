# Интернет-магазин компьютеров и комплектующих (бэкенд)

Java 21, Spring Boot 3, Spring Security (JWT), Spring Data JPA, H2.

## Запуск

```
mvn spring-boot:run
```

Сервер стартует на http://localhost:8080. База H2 лежит в папке `data/` (jdbc:h2:file:./data/pcshop).
Чтобы сбросить данные, удали папку `data/`.

При первом запуске создаются тестовые данные.

Фронт (HTML/CSS/JS без сборки) лежит в `src/main/resources/static` и открывается на том же адресе: http://localhost:8080.
Подробная инструкция по проверке и заливке на GitHub в файле `GUIDE.md`.

## Тестовые аккаунты

| Роль | Email | Пароль |
|------|-------|--------|
| admin | admin@shop.ru | admin123 |
| manager | manager@shop.ru | manager123 |
| storekeeper | store@shop.ru | store123 |
| customer | user@shop.ru | user123 |

Промокод для теста: `WELCOME10` (10%).

## Авторизация

`POST /auth/login` возвращает `access_token` и `refresh_token`.
Токен передаётся в заголовке `Authorization: Bearer <access_token>`.
Обновить токены: `POST /auth/refresh` с телом `{"refresh_token": "..."}`.

## Заметки

- Поля в JSON в snake_case (`category_id`, `stock_quantity`, `is_active`).
- Статус заказа `new` и тип возврата `return` в JSON пишутся как в ТЗ.
- Чтобы работал конфигуратор, у комплектующих в `specs` должен быть ключ `component`:
  `cpu`, `motherboard`, `ram`, `gpu`, `psu`, `case`.
- Отзыв можно оставить только на товар из доставленного заказа.
- Возврат можно подать только по доставленному заказу.
- Кладовщик и админ имеют доступ к `/stock`, `/supplies`, `/suppliers`.
- Товары, способы оплаты и доставки при удалении не стираются, а скрываются (`is_active = false`).
