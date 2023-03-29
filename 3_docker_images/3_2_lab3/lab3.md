# Лабораторная 3: образы

1. Сколько images доступно на докер-хосте?

```docker
docker images
```

2. Какой размер образа ubuntu?

```docker
docker images
```

3. Какой тег у нового образа NGINX?
   ИНФО: Мы только что спуллили новый образ.

```docker
docker images
```

4. Мы только что скачали код приложения. Какой базовый образ используется в этом Dockerfile?
   Ищи Dockerfile в директории /var/webapp-rockets.

```shell
cd /var/webapp-rockets
```

```shell
ll
```

```shell
cat Dockerfile
```

```
FROM python:3.6

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python3", "app.py"]
```

5. В какое расположение внутри контейнера будет скопирован исходный код во время создания образа?
   Исследуй Dockerfile в директории /var/webapp-rockets.

```shell
cat Dockerfile
```

6. Когда контейнер создан с помощью этого Dockerfile, какая команда используется для запуска приложения внутри него?
   Исследуй Dockerfile в директории /var/webapp-rockets.

```shell
cat Dockerfile
```

```shell
python3 app.py
```

7. Какой port у приложения внутри контейнера?
   Исследуй Dockerfile в директории /var/webapp-rockets.

8080

8. Создай докер-образ используя этот Dockerfile и назови его webapp-rockets. Не присваивай никаких тегов.

```docker
docker build . -f Dockerfile -t webapp-rockets
```

9. Запусти экземпляр образа webapp-rockets и опубликуй порт 8080 контейнера на 30082 порту докер-хоста.

```docker
docker run -d -p 30082:8080 webapp-rockets
```

10. Открой веб-приложение используя вкладку приложения в обучающем модуле.
    После выполнения ты можешь остановить работающий контейнер с помощью комбинации CTRL + C или командой docker stop $(
    docker ps -q --filter ancestor=webapp-rockets).

```docker
docker stop $(docker ps -q --filter ancestor=webapp-rockets)
```

11. Какая базовая ОС использована в образе python:3.6?
    Если потребуется, ты всегда можешь запустить такой контейнер.

```docker
docker inspect webapp-rockets
```

os: linux 64

```docker
docker history webapp-rockets
```

не понимаю...

```docker
docker exec 705 cat /etc/os-release
```

```
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

12. Какой примерный размер образа webapp-rockets?

```docker
docker images
```

13. Это действительно большой размер для образа. Докер-образы предполагаются как маленькие и легковесные. Давай немного
    пообрежем его.

14. Создай новый образ этого приложения, который будет поменьше. Измени старый Dockerfile, назови образ webapp-rockets,
    дай ему тег lite.
    Поищи базовый образ поменьше для python:3.6. Убедись, что размер готового образа будет меньше чем 150MB.
    Пароль для sudo - selena

```
FROM python:3.6-alpine

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python3", "app.py"]
```

```docker
docker build . -f Dockerfile -t webapp-rockets:lite
```

15. Запусти новый контейнер из образа webapp-rockets:lite и прокинь порт 8080 контейнера на порт 30083 докер-хоста.

```docker
docker run -d -p 30083:8080 webapp-rockets:lite
```
