## usefulStuff

Если ИДЕЯ не открывается, в терминале покажет ошибки:  /Applications/IntelliJ\ IDEA.app/Contents/MacOS/idea

killall -9 java

ps -ef | grep '[t]omcat'
echo -n 'xxxxxx' | base64

Кодировка в консоле: chcp 1251

##Docker

docker login -u $login -p $password registry.someadrr.ru
docker build --tag registry.someadrr.ru/dev/ci01978215/ci01978215_hr-platform_dev/baseimages/openresty:1.15 -f HRP-pipeline/spine-ingress/BaseImage.Dockerfile .
docker push registry.someadrr.ru/dev/ci01978215/ci01978215_hr-platform_dev/baseimages/openresty:1.15

docker login -u user -p pass registry.someadrr.ru
docker tag todolist registry.someadrr.ru/dev/ci02128305/ci02180808_sbin_dev/todolist:latest
docker push registry.someadrr.ru/dev/ci02128305/ci02180808_sbin_dev/todolist

Создать контейнер
docker run --name postgres -e POSTGRES_PASSWORD=postgres -e POSTGRE_USER=postgres -e POSTGRES_DB=postgres -p 5432:5432 -d postgres

docker update --restart=no $(docker ps -a -q)

docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker kill --signal=SIGINT $(docker ps -a -q)

docker compose up -d
docker-compose -f docker-compose-kafka.yml down
docker kill $(docker ps -q)

docker build -t jaeger-client .
docker tag 0a19027f8ef2 zhkvaleksey/jaeger-client:latest 
docker image ls 
docker push zhkvaleksey/jaeger-client 

##Postgres
Зайти в контейнер
docker exec -it -upostgres postgres /bin/bash
docker exec -it my_postgres psql -U postgres postgres

psql -la
psql
CREATE DATABASE configurator;

---
su postgres

psql -c "CREATE DATABASE app_recruit_middleware;"
psql -c "CREATE USER postgres WITH ENCRYPTED PASSWORD 'qwerty';"
psql -c "GRANT ALL PRIVILEGES ON DATABASE app_recruit_middleware TO youruser;"

\c user_data; #select db
CREATE SCHEMA quickfixj;


##Mongo

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

--------
##OpenShift

Переходим в папку, где лежит Dockerfile
    docker build --tag thrift-service .
    docker -u $login -p $password registry.some.ru
    docker tag thrift-service registry.some.ru/dev/thrift-service
    docker push registry.some.ru/dev/thrift-service

Залогиниться в openshift можно из веб приложения, в правом верхнем углу нажимаем на '?' -> Command Line Tools -> Copy Login Command -> Display token -> Log in with this token
после успешного логина выбираем проект по умолчанию - ci02128305-edevgen-si20
далее можно создавать приложение в шифте:
    oc new-app --docker-image registry.some.ru/dev/thrift-service

заходим в веб приложение шифта, в разделе Workloads переходим на страницу Deployments, удаляем созданный шифтом Deployment нашего сервиса
переходим на страницу Deployment Configs, можно сразу зайти в одно из наших приложений и скопировать конфиг, в редакторе заменить имя сервиса на имя нового сервиса, на странице Deployment Configs нажать Create Deployment Configs, вставляем отредактированный конфиг и сохраняем.
  Заходим в раздел Networking -> Routes, нажимаем Create Route:
    Name - имя вашего сервиса
    Serivce - выбираем шифтовый сервис вашего сервиса
    Target Port - 8080 -> 8080
    Нажимаем Create

  Заходим в раздел Networking -> Services, находим шифтовый сервис для вашего сервиса и заходим в него, далее вкладка YAML:
    ищем внизу конфига строку
  selector:
    deployment: ci02128305ci02180808sbindevthrift-service
  Заменяем строку deployment: ci02128305ci02180808sbindevthrift-service на name: thrift-service
  Должно получится вот так:
    selector:
      name: thrift-service
      
##Kafka

1. Install Docker Desktop on Windows https://hub.docker.com/editions/community/docker-ce-desktop-windows/
2. Download Kafka form https://www.apache.org/dyn/closer.cgi?path=/kafka/2.7.0/kafka_2.12-2.7.0.tgz
3. Start Docker Engine
4. Make a directory as “ D:\docker”
5. Create a docker-compose.yml file in the above directory

```
version: "3"
services:
  zookeeper:
    image: 'bitnami/zookeeper:latest'
    ports:
      - '2181:2181'
    environment:
      - ALLOW_ANONYMOUS_LOGIN=yes
  kafka:
    image: 'bitnami/kafka:latest'
    ports:
      - '9092:9092'
    environment:
      - KAFKA_BROKER_ID=1
      - KAFKA_LISTENERS=PLAINTEXT://:9092
      - KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092
      - KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181
      - ALLOW_PLAINTEXT_LISTENER=yes
    depends_on:
      - zookeeper
```
```
chmod +x ./....

./kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic helloKafka
./kafka-console-producer.sh --broker-list localhost:9092 --topic helloKafka
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic helloKafka    
./kafka-topics.sh --bootstrap-server localhost:9092 --list


```

##Helm

```
Собрать чарт   
helm dep up 
helm template . 

helm upgrade jaeger-client ./helm/jaeger-client -n review-review-adzhukov-new

helm repo add @dbp 
helm repo add dbp hhttps://nexus.inno.tech/repository/test-helm --username adzhukov --password 1!Qqweewq

helm upgrade dbp-tracing-1643872854 ./dbp-tracing -n dbp-tracing 
helm upgrade jaeger-client-1644235080 . -n review-adzhukov

helm install --generate-name ./dbp-tracing -n review-adzhukov
helm install --name jaeger-client ./jaeger-client
```

##Mix
```
git submodule init 
git submodule update  

cassandra проверка БД
kubectl exec -n review-adzhukov -i -t dev-607-adzhukov-cassandra-0 -- /opt/cassandra/bin/cqlsh 
select * from jaeger_v1_test.traces;
truncate jaeger_v1_test.traces;

kafka проверка логов
kubectl exec -n review-adzhukov -it uzcards-kafka-0 -- /bin/bash
/bitnami/kafka/data/jaeger_v1_test-0$
cat .log 

```
