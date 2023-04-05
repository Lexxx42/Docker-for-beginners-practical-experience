# Лабораторная №6 (Docker Compose)

1. Создай экземпляр базы данных postgres в контейнере с названием db, образ postgres, переменные окружения
   POSTGRES_PASSWORD=mysecretpassword

Если ты не уверен в правильности, посмотри в подсказке.

```docker
docker run --name db -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

2. Теперь создай простой контейнер с wordpress, он должен называться wordpress, образ: wordpress, сделай link этому
   контейнеру к контейнеру с именем db выставь 30085 порт на докер-хост

Если ты не уверен в правильности, посмотри в подсказке.

```docker
docker run -d --name wordpress -p 30085:80 --link db:db wordpress
```

3. Сейчас у нас уже развернут рабочий сайт на wordpress, ты можешь посмотреть на него через вкладку в терминале. Давай
   теперь сделаем это с помощью Docker Compose!

Если ты видишь ответ Страница недоступна, поменяй в URL протокол на https

Сначала надо прибрать за собой, давай удалим все, что осталось от предыдущих шагов.

Удали все контейнеры - db и wordpress

``docker
docker ps -a
``

```docker
docker stop
```

```docker
docker rm
```

4. Создай файл docker-compose.yml в размещении /root/wordpress. Обрати внимание, размещение должно быть
   /root/wordpress/docker-compose.yml, иначе система не сможет правильно проверить результат. Сделай sudo -i, пароль
   selena. После этого запусти стек с помощью docker-compose в detached mode.

Важно, чтобы в файле спецификация была такой же, как и раньше, т.е. контейнеры были wordpress и db и не забудь прокинуть
нужные порты

```shell
sudo su
```

```shell
cd /root/wordpress
```

```shell
touch docker-compose.yml
```

```shell
nano docker-compose.yml
```

5.

```
docker-compose.yaml:

version: "3"
services:
  wordpress:
    image: wordpress
    ports:
      - "30085:80"
    links:
      - db
  db:
    image: postgres
    environment:
      - POSTGRES_PASSWORD=mysecretpassword
```

```docker
docker-compose up -d
```

6. Мы что-то поменяли, сколько реплик контейнеров в службе wordpress?

```docker
docker-compose ps
```

7. Увеличь количество реплик wordpress до 2.

```docker
docker-compose up -d --scale wordpress=2
```

```docker
docker-compose ps
```

8. Останови стек docker-compose.
   Убедись, что Docker Compose корректно положил стек

```docker
docker-compose down
```

```docker
docker-compose ps
```
