
    docker pull zookeeper
启动 ZK 镜像

    docker run --name my_zookeeper -d zookeeper:latest
这个命令会在后台运行一个 zookeeper 容器, 名字是 my_zookeeper, 并且它默认会导出 2181 端口.
接着我们使用:
    
    docker logs -f my_zookeeper
使用 ZK 命令行客户端连接 ZK
因为刚才我们启动的那个 ZK 容器并没有绑定宿主机的端口, 因此我们不能直接访问它. 但是我们可以通过 Docker 的 link 机制来对这个 ZK 容器进行访问. 执行如下命令:

    docker run -it --rm --link my_zookeeper:zookeeper zookeeper zkCli.sh -server zookeeper
因为一个一个地启动 ZK 太麻烦了, 所以为了方便起见, 我直接使用 docker-compose 来启动 ZK 集群.
首先创建一个名为 docker-compose.yml 的文件, 其内容如下:

    version: '2'
    services:
        zoo1:
            image: zookeeper
            restart: always
            container_name: zoo1
            ports:
                - "2181:2181"
            environment:
                ZOO_MY_ID: 1
                ZOO_SERVERS: server.1=zoo1:2888:3888 server.2=zoo2:2888:3888 server.3=zoo3:2888:3888
    zoo2:
        image: zookeeper
        restart: always
        container_name: zoo2
        ports:
            - "2182:2181"
        environment:
            ZOO_MY_ID: 2
            ZOO_SERVERS: server.1=zoo1:2888:3888 server.2=zoo2:2888:3888 server.3=zoo3:2888:3888
    
    zoo3:
        image: zookeeper
        restart: always
        container_name: zoo3
        ports:
            - "2183:2181"
        environment:
            ZOO_MY_ID: 3
            ZOO_SERVERS: server.1=zoo1:2888:3888 server.2=zoo2:2888:3888 server.3=zoo3:2888:3888

安裝docker-compose

    yum install -y docker-compose
    
    $ pip install virtualenv
    $ virtualenv venv
    $ source venv/bin/activate
    (venv) $ pip install docker-compose
    (venv) $ docker-compose --version
    docker-compose version: 1.4.2
    
    pip install -U docker-compose

接着我们在 docker-compose.yml 当前目录下运行:
    
    COMPOSE_PROJECT_NAME=zk_test docker-compose up
    COMPOSE_PROJECT_NAME=zk_test docker-compose up -d
    
    COMPOSE_PROJECT_NAME=zk_test docker-compose ps
    COMPOSE_PROJECT_NAME=zk_test docker-compose down
    
使用 Docker 命令行客户端连接 ZK 集群
通过 docker-compose ps 命令, 我们知道启动的 ZK 集群的三个主机名分别是 zoo1, zoo2, zoo3, 因此我们分别 link 它们即可:

    docker run -it --rm \
        --link zoo1:zk1 \
        --link zoo2:zk2 \
        --link zoo3:zk3 \
        --net zktest_default \
        zookeeper zkCli.sh -server zk1:2181,zk2:2181,zk3:2181

通过本地主机连接 ZK 集群
因为我们分别将 zoo1, zoo2, zoo3 的 2181 端口映射到了 本地主机的2181, 2182, 2183 端口上, 因此我们使用如下命令即可连接 ZK 集群了:

    zkCli.sh -server localhost:2181,localhost:2182,localhost:2183

    