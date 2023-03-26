# Как получить доступ извне хоста?

```shell
ip addr
```

`enp0s3` - внешний адрес докер хоста.

## Проблема

Не могу один вопрос решить. "Offline. This Jenkins instance appears to be offline."

1. Использую команду из https://github.com/jenkinsci/docker/blob/master/README.md
   docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:
   lts-jdk11
2. Чекаю id контейнера
   docker ps
3. Распечатываю пароль
   docker exec cfa cat /var/jenkins_home/secrets/initialAdminPassword
4. Ввожу пароль в форму
5. Jenkins оффлайн
6. Чекаю
   stackoverflow: https://stackoverflow.com/questions/42408703/why-does-jenkins-say-this-jenkins-instance-appears-to-be-offline
7. Пишут, что надо отредактировать UpdateCenter.xml
   Вопрос: как это сделать у экземпляра (или контейнера, не знаю как правильно)?
   Может другое решение есть? У меня пока не получается...
   Хост Windows 11 Pro Version 21H2
   Виртуальная машина с докером: Ubuntu 22.04.2 LTS 64 bit
   Проброшен порт: хост 8022, гость 22. Подключаюсь через SSH
   Доступ к интернету на машине есть.
