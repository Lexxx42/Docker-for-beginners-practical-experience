# Лабораторные работы

Чтобы узнать версию докера на хосте

```docker
docker version
```

Чтобы остановить + начало id

```docker
docker stop 5a
```

Удалить все остановленные

```docker
docker stop $(docker ps -aq)
```

Запустить образ, указав имя образа

```docker
docker run --name webapp nginx:1.14-alpine
```

Удалить все образы находящиеся локально на хосте + первые символы id

```docker
docker rmi 98 62 1b
```

```docker
docker rmi -f $(docker images)
```
