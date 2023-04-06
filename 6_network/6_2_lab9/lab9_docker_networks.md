# Лабораторная №9 (Docker Networks)

1. Исследуй текущее окружение Docker и определи, какое количество networks присутствует в системе

```shell
docker network ls
```

2. Какой ID соответствует мостовой сети (bridge network)?

```shell
docker network ls
```

3. Мы только что запустили контейнер с названием alpine-1. Определи к какой сети он присоединен.

```shell
docker inspect alpine-1
```

4. Какая подсеть сконфигурирована в сети bridge?

```shell
docker network inspect bridge
```

5. Запусти контейнер с названием alpine-2 с помощью образа alpine и прикрепи его к сети none.

```shell
docker run -d --name alpine-2 --network=none alpine sleep 100
```

6. Создай новую сеть с названием wp-mysql-network, которая будет использовать сетевой драйвер bridge. Назначь ей
   172.22.0.0/24 подсеть. Настрой Gateway 172.22.0.1

```shell
docker network create --driver bridge --subnet 172.22.0.0/24 --gateway 172.22.0.1 wp-mysql-network
```

7. Разверни базу mysql с помощью образа mysql. Контейнер должен называться mysql-db. Прикрепи его к только что созданной
   сети wp-mysql-network
   Установи пароль для использования базы данных db_pass123. Переменная окружения, ответственная за это
   MYSQL_ROOT_PASSWORD

```shell
docker run -d -e MYSQL_ROOT_PASSWORD=db_pass123 --name mysql-db --network wp-mysql-network mysql
```

8. Разверни веб-приложение с названием webapp, используй образ rotorocloud/webapp-mysql. Выставь (Expose) порт 30080 на
   хост. Приложение использует переменную окружения DB_Host в качестве имени хоста базы данных mysql. Убедись, что
   прикрепил вновь созданную сеть wp-mysql-network

```shell
docker run --network=wp-mysql-network -e DB_Host=mysql-db -e DB_Password=db_pass123 -p 30080:8080 --name webapp -d rotorocloud/webapp-mysql
```
