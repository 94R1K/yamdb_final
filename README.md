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
https://github.com/94R1K/yamdb_final.git
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

# Техническая информация
Стек технологий: Python 3, Django, Django Rest, Docker, PostgreSQL, nginx, gunicorn, simple JWT.

Веб-сервер: nginx (контейнер nginx)
Backend фреймворк: Django (контейнер web)
API фреймворк: Django REST (контейнер web)
База данных: PostgreSQL (контейнер db)

Веб-сервер nginx перенаправляет запросы клиентов к контейнеру web, либо к хранилищам (volume) статики и файлов.
Контейнер nginx взаимодействует с контейнером web через gunicorn.

### Дополнительное описание API доступно по http://158.160.6.170/redoc/

# Об авторе
Лошкарев Ярослав Эдуардович \
Python-разработчик (Backend) \
Россия, г. Москва \
E-mail: real-man228@yandex.ru 

[![VK](https://img.shields.io/badge/Вконтакте-%232E87FB.svg?&style=for-the-badge&logo=vk&logoColor=white)](https://vk.com/yalluv)
[![TG](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/yallluv)
