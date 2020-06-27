
#### 删除已经存在的镜像

    docker rm xwl-weixin-h5
    docker rm xwl-web
    docker rm xwl-client
    docker rm xwl-dubbo


#### 构建镜像

    export JENKINS_JOB=/data/jenkins/jobs/zxtd/workspace
    
    cd $JENKINS_JOB/xwl-dubbo
    docker build -t www.zhixuntongda.com:5000/xwl-dubbo:latest .
    docker push www.zhixuntongda.com:5000/xwl-dubbo:latest
    
    cd $JENKINS_JOB/xwl-cmpp-client
    docker build -t www.zhixuntongda.com:5000/xwl-client:latest .
    docker push www.zhixuntongda.com:5000/xwl-client:latest
    
    cd $JENKINS_JOB/xwl-web
    docker build -t www.zhi
    xuntongda.com:5000/xwl-web:latest .
    docker push www.zhixuntongda.com:5000/xwl-web:latest
    
    cd $JENKINS_JOB/xwl-weixin-h5
    docker build -t www.zhixuntongda.com:5000/xwl-weixin-h5:latest .
    docker push www.zhixuntongda.com:5000/xwl-weixin-h5:latest


#### 拉取最新镜像

    docker pull www.zhixuntongda.com:5000/xwl-dubbo:latest
    docker pull www.zhixuntongda.com:5000/xwl-client:latest
    docker pull www.zhixuntongda.com:5000/xwl-web:latest
    docker pull www.zhixuntongda.com:5000/xwl-weixin-h5:latest


#### 运行docker xwl
 
##### dubbo

    docker run -d --restart unless-stopped -p 20880:20880 --name dubbo-xwl-v2 -v /opt/tomcat/xwl-web/upload:/opt/tomcat/xwl-web/upload -e "appId=xwl" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-dubbo:latest

##### client

    docker run -d --restart unless-stopped -p 20881:20880 --name client-xwl-v2 -e "appId=xwl" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20882:20880 --name client-wxtsd-v2 -e "appId=wxtsd" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20883:20880 --name client-zxrr-v2 -e "appId=ZXRR" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20884:20880 --name client-hbwh-v2 -e "appId=hbwh" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl  -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20885:20880 --name client-dchh-v2 -e "appId=dchh" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20886:20880 --name client-jtxtrd-v2 -e "appId=JTXTRD" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20887:20880 --name client-hbtrxxjs-v2 -e "appId=HBTRXXJS" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20888:20880 --name client-wxtsdsdt-v2 -e "appId=WXTSDSDT" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 20889:20880 --name client-xwltqdh-v2 -e "appId=TQDH" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest

##### web

    docker run -d --restart unless-stopped -p 5081:8080 --name xwl-web-v2 -v /opt/tomcat/xwl-web/upload:/opt/tomcat/xwl-web/upload -e "appId=xwl" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-web:latest
    docker run -d --restart unless-stopped -p 5082:8080 --name xwl-weixin-v2 -e "appId=xwl" -e "registry=zookeeper://123.57.52.172:2181?backup=123.57.52.172:2182,123.57.52.172:2183" -e "JAVA_OPTS=-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-weixin-h5:latest


#### 运行docker  zxtd


### zxtd

    docker run -d --restart unless-stopped --net=host -p 20880:20880 --name dubbo-zxtd -e "appId=zxtd" -e "registry=zookeeper://101.200.176.31:2181?backup=101.200.176.31:2182,101.200.176.31:2183" -e "JAVA_OPTS=-Dspring.profiles.active=zxtd -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-dubbo:latest
    docker run -d --restart unless-stopped -p 20881:20880 --name client-zxtd -e "appId=zxtd" -e "registry=zookeeper://101.200.176.31:2181?backup=101.200.176.31:2182,101.200.176.31:2183" -e "JAVA_OPTS=-Dspring.profiles.active=zxtd -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-client:latest
    docker run -d --restart unless-stopped -p 5081:8080 --name web-zxtd -e "appId=zxtd" -e "registry=zookeeper://101.200.176.31:2181?backup=101.200.176.31:2182,101.200.176.31:2183" -e "JAVA_OPTS=-Dspring.profiles.active=zxtd -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log" www.zhixuntongda.com:5000/xwl-web:latest


#### 运行时环境变量

    JAVA_OPTS="-Dspring.profiles.active=xwl -Xms128m -Xmx512m -Xss512k -XX:NewSize=128m -server -XX:+DisableExplicitGC -verbose:gc -XX:+PrintGCDateStamps -XX:+PrintGCDetails -Xloggc:/tmp/gc.log"
    environment:
      - JVM_OPTS=-Xmx12g -Xms12g -XX:MaxPermSize=1024m
    
