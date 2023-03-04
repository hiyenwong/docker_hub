
# Rocket MQ

参考 [Apache/Rocket MQ Docker](https://github.com/apache/rocketmq-docker)

## building rocket mq image

```shell
docker build --no-cache -f Dockerfile-rocketmq -t hyanwang/rocketmq:5.1.0 --build-arg version=5.1.0 .```
```

## running

```shell
./player-docker-compose.sh
```

# Rocket MQ Dashboard

## building rocket mq dashboard image

```shell
docker build --no-cache -f Dockerfile-dashboard -t hyanwang/rocketmq-dashboard:1.0.0 --build-arg version=1.0.0 .
```

## Running 

单独运行,如果你使用Docker Composer 不需要再次运行

```shell
./play-dashboard.sh
```


## Use

打开浏览器访问 http://localhost:6765/#/ops 在`NameServerAddressList` 填写 `namesrv:9876`
