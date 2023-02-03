![workflow status](https://github.com/Anton0530212/yamdb_final/blob/master/.github/workflows/yamdb_workflow.yml/badge.svg?event=push)


Это итоговый проект 16-го спринта. 
Задача: автотест на гитхаб экшн. Для развертывания проекта: 
   1.установите docker и docker-compose последней версии 
   2.перейдите в настройки гитхаба и создайте секретные ключи:

DB_ENGINE=django.db.backends.postgresql DB_NAME=postgres POSTGRES_USER= логин_для_пользователя POSTGRES_PASSWORD= пароль_для_пользователя DB_HOST=db DB_PORT=5432 далее откройте терминал, перейдите в папку yamdb_final/infra и пропишите команды: docker-compose up docker-compose exec web python manage.py migrate docker-compose exec web python manage.py createsuperuser docker-compose exec web python manage.py collectstatic --no-input если имеется бд: sudo docker cp путь_на_сервере/fixture.json контейнер:путь_в_контейнере/fixture.json sudo docker-compose exec web python manage.py loaddata fixtures2.json

автотест:

   проверка кода на PEP через flake8
   проверка внутренних тестов django
   сборка образа и пуш на докер хаб
   деплой на рабочий сервер
   при этом, необходимо добавить переменные окружения (settings в репозитории github->secrets and variables->actions)

DB_ENGINE-не обязательно-django.db.backends.postgresql DB_HOST-не обязательно-db DB_NAME-не обязательно-postgres DB_PORT-не обязательно-5432 POSTGRES_PASSWORD--не обязательно-ваш пароль от бд POSTGRES_USER-не обязательно-ваш логин от бд DEBUG- False либо True-режим дебага в settings.py django приложения DOCKER_PASSWORD-пароль от докер хаб DOCKER_USERNAME-логин от докер хаб USER-юзернейм для подключения к боевому серверу HOST-ip адрес боевого сервера SECRET_KEY-secret key в settings.py django приложения SSH_KEY- ssh key вашего компьютера TELEGRAM_TO-ваш телеграм id TELEGRAM_TOKEN-телеграм токен вашего бота для уведомления

проект развернут на 158.160.34.14/redoc/
