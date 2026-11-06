# API для Yatube

## Описание

REST API для социальной сети **Yatube**. Позволяет публиковать посты,
комментировать их, просматривать сообщества и подписываться на других
авторов. Аутентификация — по JWT-токенам.

Неаутентифицированные пользователи имеют доступ только на чтение
(кроме `/follow/` — он доступен только авторизованным). Изменять и
удалять контент может только его автор.

## Технологии

- Python 3.9+
- Django 3.2
- Django REST Framework 3.12
- Simple JWT

## Установка

Клонировать репозиторий и перейти в него:

```bash
git clone https://github.com/ivandarovskoy/api-final-yatube-ad.git
cd api-final-yatube-ad
```

Создать и активировать виртуальное окружение:

```bash
python3 -m venv venv
source venv/bin/activate
```

Установить зависимости:

```bash
python3 -m pip install --upgrade pip
pip install -r requirements.txt
```

Выполнить миграции и запустить проект:

```bash
cd yatube_api
python3 manage.py migrate
python3 manage.py runserver
```

Документация будет доступна по адресу `http://127.0.0.1:8000/redoc/`.

## Примеры запросов

Получить JWT-токен:

```
POST /api/v1/jwt/create/
{
    "username": "user",
    "password": "password"
}
```

Получить список публикаций (с пагинацией):

```
GET /api/v1/posts/?limit=10&offset=0
```

Создать публикацию (заголовок `Authorization: Bearer <access>`):

```
POST /api/v1/posts/
{
    "text": "Текст публикации",
    "group": 1
}
```

Добавить комментарий:

```
POST /api/v1/posts/1/comments/
{
    "text": "Комментарий"
}
```

Подписаться на пользователя:

```
POST /api/v1/follow/
{
    "following": "username"
}
```

Поиск по подпискам:

```
GET /api/v1/follow/?search=user
```
