
# Rocket MQ

参考 [Apache/Rocket MQ Docker](https://github.com/apache/rocketmq-docker)

## building rocket mq image
```shell
docker build --no-cache -f Dockerfile-rocketmq -t hyanwang/rocketmq:5.1.0 --build-arg version=5.1.0 .```

```
# Rocket MQ Dashboard

## buiding rocket mq dashboard image
```shell
docker build --no-cache -f Dockerfile-dashboard -t hyanwang/rocketmq-dashboard:1.0.0 --build-arg version=1.0.0 .
```
