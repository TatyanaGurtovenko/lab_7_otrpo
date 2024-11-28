# lab_7_otrpo

Два консольных приложения, одно из которых на входе из аргументов командной
строки принимает любой HTTP(S) URL, находит все внутренние ссылки (только для
этого домена) в HTML коде (a[href]), помещает их в очередь RabbitMQ по одной.
Второе приложение - "вечный" асинхронный producer/consumer, который читает из
очереди эти ссылки, также находит внутренние ссылки и помещает в их очередь
## Запуск

1. Клонируйте репозиторий:
    ```bash
    git clone https://github.com/TatyanaGurtovenko/lab_7_otrpo
    cd lab_7_otrpo
    ```


2. Установите необходимые зависимости:
    ```bash
    pip install -r requirements.txt
    ```


3. Создайте файл .env в корневой папке проекта и добавьте в него следующие переменные:
    ```bash
      RABBITMQ_HOST=localhost
      RABBITMQ_PORT=5672
      RABBITMQ_USER=
      RABBITMQ_PASSWORD=
      QUEUE_NAME=web_links
    ```

4. Запустите RabbitMQ с помощью Docker
    ```bash
       docker-compose up --build -d
    ```
    
5. Запустите producer (передайте URL в качестве аргумента):
 ```bash
   python producer.py url
 ```


6. Запустите consumer:
 ```bash
   python consumer.py
 ```
