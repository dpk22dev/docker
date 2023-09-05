kafka without zookeeper

### kafka connections:
https://www.baeldung.com/kafka-docker-connection

### connecting from outside container is not working if network is not correct
run below to find network name and use that specific name, similary in name of docker service has to be carefully written
docker network ls

### both of below work
docker run -it --rm \
    --network kafka-without-zookeeper_app-tier \
    docker.io/bitnami/kafka:3.5 kafka-topics.sh --list  --bootstrap-server kafka:9092

docker run -it --rm \
    --network kafka-without-zookeeper_app-tier \
    docker.io/bitnami/kafka:3.5 kafka-topics.sh --list  --bootstrap-server kafka-without-zookeeper-kafka-1:9092

### from local host below works
notice that port is exposed by us in docker-compose file
bin/kafka-topics.sh --describe --topic first_topic --bootstrap-server localhost:9094

### below don't
docker run -it --rm docker.io/bitnami/kafka:3.5 kafka-topics.sh --list  --bootstrap-server kafka:9092
docker run -it --rm docker.io/bitnami/kafka:3.5 kafka-topics.sh --list  --bootstrap-server localhost:9094



### if we go into running container's terminal below commands work:
kafka-topics.sh --list  --bootstrap-server localhost:9092

kafka-topics.sh --bootstrap-server localhost:9092 --topic first_topic --create --partitions 3 --replication-factor 1