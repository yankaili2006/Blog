

## registry

    docker run -d -p 5000:5000 --restart always --name registry registry:2

#### 镜像加速配置

- linux
    
    `vim /etc/docker/daemon.json`
    
- mac

    `vim ~/.docker/daemon.json`


    { "insecure-registries":["192.168.12.247:5000"] }

    {
            "registry-mirrors": ["https://z02l1jun.mirror.aliyuncs.com"],
            "insecure-registries":["123.57.52.172:5000"]
    }
    
    
    sudo cp -n /lib/systemd/system/docker.service /etc/systemd/system/docker.service
    sudo sed -i "s|ExecStart=/usr/bin/docker daemon|ExecStart=/usr/bin/docker daemon --registry-mirror=https://z02l1jun.mirror.aliyuncs.com|g" /etc/systemd/system/docker.service
    sudo sed -i "s|ExecStart=/usr/bin/dockerd|ExecStart=/usr/bin/dockerd --registry-mirror=https://z02l1jun.mirror.aliyuncs.com|g" /etc/systemd/system/docker.service
    sudo systemctl daemon-reload
    sudo service docker restart
    
    
### 启动docker服务

    COMPOSE_PROJECT_NAME=zk_test docker-compose ps
    COMPOSE_PROJECT_NAME=zk_test docker-compose up -d
    
    COMPOSE_PROJECT_NAME=zk_test docker-compose up -d


### docker file配置

    vim /etc/docker/daemon.json
    {
        "log-driver":"json-file",
        "log-opt":{
            "max-size":"10m",
            "max-file":1
        }
    }
    
    
### 一、docker安装
  
#### 1、添加 yum 源
使用 Docker 官方提供的 CentOS 软件源。执行下面的命令添加 yum 软件源。

    $ sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
    [dockerrepo]
    name=Docker Repository
    baseurl=https://yum.dockerproject.org/repo/main/centos/7/
    enabled=1
    gpgcheck=1
    gpgkey=https://yum.dockerproject.org/gpg
    EOF

#### 2、安装 Docker
更新 yum 软件源缓存，并安装 docker-engine。

    $ sudo yum update
    $ sudo yum install docker-engine
    
启动 Docker 引擎

    $ sudo systemctl enable docker
    $ sudo systemctl start docker
    
使用国内的Docker仓库daocloud：

    curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://aa5523ba.m.daocloud.io
    
    systemctl restart docker
    
安装rancher

    docker run -d --restart=always -p 8080:8080 rancher/server
    
    