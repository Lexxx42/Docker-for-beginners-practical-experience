# Тест: Compose

> Для работы с docker-compose требуются знания YAML. В версии Stepik в курсе нет лекции по YAML, но она и
> соответствующая лабораторная есть в моем курсе Ansible https://stepik.org/course/123806 или в курсе Docker для
> начинающих на https://rotoro.cloud в разделе приложений, проверь это, если еще не знаком с этим языком разметки.
> Как обычно, эти тесты основаны не только на материалах лекций - отнесись к этому с пониманием и учись работать с
> документацией.
> Еще раз упомяну - эти тесты сложнее материала для новичков и требуются, только если ты хочешь сертификат об окончании.
> Если тебя это задевает и ты считаешь, что курс стал от них хуже - просто пропусти эти тесты.
> Эти ссылки помогут в прохождении теста:
> https://docs.docker.com/compose/reference/
> https://docs.docker.com/compose/compose-file/
> https://rotoro.cloud/topic/%d0%b2%d0%b2%d0%b5%d0%b4%d0%b5%d0%bd%d0%b8%d0%b5-%d0%b2-yaml/

1. При помощи чего мы можем настроить контейнеры и связь между ними используя декларативный подход?

> Docker Compose

2. Какой YAML-файл, содержащий описание services, networks и volumes для развертывания контейнеризированного приложения,
   обычно используется?

> docker-compose.yaml

3. Какая команда используется для создания и запуска контейнеров на переднем плане, используя готовый файл
   docker-compose.yaml?

> docker-compose up

4. Какая команда используется для создания и запуска контейнеров на заднем плане, используя готовый файл
   docker-compose.yaml?

> docker-compose up --detach
> docker-compose up -d

5. Как посмотреть список созданных compose контейнеров?

> docker-compose ps

6. Какая команда поможет в проверке логов всего стека, указанного в docker-compose.yaml?

> docker-compose logs

7. Какой командой можно остановить (не удаляя) весь стек контейнеров, описанных в compose-файле?

> docker-compose stop

8. Какой командой можно удалить весь стек контейнеров, описанных в compose-файле?

> docker-compose down

9. Как используется поле version в compose-файле? (выбери 3)

> docker-compose использует максимально последнюю подходящую схему, не ориентируясь на версию
> Поле версии носит лишь информативный характер
> docker-compose анализирует файл и самостоятельно принимает решение о том, по схеме какой версии работать

> Top-level version property is defined by the specification for backward compatibility but is only informative.
> A Compose implementation SHOULD NOT use this version to select an exact schema to validate the Compose file, but
> prefer
> the most recent schema at the time it has been designed.
>
>Compose implementations SHOULD validate whether they can fully parse the Compose file. If some fields are unknown,
> typically because the Compose file was written with fields defined by a newer version of the specification, Compose
> implementations SHOULD warn the user. Compose implementations MAY offer options to ignore unknown fields (as defined
> by “loose” mode).

10. Compose-файлы версий 2 и 3 должны явно указывать свою версию в корневом разделе YAML документа?

> Да

> Вкратце, композ парсит файл и по инструкциям сам понимает, до какой версии опускаться. Но версии все же нужно
> указывать, это нужно не только в информационных целях для пользователей, которые смотрят в репо с развертыванием, но и
> для композа, поскольку версии 2 и 3 несовместимы, и он это проверяет, если хотят применить третью поверх второй
> например.

11. Используя команду docker-compose up мы можем поднять несколько контейнеров на разных докер-хостах?

> Нет

12. На какой порт хоста будет выставлено приложение при исполнении docker-compose up -d?

```
docker-compose.yaml:

version: "3.8"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
    volumes:
      - .:/code
      - logvolume01:/var/log
    ports:
      - "8080:80"
  redis:
    image: redis
  db:
    image: postgres
volumes:
  logvolume01: {}
```

> 8080

13. Что из утверждений верно?

```
docker-compose.yaml:

version: "3.8"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
    volumes:
      - .:/code
      - logvolume01:/var/log
    ports:
      - "8080:80"
  redis:
    image: redis
  db:
    image: postgres
volumes:
  logvolume01: {}
```

> Образ web будет собран, а образы redis и postgres будут скачаны с Dockerhub, если их еще нет на хосте

14. Что можно сказать о монтированиях для службы web в этом compose-файле?

> Примечание: о монтировании мы будем говорить в теме хранения

```
docker-compose.yaml:

version: "3.8"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
    volumes:
      - .:/code
      - logvolume01:/var/log
    ports:
      - "8080:80"
  redis:
    image: redis
  db:
    image: postgres
volumes:
  logvolume01: {}
```

> /code это Bind Mount, /var/log это Volume mount

15. Что из утверждений верно об этом файле?

```
docker-compose.yaml:

version: "3.8"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
    volumes:
      - .:/code
      - logvolume01:/var/log
    ports:
      - "8080:80"
  redis:
    image: redis
  db:
    image: postgres
volumes:
  logvolume01: {}
```

> Службы redis и db должны будут запуститься до службы web
