# API для получения собственного профиля
## /v1/profile/search

| Параметр  | Значение  | 
|:----------|:----------|
| Method    | POST      |
| Authorization    | +  |
|Query parameters|- 	 |

### Сценарий
1. Получить авторизацию пользователя
1. Проверить, что токен не просрочен, если просрочен вернуть ошибку 419 - Authentication Timeout
2. Осуществить выборку пользователей из БД по поисковому запросу удовлетворяющие услованиям поиска - ILIKE %query%. Поиск провести по полям, fullname, username, about, location, skills
3. Получить из БД список Skills пользователя
4. Отправить Ответ

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
| skills|json|Контакты пользователя|Н

### Пример запроса
``` json
{
    "RqUid": "1F15EFD8-0158-4CCB-9A7D-8846CDA307B2",
    "query": [
        {
            "username": "iry",
            "fullname" : "iry",
            "location" : "iry",
            "about" : "iry",
            "role" : "iry"
        }
    ],
    "currentPage": 1,
    "perPage": 1000,
    "onlyFriends": false
}
```


### Пример ответа

``` json
[{
    "role": "Founder",
    "fullname": "Дмитрий Бондарев",
    "skills": [
      "Управление проектам",
      "Project mangment"
    ],
    "about": "Serial entrepreneur for 28 of my 53 years. 8 startups, 2 exits. \nПомогаю техническим командам сделать проект бизнесом.",
    "imagePath": "https://i.imgur.com/CQKb2yw.jpg",
    "email": "dmitry.bondarev@gmail.com",
    "location": "St.-Petersburg",
    "id": "some uuid string",
    "projects": []
}]
```