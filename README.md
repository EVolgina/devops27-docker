# Задача 1 Сценарий выполнения задачи:
создайте свой репозиторий на https://hub.docker.com;
выберите любой образ, который содержит веб-сервер Nginx;
создайте свой fork образа;
реализуйте функциональность: запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:
'''<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>'''
Опубликуйте созданный fork в своём репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.
Ответ:
'''
devops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo nano dockerfile
devodevops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo docker build -f dockerfile -t evolgina/devops27:tagname .
devodevops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo docker push evolgina/devops27:tagname
docker login --username evolgina
devops@WORKBOOK:/mnt/c/Users/Admin/docker$ sudo docker run -d -p 8080:80 evolgina/devops27:tagname
'''
![hello]()
### ссылка https://hub.docker.com/repository/docker/evolgina/devops27/tags?page=1&ordering=last_updated

# Задача 2
Посмотрите на сценарий ниже и ответьте на вопрос: «Подходит ли в этом сценарии использование Docker-контейнеров или лучше подойдёт виртуальная машина, физическая машина? Может быть, возможны разные варианты?»

Детально опишите и обоснуйте свой выбор.

--

Сценарий:

высоконагруженное монолитное Java веб-приложение;
Nodejs веб-приложение;
мобильное приложение c версиями для Android и iOS;
шина данных на базе Apache Kafka;
Elasticsearch-кластер для реализации логирования продуктивного веб-приложения — три ноды elasticsearch, два logstash и две ноды kibana;
мониторинг-стек на базе Prometheus и Grafana;
MongoDB как основное хранилище данных для Java-приложения;
Gitlab-сервер для реализации CI/CD-процессов и приватный (закрытый) Docker Registry.
Задача 3
Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера.
Запустите второй контейнер из образа debian в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера.
Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.
Добавьте ещё один файл в папку /data на хостовой машине.
Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.
Задача 4 (*)
Воспроизведите практическую часть лекции самостоятельно.

Соберите Docker-образ с Ansible, загрузите на Docker Hub и пришлите ссылку вместе с остальными ответами к задачам.
