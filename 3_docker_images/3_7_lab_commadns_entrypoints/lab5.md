# Лабораторная №5 (Commadns and Entrypoints)

Мы представили несколько Dockerfiles нескольких популярных продуктов в каталоге /home/moon/.
Изучи их и ответь на несколько вопросов.

1. Какая ENTRYPOINT установлена для создания образа nosql базы данных?

```shell
ll
```

```shell
cat Dockerfile-mongodb
```

2. Какая ENTRYPOINT установлена для создания образа реляционной базы данных, коммюнити версии mysql?

```shell
cat Dockerfile-mariadb
```

3. Какая CMD установлена для создания образа системы управления контентом wordpress?

```shell
cat Dockerfile-wordpress
```

4. Какой будет окончательная команда при запуске контейнера из образа wordpress из данного Dockerfile? Прими во внимание
   и инструкцию ENTRYPOINT, и инструкцию CMD

> In a Dockerfile, CMD and ENTRYPOINT are instructions used to define the default command to be executed when the
> container starts.

> CMD instruction is used to set the default command and/or parameters that will be executed when a new container is
> started from the image. It can be overridden by specifying a command when starting the container.

> For example, CMD ["python", "app.py"] sets the default command to run the app.py file with the python interpreter.

> ENTRYPOINT instruction is used to set the default executable command for a container. It is the command that will be
> executed when the container starts, and any arguments passed to the docker run command will be appended to the
> ENTRYPOINT command.

> For example, ENTRYPOINT ["python", "app.py"] sets the default executable to python app.py. When the container starts
> with the command docker run myapp arg1 arg2, it will execute the command python app.py arg1 arg2.

> If both CMD and ENTRYPOINT instructions are specified in a Dockerfile, CMD is used to provide default arguments for
> the
> command specified by ENTRYPOINT.

> For example, if the Dockerfile has both ENTRYPOINT ["python"] and CMD ["app.py"], then the default command when
> starting
> the container will be python app.py. However, if the container is started with a command, such as docker run myapp
> script.py, then the default command will be overridden and the container will execute python script.py.

```
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
```

```
docker-entrypoint.sh apache2-foreground
```

5. Какая команда выполняется при запуске контейнера, созданного из Dockerfile с названием ubuntu?

```shell
cat Dockerfile-ubuntu
```

6. Запусти контейнер из образа ubuntu и переопредели команду (CMD) для старта в контейнере, заменив ее на sleep 1000
   Запусти это в detached mode.

```docker
docker run -d ubuntu sleep 1000
```
