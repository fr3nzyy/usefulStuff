# usefulStuff

Если ИДЕЯ не открывается, в терминале покажет ошибки:  /Applications/IntelliJ\ IDEA.app/Contents/MacOS/idea

killall -9 java

ps -ef | grep '[t]omcat'
echo -n 'xxxxxx' | base64

Кодировка в консоле: chcp 1251

Docker

docker login -u $login -p $password registry.someadrr.ru
docker build --tag registry.someadrr.ru/dev/ci01978215/ci01978215_hr-platform_dev/baseimages/openresty:1.15 -f HRP-pipeline/spine-ingress/BaseImage.Dockerfile .
docker push registry.someadrr.ru/dev/ci01978215/ci01978215_hr-platform_dev/baseimages/openresty:1.15


docker login -u user -p pass registry.someadrr.ru
docker tag todolist registry.someadrr.ru/dev/ci02128305/ci02180808_sbin_dev/todolist:latest
docker push registry.someadrr.ru/dev/ci02128305/ci02180808_sbin_dev/todolist

Создать контейнер
docker run --name postgres -e POSTGRES_PASSWORD=postgres -e POSTGRE_USER=postgres -e POSTGRES_DB=postgres -p 5432:5432 -d postgres


Postgres
Зайти в контейнер
docker exec -it -upostgres postgres /bin/bash

psql -la
psql
CREATE DATABASE configurator;

---
su postgres

psql -c "CREATE DATABASE app_recruit_middleware;"
psql -c "CREATE USER postgres WITH ENCRYPTED PASSWORD 'qwerty';"
psql -c "GRANT ALL PRIVILEGES ON DATABASE app_recruit_middleware TO youruser;"



Mongo

docker pull mongo
docker run -d --name mongo \
-e MONGO_INITDB_ROOT_USERNAME=mongo \
-e MONGO_INITDB_ROOT_PASSWORD=mongo \
-e MONGO_INITDB_DATABASE=comments \
-p 27017:27017 \
mongo

mongo admin -u mongo -p 'mongo' -host localhost -port 27017

docker exec -it mongo mongo



Редактирование переменных окружения

vim ~/.bash_profile
    . .bash_profile

