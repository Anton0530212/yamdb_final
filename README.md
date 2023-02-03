![workflow](https://github.com/Anton0530212/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?event=push)


# REST API для проекта YaMDb

## Описание
Простой, надежный и понятный API социальной сети с базой данных отзывов к произведениям.

## Технологии
- Python 3.7
- Django 2.2.16
- DRF 3.12.4
- Simple-JWT

### Шаблон наполнения env-файла:
```
DB_ENGINE=... # указываем, что работаем с postgresql
DB_NAME=... # имя базы данных
POSTGRES_USER=... # логин для подключения к базе данных
POSTGRES_PASSWORD=... # пароль для подключения к БД (установите свой)
DB_HOST=... # название сервиса (контейнера)
DB_PORT=... # порт для подключения к БД
```

### Как запустить проект:
Клонировать репозиторий и перейти в него в командной строке:
```
git clone https://github.com/Anton0530212/yamdb_final
```
```
cd infra_sp2
```
Запустить приложение через docker-контейнеры:
```
cd infra
```
```
docker-compose up -d --build
```
Выполнить миграции и собрать статику:
```
docker-compose exec web python manage.py migrate
```
```
docker-compose exec web python manage.py collectstatic --no-input
```
При необходимости, БД возможно наполнить тестовыми данными:
```
docker-compose exec web python manage.py import_csv_to_db
```
Остановить работу контейнеров и удалить их (сохранив образы):
```
docker-compose down -v
```

#### _Алгоритм регистрации пользователей_
1. Пользователь отправляет POST-запрос на добавление нового пользователя с параметрами email и username на эндпоинт /api/v1/auth/signup/.
2. YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email.
3. Пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен).
4. При желании пользователь отправляет PATCH-запрос на эндпоинт /api/v1/users/me/ и заполняет поля в своём профайле (описание полей — в документации).

- Запрос на регистрацию пользователя:
```
POST auth/signup/
```
```
body:
{
    "username": "Test_User",
    "email": "Test_email@test.ru"
}
```
- вернет следующий ответ
```
{
    "username": "Test_User",
    "email": "Test_email@test.ru"
}
```

#### _Примеры запросов к API для неавторизованных пользователей_
Неавторизованные пользователи могут просматривать описания произведений, читать отзывы и комментарии.
- Пример запроса на получения информации о произведении по id:
```
GET api/v1/titles/{titles_id}/
```
- Ответ:
```
{
    "id": 0,
    "name": "string",
    "year": "test_text",
    "rating": "string"
    "description": "string",
    "genre": [
        {...}
    ],
    "category": {
    "name": "string",
    "slug": "string"
    }
}
```

#### _Примеры запросов к API для авторизованных пользователей_
Авторизованные пользователи наделены правом создания, изменения и удаления отзывов и комментариев, авторами которого они являются.
- Для авторизации зарегистрированному пользователю, получившему на указанную при регистрации эл.почту код подтверждения, необходимо получить JWT-токен с помощью следующего запроса
```
POST api/v1/auth/token/
```
```
body:
{
    "username": "Test_User",
    confirmation_code": "string"
}
```

"access" - поле, содержащее токен.

- Запрос на создание отзыва на произведение:
```
POST api/v1/titles/{titles_id}/reviews/
```
```
body:
{
    "text": "string",
    "score": 1
}
```
- вернет следующий ответ
```
{
    "id": 0,
    "text": "string",
    "author": "string",
    "score": 1,
    "pub_date": "2019-08-24T14:15:22Z"
}
```
- Сайт доступен по адресу:(http://158.160.34.14/redoc/)
- Подробнее про установку DRF можно почитать [здесь](https://github.com/encode/django-rest-framework/blob/master/README.md )


## Авторы:
[Левина Юля](https://github.com/JulLevina),
[Андрей Пахомов](https://github.com/pakhem),
[Антон Плотицын](https://github.com/Anton0530212)
