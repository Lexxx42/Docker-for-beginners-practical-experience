# Тест: Docker Engine

Тема движка Docker одна из самых сложных, вот за ней и скрывается 'магия' контейнеризации.

В курсе для новичков я не ставил целью объяснить, как это работает в глубине, а лишь дать обзор темы. Как обычно вопросы
немного сложнее материала лекции.

Еще раз упомяну - эти тесты сложнее материала для новичков и требуются, только если ты хочешь сертификат об окончании.
Если тебя это задевает и ты считаешь, что курс стал от них хуже - просто пропусти эти тесты.

Вот полезные ссылки:

https://docs.docker.com/get-started/overview/

https://docs.docker.com/engine/

https://docs.docker.com/storage/

https://docs.docker.com/engine/reference/commandline/volume/#child-commands

1. Какие компоненты входят в Docker Engine?

> Docker Cli, Docker Daemon, REST API

2. Какой компонент Docker управляет образами, контейнерами, томами и сетями?

> Docker Daemon

3. Какой компонент по умолчанию отвечает за управление контейнерами в современных поставках Docker в Linux?

> LibContainer

4. Можем ли запускать контейнеры без установки Docker?

> Да (kubernetis для запуска контейнеров из docker образов "начинает использовать" cri-o вместо docker)

5. Какой компонент отвечает за поддержание контейнеров в живом состоянии, когда Docker Daemon отключается?

> Containerd-Shim

6. Какими объектами управляет Docker Engine?

> Networks, Volumes, Images, Containers

7. Данные внутри контейнера по умолчанию являются постоянными?

> Нет

8. Какая из этих сущностей используется только для чтения и является шаблоном для создания контейнеров?

> Docker images

9. Где по умолчанию Docker хранит свои данные?

> /var/lib/docker

10. Какая команда покажет версию Docker Engine?

> docker version

11. По умолчанию все файлы внутри контейнера находятся в записываемом слое контейнера?

> Да

12. Тома (Volumes) являются предпочтительным механизмом для организации постоянного хранения для докер-контейнеров?

> Да

13. Какой командой мы можем удалить неиспользуемые тома?

> docker volume prune

14. Какие опции используются для монтирования томов? (Выбери 3)

> --volume
> -v
> --mount

15. Какая из команд будет правильной для запуска контейнера webserver с томом secure-vol, который смонтирован в
    директорию назначения /opt внутри контейнера в режиме readonly? (Выбери 4)

> docker run -d --name webserver --mount source=secure-vol,target=/opt,ro nginx
> docker run -d --name webserver -v secure-vol:/opt:ro nginx
> docker run -d --name webserver --volume secure-vol:/opt:ro nginx
> docker run -d --name webserver --mount source=secure-vol,target=/opt,readonly nginx
