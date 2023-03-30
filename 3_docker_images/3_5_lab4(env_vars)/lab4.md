# Лабораторная №4 (EnvVars)

1. Исследуй переменные окружения в запущенном контейнере и определи значение переменной ROCKET_SIZE

```docker
docker ps
```

```docker
docker inspect 34ce4f2a7b25
```

2. Запусти контейнер с именем rocket-app из образа rotorocloud/simple-webapp-rockets и установи переменную ROCKET_SIZE в
   значение big. Сделай приложение доступным на порту 30888 докер-хоста. Приложение в контейнере работает на 8080 порту.

```docker
docker run -d -p 30888:8080 -e ROCKET_SIZE=big --name rocket-app rotorocloud/simple-webapp-rockets
```

3. Разверни экземпляр базы mysql с помощью образа mysql и назови контейнер mysql-db.

Для этого контейнера установи пароль db_pass123. Ты можешь посмотреть правильный образ mysql на Docker Hub и там же
узнать, как правильно проинициализировать root-пароль для ее контейнеризированной версии.

```docker
docker run --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 -d mysql:latest
```

4. Узнай, сколько баз данных создано в контейнере с mysql

```docker
docker ps
```

Connect to the MySQL server running inside the container:

```docker
docker exec -it fd42ad81b5d7 mysql -p
```

Enter the MySQL root password you specified when starting the container:

```
db_pass123
```

Run the following SQL command to list all databases:

```sql
SHOW DATABASES;
```

5. Попробуй cнова обратиться к базе и посмотри текущее значение переменной окружения MYSQL_ROOT_PASSWORD.
   ИНФО: Мы что-то изменили, детально исследуй контейнер

```sql
EXIT;
```

```docker
docker ps
```

```docker
docker inspect
```

6. Все верно, мы поменяли пароль в базе, но переменная осталась прежняя. Снова узнай, сколько баз данных создано в
   контейнере с mysql.
   ИНФО: Новый пароль db_newpass123.

```docker
docker exec -it fd42ad81b5d7 mysql -p
```

```
db_newpass123
```

```sql
SHOW DATABASES;
```
