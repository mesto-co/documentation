# API для получения собственного профиля
## /v1/user/:userid

| Параметр  | Значение  | 
|:----------|:----------|
| Method    | GET      |
| Authorization    | +  |
|Query parameters|- 	 |
### Сценарий
1. Получить авторизацию пользователя
1. Проверить, что токен не просрочен, если просрочен вернуть ошибку 419 - Authentication Timeout
1. Получить из БД по userId из path параметра запись о пользователе,
1. Получить из БД Список проектов пользователя, - Пока что не получаем.
1. Получить из БД Список контактов пользователя,
1. Отправить Ответ

### Модель данных
#### User
| Название  | Тип данных  | Описание | Обязательность (О/Н)
|:----------|:----------|:----------|:----------
| id | UUID | Уникальный идентификатор | О
| fullname|String|Полное имя пользователя|О
| role | String |Роль пользователя| Н
| about | String |О пользователе| Н
| imagePath | String |Ссылка на аватарку| Н
| email | String |email пользователя| Н
| location | String |локация пользователя| Н
| projects | Project[] | список проектов пользователя| Н
| contacts|Contact[]|Контакты пользователя|Н

#### Contact
| Название  | Тип данных  | Описание | Обязательность (О/Н)
|:----------|:----------|:----------|:----------
| id | UUID | Уникальный идентификатор | О
| title | String |Название контакта| О
| url | String |Ссылка на ресурс|О

### Пример ответа

``` json
{
    "role": "Founder",
    "fullname": "Дмитрий Бондарев",
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