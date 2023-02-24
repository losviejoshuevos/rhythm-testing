# Задание №1

## Описание принципа работы программы

Данная программа представляет собой веб-чат на основе `WebSocket` с использованием фреймворка `FastAPI`.

Основной функционал реализован в классе `ConnectionManager`. Он отвечает за управление подключениями к веб-чату и отправку сообщений.

При запуске программы создается экземпляр класса `ConnectionManager` и инициализируется список активных подключений `active_connections`.

В методе `connect` происходит подключение нового `WebSocket` клиента. WebSocket - это двунаправленный протокол, поэтому перед началом работы с клиентом нужно выполнить шаг установки соединения. Это делается вызовом метода `await` `websocket.accept()`, который возвращает подтверждение успешного подключения клиенту.

В методе `disconnect` происходит отключение клиента от веб-чата.

Метод `send_personal_message` используется для отправки личного сообщения определенному клиенту.

Метод `broadcast` используется для отправки сообщения всем подключенным клиентам.

Далее, в основном приложении `FastAPI`, создается экземпляр класса `FastAPI()` и определяется HTML-шаблон, который будет использоваться для отображения страницы веб-чата.

В методе `get()` происходит возврат HTML-страницы в качестве ответа на GET-запрос к корневому пути ("/").

В методе `websocket_endpoint` обрабатывается WebSocket соединение. При подключении нового клиента вызывается метод `connect`, добавляющий новое подключение в список активных подключений и отправляющий сообщение об этом всем клиентам. Затем выполняется бесконечный цикл, который ожидает получения новых сообщений от клиента, отправляет ответное сообщение об успешном приеме и отправляет его всем клиентам. Если происходит обрыв соединения, вызывается метод `disconnect`, удаляющий соответствующее подключение из списка активных и отправляющий сообщение об этом всем клиентам.

Приложение запускается на локальном сервере с использованием библиотеки `Uvicorn`. Оно ожидает запросов на адрес 127.0.0.1:8000.

## Тест-кейсы

### Тест кейс: успешное подключение к чату и отправка сообщения.

Предусловие: сервер чата запущен и доступен клиенту по адресу http://127.0.0.1:8000.

Шаги:

1. Открыть браузер и перейти по адресу http://127.0.0.1:8000
2. Ввести сообщение в поле ввода и нажать кнопку "Send"

Ожидаемый результат: сообщение отображается в окне чата.

### Тест кейс: отключение от чата во время активной сессии.

Предусловие: сервер чата запущен и доступен клиенту по адресу http://127.0.0.1:8000.

Шаги:

1. Открыть браузер и перейти по адресу http://127.0.0.1:8000
2. Открыть DevTools и выполнить JavaScript-код для закрытия WebSocket-соединения: ws.close()

Ожидаемый результат: сообщение о том, что пользователь покинул чат, появляется в окне чата.

### Тест кейс: открытие нескольких сессий и передача сообщений между ними.

Предусловие: сервер чата запущен и доступен клиенту по адресу http://127.0.0.1:8000.

Шаги:

1. Открыть два браузера и перейти по адресу http://127.0.0.1:8000 в каждом из них.
2. Отправить сообщение из одного браузера и убедиться, что оно отображается в другом браузере.

Ожидаемый результат: сообщение отображается в обоих окнах чата.