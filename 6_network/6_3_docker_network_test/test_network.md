# Тест: Docker Network

Концепция сети в плоскостях виртуализации/контейнеризации оставила от классических сетей общие принципы построения, но
внесла свое новое видение предмета. Я говорю о таких вещах, как виды сетей в VM и network namespaces.

Из-за этих вещей иногда классическому сетевому админу бывает сложно погрузиться в мир devops. На моем ресурсе
rotoro.cloud в курсе Certified Kubernetes Administrator мы обсуждаем эти нюансы, поэтому, если у тебя там есть подписка,
можешь проверить.

Ок, чтобы не усложнять я не лез в оверлейные сети, но в любом случае тебе что-то придется искать в документации.

Еще раз упомяну - эти тесты сложнее материала для новичков и требуются, только если ты хочешь сертификат об окончании.
Если тебя это задевает и ты считаешь, что курс стал от них хуже - просто пропусти эти тесты.

Вот полезные ссылки:

https://docs.docker.com/network/

https://docs.docker.com/network/bridge/

https://docs.docker.com/engine/reference/commandline/network/

https://docs.docker.com/engine/tutorials/networkingcontainers/

1. Как получить список доступных по умолчанию сетей в Docker?

> docker network ls

2. Какой командой можно посмотреть настройки сети и назначенный IP-адрес контейнера с id 7206cfc5e8ae и образом redis?

> docker inspect 7206cfc5e8ae

3. Какой сетевой драйвер будет использован по умолчанию, если ты не указал его явно?

> bridge

4. Какой тип сети следует выбрать, чтобы сетевой стек контейнера не был изолирован от хоста, а использовал его сетевое
   пространство, а также чтобы у контейнера не было бы своего собственного IP-адреса?

> host

5. Как узнать подсеть и шлюз сети 3afa2bbcfce8?

> docker network inspect 3afa2bbcfce8
> docker inspect 3afa2bbcfce8

6. Что из приведенных команд создаст пользовательскую мостовую сеть с названием stage-ns? (Выбери 3)

> docker network create --driver bridge stage-ns
> docker network create -d bridge stage-ns
> docker network create stage-ns

7. Какая команда подключит работающий контейнер с именем feature к существующей мостовой сети stage-ns?

> docker network connect stage-ns feature

8. Какая команда отключит работающий контейнер с именем feature от мостовой сети stage-ns?

> docker network disconnect stage-ns feature

9. Как можно удалить все неиспользуемые сети?

> docker network prune

10. Как удалить сеть stage-ns?

> docker network rm stage-ns
