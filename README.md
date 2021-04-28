kafka
=======

本地搭建 `kafka` 环境


### 构建环境

下载本仓库后
```bash
# 启动
$ docker-compose up -d

# 停止
$ docker-compose stop
```
> kafka 启动之后，只能本机访问，同一局域网其他机器没法访问


### 使用

进入容器
```bash
$ docker exec -it kafka /bin/bash

$ cd /opt/kafka/bin
```

生产消息
```bash
$ ./kafka-console-producer.sh --broker-list localhost:9092 --topic my-topic
```

消费消息
```bash
$ ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my-topic --from-beginning
```


### 其他

客户端访问 `kafka` 的时候
1. 客户端连接到 `KAFKA_LISTENERS` 标识的地址，完后认证后，获取一个 `brokers` 的返回地址
2. 通过返回的 `brokers` 地址重新建立与 `kafka` 的连接，这个返回的地址就是 `KAFKA_ADVERTISED_LISTENERS` 的值

因此，若要局域网其他机器也能访问到容器内的 `kafka`，则需要声明 `KAFKA_ADVERTISED_LISTENERS` 的地址.

字段说明：
- KAFKA_LISTENERS 定义 `kafka` 的服务监听地址
- KAFKA_ADVERTISED_LISTENERS `kafka` 发布到 `zookeeper` 供客户端使用的服务地址


### 参考
[Docker kafka](https://www.yuque.com/tiankonghewo/note/iuh1ek)  
[kafka配置KAFKA_LISTENERS和KAFKA_ADVERTISED_LISTENERS](https://www.jianshu.com/p/26495e334613)  
