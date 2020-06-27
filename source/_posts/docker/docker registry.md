
### 1、安装

    docker run -d --restart=always -e SETTINGS_FLAVOR=dev -e STORAGE_PATH=/data/registry -v /data/docker-images:/data/registry -p 5000:5000 registry
    docker run -d -e SETTINGS_FLAVOR=dev -e STORAGE_PATH=/data/registry -v /data/docker-images:/data/registry -p 5000:5000 registry
    
### 2、配置

- 老版本：

    `sudo sh -c 'echo DOCKER_OPTS=\"--insecure-registry www.zhixuntongda.com:5000\" >> /etc/default/docker'`

- 新版本:

    ```
    vim /etc/docker/daemon.json
    { "insecure-registries":["www.zhixuntongda.com:5000"] }
    sudo service docker restart
    ```

### 3、推送
拉取image到本地

    docker pull library/centos6
    
本地对份镜像启动起来，形成container，给container去另外一个名字

    docker tag 2b4d84fdd66f www.zhixuntongda.com:5000/xwl-client
    docker tag 2e33c17a7f5f www.zhixuntongda.com:5000/xwl-dubbo
 
最后将新的docker images推送到私服上
 
    docker push www.zhixuntongda.com:5000/xwl-client
    docker push www.zhixuntongda.com:5000/xwl-dubbo
    
#### 4、测试
从私服上搜索存在哪些可用镜像

    $curl  http://www.zhixuntongda.com:5000/v2/_catalog
    {"repositories":["xwl-client"]}
    
    $ curl  http://www.zhixuntongda.com:5000/v2/xwl-client/tags/list
    {"name":"xwl-client","tags":["latest"]}
        
 
