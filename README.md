# API_YAMDB
REST API проект для сервиса YaMDb — сбор отзывов о фильмах, книгах или музыке.

## Описание

API для получения информации и обсуждения наиболее интересных произведений.
Для автоматизации развертывания на боевых серверах используется среда виртуализации Docker, а также Docker-compose - инструмент для запуска многоконтейнерных приложений.

## Стек технологий:
- Python 3
- DRF (Django REST framework)
- Django ORM
- Docker
- Gunicorn
- Nginx
- Django 2.2 TLS
- PostgreSQL
- GIT

## Установка
##### Шаг 1. Проверьте установлен ли у вас Docker
Прежде, чем приступать к работе, необходимо знать, что Docker установлен. Для этого достаточно ввести:
```bash
docker -v
```
Или скачайте [Docker Desktop](https://www.docker.com/products/docker-desktop) для Mac или Windows. [Docker Compose](https://docs.docker.com/compose) будет установлен автоматически. В Linux убедитесь, что у вас установлена последняя версия [Compose](https://docs.docker.com/compose/install/). Также вы можете воспользоваться официальной [инструкцией](https://docs.docker.com/engine/install/).

##### Шаг 2. Клонируйте репозиторий себе на компьютер
Введите команду:
```bash
git clone https://github.com/DenisSivko/infra_sp2.git
```

##### Шаг 3. Создайте в клонированной директории файл .env
Пример:
```bash
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

##### Шаг 4. Запуск docker-compose
Для запуска необходимо выполнить из директории с проектом команду:
```bash
docker-compose up -d
```

##### Шаг 5. База данных
Создаем и применяем миграции:
```bash
docker-compose exec web python manage.py makemigrations --noinput
docker-compose exec web python manage.py migrate --noinput
```

##### Шаг 6. Подгружаем статику
Выполните команду:
```bash
docker-compose exec web python manage.py collectstatic --no-input 
```

##### Шаг 7. Заполнение базы тестовыми данными
Для заполнения базы тестовыми данными вы можете использовать файл fixtures.json, который находится в infra_sp2. Выполните команду:
```bash
docker-compose exec web python manage.py loaddata fixtures.json
```

##### Другие команды
Создание суперпользователя:
```bash
docker-compose exec web python manage.py createsuperuser
```

Остановить работу всех контейнеров можно командой:
```bash
docker-compose down
```

Для пересборки и запуска контейнеров воспользуйтесь командой:
```bash
docker-compose up -d --build 
```

Мониторинг запущенных контейнеров:
```bash
docker stats
```

Останавливаем и удаляем контейнеры, сети, тома и образы:
```bash
docker-compose down -v
```

##Документация к API доступна по адресу `http://127.0.0.1/redoc/`
