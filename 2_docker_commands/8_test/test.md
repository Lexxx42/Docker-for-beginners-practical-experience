# Тест

## Как удалить все запущенные и остановленные контейнеры на хосте?

> + docker container rm -f $(docker container ls -aq)
> + docker container rm -f $(docker container ps -aq)
> + docker rm -f $(docker ps -aq)
    > Note that the difference between docker rm and docker container rm is simply that the latter explicitly refers to
    container objects (introduced in Docker 1.13) while the former uses the legacy syntax.
    > the "ls" command is an alias for "ps"

## Какая из команд создаст (не запустит) контейнер с образом redis и именем redis?

> + docker container create --name redis redis
    > When you run this command, Docker will create a new container based on the redis image and name it redis. However,
    the container will not be started yet. You can start the container later using the docker container start redis
    command.
    > docker container create [OPTIONS] IMAGE [COMMAND] [ARG...]
    то есть нельзя после названия образа писать опции к команде create, например имя контейнера --name

## Мы развернули несколько контейнеров. Как увидеть, какой из них потребляет больше всего памяти?

> + docker container stats
    > The docker container stats command is used to display real-time usage statistics for running containers. It
    provides a live stream of resource usage metrics such as CPU usage, memory consumption, network I/O, and disk I/O
    for one or more running containers.

## Как запустить контейнер с названием webserver  с образом nginx в интерактивном режиме? (Выбери 2)

> + docker run -it --name webserver nginx
> + docker container run -it --name webserver nginx

## Какая команда используется для обновления restart policy контейнера redis в значение always?

> + docker container update --restart always redis
    > The docker container update command is used to update the configuration of an existing container. The --restart
    option is used to set the restart policy for the container. The always option for the --restart option means that
    Docker will always attempt to restart the container if it stops for any reason, including if the Docker daemon is
    restarted.

## Как скопировать директорию nginx из контейнера webapp на хост по пути /tmp/?

> + docker container cp webapp:/etc/nginx /tmp/
    > The command docker container cp webapp:/etc/nginx /tmp/ is used to copy the nginx directory from the container
    webapp to the /tmp/ directory on the host. Here's what each part of the command means:

> docker container cp is the command to copy files and directories between a container and the host.


> webapp is the name or ID of the container from which the files will be copied.
> :/etc/nginx is the path of the directory to be copied inside the container. In this case, it is the nginx directory

> located in the /etc directory.

> /tmp/ is the path of the directory on the host where the directory will be copied to.

> When this command is executed, Docker will create the /tmp/nginx directory on the host machine (if it doesn't
> exist
> already), and copy the entire nginx directory from the webapp container to it. This can be useful if you need to
> access
> files or configurations from a container on the host machine for debugging or testing purposes.

## Можно ли сопоставить несколько контейнеров с одним и тем же портом к одному порту на докер-хосте?

> нет

## Какой командой мы можем проверить драйвер логирования по умолчанию?

> [ChatGPT]: docker info --format '{{.LoggingDriver}}'
>
> correct answer: docker system info
>
> The docker system info command displays system-wide information about the Docker installation on the host. It includes
> information about the Docker version, operating system, number of containers and images, storage driver, logging
> driver,
> and other useful details about the Docker environment.

## Как запустить контейнер redis и быть уверенным, что для него не будет настроено логов?

> [ChatGPT]: docker run -d --name redis --log-driver=none redis
>
> correct answer: `docker run -it -d --log-driver none redis`
>
> By setting the logging driver to "none", you're telling Docker not to collect or store any logs for the Redis
> container. This can be useful if you don't need or want to log Redis's output, or if you want to reduce the amount of
> data that Docker has to store. However, it's important to note that disabling logging altogether can make it harder to
> debug problems with your container later on.

## Как проверить статус службы docker на хосте?

> sudo systemctl status docker

## При помощи какого механизма Docker сопоставляет порты контейнера и хоста?

> При помощи правил IPTables
>
> Docker uses IPTables to perform port mapping between the container and the host. When a Docker container starts, it
> creates a network namespace with its own network stack that includes its own IP address and set of network interfaces.
> To allow communication between the container and the host, Docker sets up IPTables rules that map the container's
> ports
> to the host's ports. Specifically, Docker creates DNAT rules (Destination Network Address Translation) that redirect
> incoming traffic to the container's IP address and port to the corresponding port on the host. These rules are created
> in the nat table of the host's IPTables. When the response is sent back, the IPTables rules are used again to
> translate
> the source address of the response to the container's IP address and port. This way, the container appears to be
> directly connected to the network with its own IP address and ports, even though it is running in a separate network
> namespace.

## Какой флаг настроит Docker на проброс порта 80 UDP в контейнере на порт 8080 докер-хоста?

> -p 8080:80/udp
>
> In the example -p 8080:80/udp, the host port 8080 is mapped to the container port 80 using the UDP protocol. This
> means that any traffic sent to the Docker host on port 8080 using UDP protocol will be forwarded to the container on
> port 80 using the same protocol.
>
> This is useful for applications that require a specific port and protocol to be used for communication, such as some
> video streaming applications that use UDP instead of TCP for lower latency.

## Если не указано иное, Docker публикует открытый порт на всех сетевых интерфейсах?

> Yes, by default Docker publishes an open port on all network interfaces (0.0.0.0). This means that the container's
> port can be accessed from any IP address on the host machine's network.
>
> However, you can also specify a specific network interface to bind to by specifying the interface's IP address when
> publishing the port. For example, -p 127.0.0.1:8080:80 would only bind the container's port 80 to the localhost
> interface (127.0.0.1) on the host machine.

## Какой командой мы можем получить сводку важной информации о контейнере webapp (например сетевые адреса, переменные окружения, политику рестарта и т.д.)?

> docker container inspect webapp

## Чем из приведенного мы можем получить поток логов контейнера my-app?

> + docker container logs -f my-app
