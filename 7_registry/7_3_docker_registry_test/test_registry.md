# Тест: Docker Registry

Подход к Registry у Docker Community Edition и Mirantis Kubernetes Engine (известный ранее как Docker Enterprise) сильно
отличаются.

В Docker CE ты можешь самостоятельно поднять службы реестра, настроить там аутентификацию, сканирование на уязвимости,
подпись образов и т.д. В Enterprise версии все это идет из коробки.

Здесь у нас будет вопрос по Docker Trusted Registry - т.е. продукта, который есть только в Docker Enterprise.

Еще раз упомяну - эти тесты сложнее материала для новичков и требуются, только если ты хочешь сертификат об окончании.
Если тебя это задевает и ты считаешь, что курс стал от них хуже - просто пропусти эти тесты.

Эти ссылки помогут в прохождении теста:

https://docs.docker.com/engine/reference/commandline/docker/

https://docs.docker.com/registry/introduction/

1. Ты логинишься при помощи команды docker login , данные для аутентификации сохраняются локально. Где находятся эти
   креденшилс?

> `$HOME/.docker/config.json`
> [docker login](https://docs.docker.com/engine/reference/commandline/login/)

2. Что из этого верный адрес для докер-образа, имя которого webapp-rockets, а организация, владеющая этим образом
   rocketcorp, держит его в приватном реджистри по адресу registry.group-x.money?

> `registry.group-x.money/rocketcorp/webapp-rockets`

3. Какая команда используется для поиска образов с именем, содержащим в себе nginx, и по крайней мере с 15 звездами? Мы
   хотим ограничить вывод тремя строками.

> `docker search --filter=stars=15 --limit 3 nginx`

4. Какая команда поможет в поиске официального образа httpd?

> `docker search --filter is-official=true httpd`
> [docker search](https://docs.docker.com/engine/reference/commandline/search/)

5. Что из этого пользователь (аккаунт) и образ (репозиторий) в образе grafana/alpine?

> user=grafana, image=alpine

6. Выбери особенности docker trusted registry (DTR).

> Встроенный контроль доступа
> Сканирование образов
> Управление образами и заданиями
> Подпись образов
> [Docker Trusted Registry overview](https://docs.docker.com.xy2401.com/ee/dtr/)

7. Какой командой можно получить список локальных образов, имеющих метку org.opencontainers.image.title?

> docker images --filter "label=org.opencontainers.image.title"
> [docker images](https://docs.docker.com/engine/reference/commandline/images/)

8. Какой командой можно изменить тег webserver:latest на webserver:httpd? (Выбери 2)

> docker image tag webserver:latest webserver:httpd
> docker tag webserver:latest webserver:httpd
> [docker image tag](https://docs.docker.com/engine/reference/commandline/image_tag/)
> [docker tag](https://docs.docker.com/engine/reference/commandline/tag/)

9. Какой командой можно загрузить образ в приватный реджистри?

> docker push <private-registry-address>/<username>/<repo-name>

10. Ты запускаешь команду docker pull rotorocloud/cosign, но получаешь ошибку. В чем дело?

> У образа rotorocloud/cosign в реестре нет тега latest
