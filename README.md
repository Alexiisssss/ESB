# ESB API на MuleSoft

## Описание

Этот проект реализует REST API для обработки заказов с использованием **MuleSoft Anypoint Platform** и **PostgreSQL**.

## Функциональность API

- `POST /orders` — создание заказа
  
- `GET /orders/{id}` — получение информации о заказе
  
- `PUT /orders/{id}/status` — обновление статуса заказа
  
- `DELETE /orders/{id}` — удаление заказа


## Используемые технологии

- **MuleSoft Anypoint Studio**
  
- **PostgreSQL** для хранения данных
  
- **ActiveMQ** для очередей сообщений
  
- **DataWeave** для трансформации данных


## Запуск проекта

1. Установите PostgreSQL и создайте базу `ordersdb`.
   
2. Запустите ActiveMQ (`activemq start`).
   
3. Откройте проект в **MuleSoft Anypoint Studio** и разверните API.
   
4. API доступен по адресу `http://localhost:8081`.


## Проверка сообщений в ActiveMQ

*Если ActiveMQ запущен локально, открой браузер и перейди по адресу:

http://localhost:8161/admin

*Логин и пароль по умолчанию:

login: admin

password: admin

*Запустите сервер:

activemq start


*Выполнить PUT-запрос к http://localhost:8081/orders/{id}/status к примеру в Postman

http://localhost:8081/orders/{id}/status

В body:

{
  "status": "Shipped"
}

status OK 200:

{
  "message": "Order status updated successfully"
}


В ActiveMQ Web Console (http://localhost:8161/admin) открыть Queues.

Найди очередь order_status_updates (или ту, которая у выс указана в jms:publish)

Убедитесь, что в Messages Enqueued (количество сообщений в очереди) есть хотя бы одно сообщение.

Если сообщения нет, значит MuleSoft не отправляет его, в этом случае используйте логирование в MuleSoft.



## Тестирование API в Postman

http://localhost:8081

- **POST /orders**

  {
    "client": "Иван Иванов",
    "amount": 1500,
    "status": "new"
  }


**GET /orders/1**

**PUT /orders/1/status**

{
  "status": "shipped"
}

**DELETE /orders/1**
