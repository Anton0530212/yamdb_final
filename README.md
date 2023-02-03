![workflow](https://github.com/Anton0530212/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?event=push)


# REST API для проекта YaMDb

## Описание
Простой, надежный и понятный API социальной сети с базой данных отзывов к произведениям.

## Технологии
Python 3,
Django 2.2,
Django REST Framework,
Simple-JWT

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
git clone https://github.com/Wests007/api_yamdb.git
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

### Полная документация запросов к API доступна после запуска сервера по адресу:
```
http://localhost/redoc
```

### Примеры запросов к API:

- Регистрация
POST /api/v1/auth/signup/
```
{
    "email": "string",
    "username": "string"
}
```

- Получение токена
POST /api/v1/auth/token/
```
{
    "username": "string",
    "confirmation_code": "string"
}
```

- Редактирование пользовательского профиля
PATCH /api/v1/users/me/
```
{
    "username": "string",
    "email": "user@example.com",
    "first_name": "string",
    "last_name": "string",
    "bio": "string"
}
```

- Получение списка всех категорий
GET /api/v1/categories/
```
[
    {
        "count": 0,
        "next": "string",
        "previous": "string",
        "results":
            [
                {
                    "name": "string",
                    "slug": "string"
                }
            ]
    }
]
```

- Получение списка всех жанров
GET /api/v1/genres/
```
[
    {
        "count": 0,
        "next": "string",
        "previous": "string",
        "results":
            [
                {
                    "name": "string",
                    "slug": "string"
                }
            ]
    }
]
```

- Добавление нового отзыва
POST /api/v1/titles/{title_id}/reviews/
```
{
    "text": "string",
    "score": 1
}
```

- Добавление комментария к отзыву
POST /api/v1/titles/{title_id}/reviews/{review_id}/comments/
```
{
    "text": "string"
}
```

## Авторы:
[Левина Юля](https://github.com/JulLevina),
[Андрей Пахомов](https://github.com/pakhem),
[Антон Плотицын](https://github.com/Anton0530212)
