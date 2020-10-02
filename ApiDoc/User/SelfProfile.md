# API для получения собственного профиля
## /v1/user

| Параметр  | Значение  | 
|:----------|:----------|
| Method    | GET      |
| Authorization    | +  |
|Query parameters|- 	 |
### Сценарий
1. Получить авторизацию пользователя
1. Проверить, что токен не просрочен, если просрочен вернуть ошибку 419 - Authentication Timeout
1. Получить из БД по токену запись о пользователе,
1. Получить из БД Список проектов пользователя, - Пока что не получаем.
1. Получить из БД Список контактов пользователя,
1. Отправить Ответ

### Пример ответа

``` json
{
    "role": "Founder",
    "name": "Дмитрий Бондарев",
    "contacts": [
        {
            "id": 64,
            "title": "Telegram",
            "link": "http://t.me/dmitrybondarev"
        },
        {
            "id": 61,
            "title": "Openland",
            "link": "https://openland.com/bondarev"
        },
        {
            "id": 63,
            "title": "LinkedIn",
            "link": "https://www.linkedin.com/in/bondarev/"
        },
        {
            "id": 62,
            "title": "Facebook",
            "link": "https://www.facebook.com/dmitry.bondarev.75"
        }
    ],
    "about": "Serial entrepreneur for 28 of my 53 years. 8 startups, 2 exits. \nПомогаю техническим командам сделать проект бизнесом.",
    "imagePath": "https://i.imgur.com/CQKb2yw.jpg",
    "email": "dmitry.bondarev@gmail.com",
    "location": "St.-Petersburg",
    "id": "some uuid string",
    "projects": []
}
```