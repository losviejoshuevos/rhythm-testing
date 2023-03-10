# Задание №2

## Описание принципа работы программы

Это приложение, которое предоставляет интерфейс для получения данных из базы данных. Оно реализовано на основе библиотеки `FastAPI` и содержит два адреса для получения данных: `"/get_genres"` и `"/get_data/{genre_id}"`.

Первый адрес `"/get_genres"` возвращает список жанров из базы данных в формате словаря, где ключом является id жанра, а значением - название жанра.

Второй адрес `"/get_data/{genre_id}"` возвращает список записей поля "композитор" в жанре с заданным id в формате словаря, где ключом является имя композитора, а значением - название трека. Кроме того, в словарь также добавляется количество таких записей.

файл `main.py` содержит конфигурацию и запуск сервера. Файл `ping.py` содержит определения адресов для получения данных. Файл `test.db` является базой данных, а файл `db.py` используется для подключения к этой базе данных и выполнения SQL-запросов.

## Тест-кейсы для программы:

### Тест-кейс для функции get_genres:

Предусловия:
Наличие файла базы данных `test.db`.
Программа запущена и доступен клиенту по адресу http://127.0.0.1:8000.

Шаги:

1. Открыть программу Postman.
2. Отправить GET-запрос на адрес http://127.0.0.1:8000/ping_page/get_genres.
3. Получить ответ от сервера.

Ожидаемый результат:
Статус-код ответа 200.
Ответ содержит словарь вида "id: name" всех жанров, присутствующих в базе данных.

### Тест-кейс для функции get_data:

Предусловия:
Наличие файла базы данных `test.db`.
Программа запущена и доступен клиенту по адресу http://127.0.0.1:8000.

Шаги:

1. Открыть программу Postman.
2. Отправить GET-запрос на адрес http://127.0.0.1:8000/ping_page/get_data/{genre_id}, где {genre_id} - идентификатор жанра, для которого необходимо получить данные.
3. Получить ответ от сервера.

Ожидаемый результат:
Статус-код ответа 200.
Ответ содержит словарь вида "composer: name" всех уникальных записей по полю "композитор" в требуемом жанре, отсортированных по композитору, а также количество таких записей в тот же словарь.

### Тест-кейс для функции pong:

Предусловия:
Наличие файла базы данных `test.db`.
Программа запущена и доступен клиенту по адресу http://127.0.0.1:8000.

Шаги:

1. Открыть программу Postman.
2. Отправить GET-запрос на адрес http://127.0.0.1:8000/ping_page/ping.
3. Получить ответ от сервера.

Ожидаемый результат:
Статус-код ответа 200.
Ответ содержит словари со строкой "ping": "pong!", "environment": "Test task" и "testing": "testing".
