### cx is accessible on port 9042 outside using below creds
u: cassandra
p: cassandra

### to access from within container
docker run -it --rm \
    --network cassandra-single_app-tier \
    bitnami/cassandra:latest cqlsh --username cassandra --password cassandra cassandra-server


https://hub.docker.com/r/bitnami/cassandra
