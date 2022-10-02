### [![Typing SVG](https://readme-typing-svg.herokuapp.com?color=%2336BCF7&lines=Проект+API+YaMDB+by+Y4R1K)](https://git.io/typing-svg)
![example workflow](https://github.com/94R1K/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
# Описание
Проект предназначен для взаимодействия с API социальной сети YaMDb. YaMDb собирает отзывы пользователей на различные произведения.

API предоставляет возможность взаимодействовать с базой данных по следующим направлениям:
- авторизироваться
- создавать свои отзывы и управлять ими (корректировать\удалять)
- просматривать и комментировать отзывы других пользователей
- просматривать комментарии к своему и другим отзывам
- просматривать произведения, категории и жанры произведений

# Переменные окружения
Проект использует базу данных PostgreSQL.
Для подключения и выполненя запросов к базе данных необходимо создать и заполнить файл .env с переменными окружения в папке /infra/.

Шаблон для заполнения файла .env:

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

### Как запустить проект:
Клонировать репозиторий и перейти в него в командной строке:

```
https://github.com/94R1K/infra_sp2.git
```

Создать и активировать виртуальное окружение:

```
python -m venv venv
```

```
source venv/Scripts/activate
```

Установить зависимости из файла requirements.txt:

```
cd api_yamdb
```

```
python -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```
Из папки /infra/ выполнить команду создания и запуска контейнеров:

```
docker-compose up -d
```

Выполнить миграции:

```
docker-compose exec web python manage.py migrate
```

Создать суперюзера:

```
docker-compose exec web python manage.py createsuperuser
```

Собрать статику:

```
docker-compose exec web python manage.py collectstatic --no-input 
```

Теперь проект доступен по адресу http://localhost/admin/

# Заполнение базы данных
Скопировать файл с дампом базы данных из папки /infra/ в контейнер:

```
docker cp fixtures.json infra-web-1:/app/fixtures.json
```
Заполнить базу данных из файла с дампом:

```
docker-compose exec web python manage.py loaddata fixtures.json
```

# Техническая информация
Стек технологий: Python 3, Django, Django Rest, Docker, PostgreSQL, nginx, gunicorn, simple JWT.

Веб-сервер: nginx (контейнер nginx)
Backend фреймворк: Django (контейнер web)
API фреймворк: Django REST (контейнер web)
База данных: PostgreSQL (контейнер db)

Веб-сервер nginx перенаправляет запросы клиентов к контейнеру web, либо к хранилищам (volume) статики и файлов.
Контейнер nginx взаимодействует с контейнером web через gunicorn.

### Дополнительное описание API доступно по http://localhost/redoc/

# Об авторе
Лошкарев Ярослав Эдуардович \
Python-разработчик (Backend) \
Россия, г. Москва \
E-mail: real-man228@yandex.ru \
VK: https://vk.com/94r1k \
Telegram: @y4r1k0
# Развернутый проект можно посмотреть по ссылкам:
http://158.160.6.170/api/v1/
http://158.160.6.170/admin/
http://158.160.6.170/redoc/
