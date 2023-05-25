### 常用命令

```
docker ps   查看正在运行的容器
```









#### mysql

```docker pull mysql:5.7
docker pull mysql

// 启动, 目录挂载
docker run -p 3306:3306 --name mysql \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=a111111 \
-d mysql:latest

//链接
https://blog.csdn.net/qq_31762741/article/details/121465465?ops_request_misc=&request_id=&biz_id=102&utm_term=docker%E5%AE%89%E8%A3%85mysql%E5%B9%B6%E9%85%8D%E7%BD%AE&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-121465465.142^v80^insert_down38,201^v4^add_ask,239^v2^insert_chatgpt&spm=1018.2226.3001.4187


//------
docker start mysql
docker exec -it mysql /bin/bash
exit

//重启
docker restart mysql
```



```

```







#### redis

```
docker pull redis

mkdir -p /mydata/redis/conf
touch /mydata/redis/conf/redis.conf  // 将官网下载的配置文件复制到这里


docker run -p 6379:6379 --name redis \
-v /mydata/redis/data:/data \
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf

docker exec -it redis redis-server -v

// 登陆客户端
docker exec -it redis redis-cli
auth a111111
```





####  consul

```
docker run -d -p 8500:8500 -p 8300:8300 -p 8301:8301 -p 8302:8302 -p 8600:8600/udp consul consul agent -dev -client=0.0.0.0

浏览器访问 http://127.0.0.1:8500/ui/dc1/services 测试是否安装成功


```







#### Es

```
docker run --name elasticsearch -p 9200:9200 -p 9300:9300 \
-e  "discovery.type=single-node" \
-e ES_JAVA_OPTS="-Xms64m -Xmx128m" \
-v /mydata/elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml \
-v /mydata/elasticsearch/data:/usr/share/elasticsearch/data \
-v  /mydata/elasticsearch/plugins:/usr/share/elasticsearch/plugins \
-d elasticsearch:7.17.8
```



#### Kibana

```

docker run --name kibana -e ELASTICSEARCH_HOSTS=http://127.0.0.1:9200 -p 5601:5601 -d kibana:7.17.8

docker run --name kibana --link=elasticsearch:elasticsearch -p 5601:5601 -d kibana:7.17.8
```







#### zoo_kafka

```
docker network create app-tier --driver bridge

docker run -d --name zookeeper \
	-p 2181:2181 \
    --network app-tier \
    -e ALLOW_ANONYMOUS_LOGIN=yes \
  	zookeeper:latest
  	
  	
  	2)docker run -d --log-driver json-file --log-opt max-size=100m --log-opt max-file=2  --name zookeeper -p 2181:2181 -v /etc/localtime:/etc/localtime wurstmeister/zookeeper


docker run -d --name kafka \
    --network app-tier \
    -p 9092:9092 \
    -e ALLOW_PLAINTEXT_LISTENER=yes \
    -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092 \
    -e KAFKA_LISTENERS=PLAINTEXT://127.0.0.1:9092 \
	wurstmeister/kafka:latest

```













zookeeper

```
docker run  -d --name kafka  -p 9092:9092  --link zookeeper  -e KAFKA_BROKER_ID=0  -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092  -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka 

```



// 然想在容器中使用非安全的监听器，可以按照以下步骤解决这个问题：

1. 在 Dockerfile 或 docker run 命令中，添加环境变量 ALLOW_PLAINTEXT_LISTENER=yes，如下所示：

````
docker run --name kafka -p 9092:9092 \
    -v /mydata/zoo_kafka/kafka/conf/server.properties:/opt/kafka/config/server.properties \
    -v /mydata/zoo_kafka/kafka/conf/log4j.properties:/opt/kafka/config/log4j.properties \
    -v /mydata/zoo_kafka/kafka/data/:/opt/kafka/data \
    -v /mydata/zoo_kafka/kafka/logs/:/opt/kafka/logs \
    -e ALLOW_PLAINTEXT_LISTENER=yes \
    -e KAFKA_ZOOKEEPER_CONNECT=127.0.0.1:2181 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092 \
    -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 \
    -d wurstmeister/kafka:latest
    
    
    
    docker run --name kafka -p 9092:9092 \
    -v /mydata/zoo_kafka/kafka/conf/:/opt/kafka/config \
    -e KAFKA_ZOOKEEPER_CONNECT=127.0.0.1:2181 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092 \
    -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 \
    -d wurstmeister/kafka:latest
````





```
docker run -d --name kafka -p 9092:9092 -v ~/kafka-docker/single-node/server.properties:/opt/kafka/config/server.properties --link zookeeper:zookeeper wurstmeister/kafka
```





docker run -d  --log-driver json-file --log-opt max-size=100m --log-opt max-file=2 --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=1 -e KAFKA_ZOOKEEPER_CONNECT=127.0.0.1:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -v /etc/localtime:/etc/localtime wurstmeister/kafka





2)docker run -d --restart=always --log-driver json-file --log-opt max-size=100m --log-opt max-file=2 --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=192.168.244.132/kafka -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.244.132:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -v /etc/localtime:/etc/localtime wurstmeister/kafka





#### zookeeper kafka

```


docker run -d --name zookeeper -p 2181:2181 zookeeper


docker run  -d --name kafka  -p 9092:9092  --link zookeeper  -e KAFKA_BROKER_ID=0  -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092  -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka

```



#### 常用命令

* 自动启动

  ```
  docker update redis --restart=always   
  ```

  
