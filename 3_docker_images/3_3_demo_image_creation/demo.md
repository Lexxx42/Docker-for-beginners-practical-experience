+ Добавить тег созданному образу докера

```docker
docker tag [id_container] [name]:[tag]
```

+ Отправить образ в хранилище

```docker
docker push [name]:[tag]
```

+ Нужно залогиниться в хранилище, чтобы туда пушить

```docker
docker login
```

Username, Password
[Запушил свой репозиторий](https://hub.docker.com/r/alex42konukhov/yandex-weather-bot)

> Make sure you have tagged your image in this format:
> {{username}}/{{imagename}}:{{version}}
> And push with
> [link](https://forums.docker.com/t/docker-push-error-requested-access-to-the-resource-is-denied/64468/10)

```docker
docker tag yandex-weather-bot:debian-bullseye alex42konukhov/yandex-weather-bot:debian-bullseye
```

```docker
docker push alex42konukhov/yandex-weather-bot:debian-bullseye
```

Чтобы спуллить репозиторий:

```docker
docker pull alex42konukhov/yandex-weather-bot:debian-bullseye
```
