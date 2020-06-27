
#### 使用rancher安装mysql

需要设置环境变量：MYSQL_ROOT_PASSWORD 端口映射MYSQL_DATABASE

rancher自带的 rawmind/alpine-zk:3.4.9

jenkins 无法联网

    --dns 8.8.8.8
    
[docker使用技巧](https://github.com/Dataman-Cloud/shurenyun-user-manual/blob/master/docker/3/Docker%E5%B0%8F%E6%8A%80%E5%B7%A7.md)

#### 进入容器

获取容器第第一个进程在宿主机上的PID号

    docker inspect -f {{.State.Pid}}  <container_name>|<container_ID>

使用nsenter进入该容器

    nsenter --target <container_pid> --mount --uts --ipc --net --pid

