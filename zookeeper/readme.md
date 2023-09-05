zk running on below port:
2181

### below doesn't work
docker run -it --rm \
    --network zookeeper_app-tier \
    bitnami/zookeeper:latest zkCli.sh -server zookeeper:2181  get /

### use zoo navigator, but not working
docker run \
  -d --network host \
  -e HTTP_PORT=9000 \
  --name zoonavigator \
  --restart unless-stopped \
  elkozmon/zoonavigator:latest    