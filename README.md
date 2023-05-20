# Задача 1 Сценарий выполнения задачи:
создайте свой репозиторий на https://hub.docker.com; \
выберите любой образ, который содержит веб-сервер Nginx; \
создайте свой fork образа; \
реализуйте функциональность: запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже: \

<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>

Опубликуйте созданный fork в своём репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.
##### Ответ:
1.Скачиваем образ nginx
2.Создаем dockerfile (сценарий)
3.Делаем fork образа
4.Пушим образ в репозиторий на hub.docker.com
5.Запускаем контейнер с пробросом на 8080 порт хоста

``` devops@WORKBOOK:/mnt/c/Users/Admin/docker$ docker pull nginx
devops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo nano dockerfile
devodevops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo docker build -f dockerfile -t evolgina/devops27:tagname .
devodevops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo docker push evolgina/devops27:tagname
docker login --username evolgina
devops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo docker run -d -p 8080:80 evolgina/devops27:tagname 
```
![hello](https://github.com/EVolgina/devops27-docker/blob/main/hello.PNG)

### ссылка https://hub.docker.com/repository/docker/evolgina/devops27/tags?page=1&ordering=last_updated

# Задача 2
Посмотрите на сценарий ниже и ответьте на вопрос: «Подходит ли в этом сценарии использование Docker-контейнеров или лучше подойдёт виртуальная машина, физическая машина? Может быть, возможны разные варианты?» \
Детально опишите и обоснуйте свой выбор.\
Сценарий: \
- высоконагруженное монолитное Java веб-приложение; \
- Nodejs веб-приложение; \
- мобильное приложение c версиями для Android и iOS; \
- шина данных на базе Apache Kafka; \
- Elasticsearch-кластер для реализации логирования продуктивного веб-приложения — три ноды elasticsearch, два logstash и \
две ноды kibana;\
- мониторинг-стек на базе Prometheus и Grafana; \
- MongoDB как основное хранилище данных для Java-приложения; \
- Gitlab-сервер для реализации CI/CD-процессов и приватный (закрытый) Docker Registry.\
##### Ответ:
- Физический сервер или VM предпочтительнее, т.к. монолитное и на микросервисы сложно разбить. К тому же высоконагруженное - 
необходим прямой доступ к ресурсам.
- Nodejs веб-приложение;
Подойдет Docker, так как это веб-платформа с подключаемыми внешними библиотеками
- Мобильное приложение c версиями для Android и iOS;
Необходим GUI, так что подойдет виртуалка.
- Шина данных на базе Apache Kafka;
Если среда рабочая и полнота данных критична, то лучше использовать VM; если среда тестовая и потеря данных некритична,
можно использовать Docker.
- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и
две ноды kibana;
Elasticsearvh лучше на VM, отказоустойчивость решается на уровне кластера, kibana и logstash можно вынести в Docker
- Мониторинг-стек на базе Prometheus и Grafana;
Подойдет Docker, так как данные не хранятся, и масштабировать легко.
- MongoDB, как основное хранилище данных для java-приложения;
Зависит от нагрузки на DB. Если нагрузка большая, то физический сервер, если нет – VM.
- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.
Подойдет VM для DB и фалового хранилища, Docker для сервисов

# Задача 3
Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера.\
Запустите второй контейнер из образа debian в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера.\
Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.\
Добавьте ещё один файл в папку /data на хостовой машине.\
Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.\
##### Ответ:
- Запускаем первый контейнер из образа centos c любым тэгом в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера:\
$ docker run -v /data:/data --name centos-container -d -t centos

- Запускаем второй контейнер из образа debian в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера:
$ docker run -v /data:/data --name debian-container -d -t debian \

- Смотрим запущенные контейнеры:
``` devops@WORKBOOK:/mnt/c/Users/Admin/debian$ sudo docker ps
CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS          PORTS                                   NAMES
34770526b03f   debian                      "bash"                   4 minutes ago    Up 4 minutes                                            debian-container
a294034b675b   centos                      "/bin/bash"              43 minutes ago   Up 43 minutes                                           centos-container
f9210a207c95   evolgina/devops27:tagname   "/docker-entrypoint.…"   2 hours ago      Up 2 hours      0.0.0.0:8080->80/tcp, :::8080->80/tcp   magical_agnesi
```
- Подключаемся к первому контейнеру с помощью docker exec и создаем текстовый файл в /data:\
$ docker exec centos-container /bin/bash -c "echo test_message>/data/readme.md"\
Добавляем еще один файл в папку /data на хостовой машине:\
devops@WORKBOOK:/mnt/c/Users/Admin$ sudo touch /data/test.txt \
devops@WORKBOOK:/mnt/c/Users/Admin$ sudo nano /data/test.txt \
- Подключаемся во второй контейнер и отображаем листинг и содержание файлов в /data контейнера.\

``` devops@WORKBOOK:/mnt/c/Users/Admin$ sudo docker exec -it debian-container /bin/bash
root@34770526b03f:/# cd /data
root@34770526b03f:/data# ls -l
total 8
-rw-r--r-- 1 root root 13 May 20 13:21 readme.md
-rw-r--r-- 1 root root  8 May 20 13:24 test.txt
root@34770526b03f:/data#
```

