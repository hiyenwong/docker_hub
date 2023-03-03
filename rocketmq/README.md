
# Rocket MQ

## building rocket mq image
```shell
docker build --no-cache -f Dockerfile-centos -t 10.110.91.244:8000/apache/rocketmq:5.1.0 --build-arg version=5.1.0 .```

```
# Rocket MQ Dashboard

## buiding rocket mq dashboard image
```shell
docker build --no-cache -f Dockerfile-dashboard -t hyanwang/rocketmq-dashboard:1.0.0 --build-arg version=1.0.0 .
```
```
