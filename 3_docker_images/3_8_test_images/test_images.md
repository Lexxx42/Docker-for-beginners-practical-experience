# Тест: Images

Есть несколько best practices при создании образов для докер-контейнеров. Эти рекомендации помогают получить
производительные и безопасные решения.

А именно, это такие вещи, как:

+ контроль за базовыми образами, на которых построены твои образы
+ контроль за размером образа
+ контроль за пакетами в образе
+ контроль за уязвимостями в образе
+ контроль за хранением в образе

Для каждого из этих векторов есть специальные методы оценки и митигации. На моем ресурсе rotoro.cloud в курсе Certified
Kubernetes Security Specialist мы подробно обсуждаем эти вопросы и учимся собирать образы правильно. Если у тебя там
есть подписка, можешь пройти те лабораторные.

Еще раз упомяну - эти тесты сложнее материала для новичков и требуются, только если ты хочешь сертификат об окончании.
Если тебя это задевает и ты считаешь, что курс стал от них хуже - просто пропусти эти тесты.

Вот полезные ссылки:

https://docs.docker.com/engine/reference/builder/

https://docs.docker.com/develop/develop-images/dockerfile_best-practices/

https://docs.docker.com/language/golang/build-images/

https://docs.docker.com/build/building/multi-stage/

https://docs.docker.com/build/building/context/

https://docs.docker.com/engine/reference/commandline/history/

1. После сборки образ назвали parser. Что произойдет, если мы запустим команду: docker run parser sleep 1h?

> Dockerfile:
> FROM ubuntu:20.04
> COPY . /app
> RUN make /app
> CMD python /app/app.py

```
Docker изменит инструкцию CMD на 'sleep 1h'
```

2. Выбери инструкцию CMD для команды echo -n "My home is $HOME", которая выводит значение переменной окружения и
   считается предпочитаемой.

> The CMD instruction is used to specify the default command to run when a container is started from the Docker image.
> The
> CMD instruction allows you to set a default command or parameters, which can be overridden by users when they run the
> container.

> In this example CMD [ "sh", "-c", "echo -n My home is $HOME" ], the default command is set to run the shell (sh) and
> execute the command echo -n My home is $HOME. The command will print the string "My home is" followed by the value of
> the $HOME environment variable. The -n option is used to suppress the newline at the end of the output.

> The CMD instruction must be specified in the Dockerfile, and it is the last command that is executed when the
> container
> is started. If there are multiple CMD instructions in the Dockerfile, only the last one will be executed. If a user
> specifies a command to run when starting the container, it will override the CMD instruction in the Dockerfile.

```
CMD [ "sh", "-c", "echo -n My home is $HOME" ]
```

3. Мы решили создать свой образ и в процессе его сборки требуется скачать файл с https://rootfs.tar.xz и автоматически
   распаковать пути /. Какую команду выбрать?

```
ADD https://rootfs.tar.xz /
```

4. Что поможет уменьшить размер образа?

```
1. Установка только необходимых пакетов в образ
2. Использовать multi-stage сборки
3. Предотвращение копирования нежелательных файлов в контекст сборки при помощи '.dockerignore'
4. Комбинирование нескольких инструкций в одну и очистка временных файлов в этой же инструкции
```

5. Как определить, что Dockerfile содержит в себе multi-stage?

```
В Dockerfile присутствуют несколько инструкций FROM
```

6. Изучи Dockerfile. Какое значение нужно добавить после флага --from во второй стадии сборки, чтобы скомпилированный
   бинарник go-приложения из первой стадии был помещен в финальный образ?

```
Dockerfile:

FROM golang:1.12-alpine as builder

ENV GO111MODULE=on

WORKDIR /app
COPY . .

RUN apk --no-cache add git alpine-sdk build-base gcc

RUN go get \
    && go get golang.org/x/tools/cmd/cover \
    && go get github.com/mattn/goveralls

RUN go build -o example cmd/example/main.go

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=<неизвестно> /app/example .
CMD ["./example"]
```

```
builder
```

7. Какая команда напечатает значения 'Architecture' и 'Os' образа с названием rockets?

```docker
docker image inspect rockets -f '{{.Os}} {{.Architecture}}'
```

8. Если мы используем CMD для предоставления аргумента по умолчанию для инструкции ENTRYPOINT, то должны быть указаны
   обе инструкции, как CMD, так и ENTRYPOINT?

```
Да
```

9. Какая команда удалит все неиспользуемые образы на докер-хосте?

```docker
docker image prune -a
```

10. Как собрать образ при помощи Dockerfile из директории /opt/prj01/, используя для контекста путь /opt/prj01/v2 и
    назвать этот образ app:v2?

```
У нас есть директория с 

$ tree /opt/prj01/
/opt/prj01/
|-- Dockerfile
|-- v1
|   `-- app.py
`-- v2
    `-- app.py
```

```docker
docker build /opt/prj01/v2 -f /opt/prj01/Dockerfile -t app:v2
```

11. Как увидеть список всех слоев образа redis вместе с размером каждого слоя?

