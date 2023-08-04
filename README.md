# api_final

## Описание:

REST API для Yatube. 
Через этот интерфейс смогут работать мобильное приложение или чат-бот; через него же можно будет передавать данные в любое приложение или на фронтенд.

## Как запустить проект:

__Клонировать репозиторий и перейти в него в командной строке:__

```
git clone https://github.com/Maksprots/api_final_yatube.git
```

```
cd api_final_yatube
```

__Cоздать и активировать виртуальное окружение:__

```
python3 -m venv env
```

```
source env/bin/activate
```

```
python3 -m pip install --upgrade pip
```

__Установить зависимости из файла requirements.txt:__

```
pip install -r requirements.txt
```

__Выполнить миграции:__

```
python3 manage.py migrate
```

__Запустить проект:__

```
python3 manage.py runserver
```

## Примеры:

### Пример POST-запроса с токеном на добавление нового поста.

    [POST] .../api/v1/posts/

    {
        "text": "Какой - то текст"
    }
    
__Пример ответа:__

    {
        "id": 14,
        "text": "Какой - то текст",
        "author": "user",
        "image": null,
        "group": 1,
        "pub_date": "2021-06-01T08:47:11.084589Z"
    }


### Пример POST-запроса с токеном на отправку нового комментария к посту с id=14.

    [POST] .../api/v1/posts/14/comments/
    {
        "text": "Какой то текст комментария",
    } 

__Пример ответа:__

    {
        "id": 4,
        "author": "anton",
        "post": 14,
        "text": "Какой то текст комментария",
        "created": "2021-06-01T10:14:51.388932Z"
    } 

### Пример GET-запроса с токеном на получение всех постов.

    [GET] .../api/v1/posts/

__Пример ответа:__

    {
        "id": 1,
        "author": "admin",
        "text": "gg",
        "pub_date": "2023-01-12T01:14:18.873001Z",
        "image": null,
        "group": null
    },
    {
        "id": 2,
        "author": "admin",
        "text": "gg",
        "pub_date": "2023-01-12T01:14:52.306199Z",
        "image": null,
        "group": null
    },
    {
        "id": 3,
        "author": "admin",
        "text": "gg",
        "pub_date": "2023-01-12T01:14:53.681446Z",
        "image": null,
        "group": null
    },


### Пример GET-запроса с токеном на получение информации о постах с ограничением в 2 поста и начиная со второго поста

    [GET] .../api/v1/posts/?limit=2&offset=2

__Пример ответа:__

    {
        "count": 13,
        "next": "http://127.0.0.1:8000/api/v1/posts/?limit=2&offset=4",
        "previous": "http://127.0.0.1:8000/api/v1/posts/?limit=2",
        "results": [
            {
                "id": 3,
                "author": "admin",
                "text": "gg",
                "pub_date": "2023-01-12T01:14:53.681446Z",
                "image": null,
                "group": null
            },
            {
                "id": 4,
                "author": "admin",
                "text": "gg",
                "pub_date": "2023-01-12T01:14:54.611741Z",
                "image": null,
                "group": null
            }
        ]
    }
### Пример GET-запроса с токеном на получение информации о группе.

    [GET] .../api/v1/groups/2/

__Пример ответа:__

    {
        "id": 2,
        "title": "Рассказы",
        "slug": "lirics",
        "description": "Группа рассказов"
    }