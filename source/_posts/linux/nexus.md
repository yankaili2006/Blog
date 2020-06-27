
## 借鉴文章
   
    https://mritd.me/2017/01/08/set-up-docker-registry-by-nexus/

## 安装 nexus

#### 首先将 nexus 移动到任意位置

    wget --no-check-certificate https://download.sonatype.com/nexus/3/nexus-3.2.0-01-unix.tar.gz
    tar -zxvf nexus-3.2.0-01-unix.tar.gz

    mv nexus-3.2.0-01 /usr/local
    
#### 创建 nexus 用户

    adduser -r -s /sbin/nologin -d /data/nexus-data nexus

默认 nexus 运行后会在同级目录下创建一个 sonatype-work 工作目录，并将其数据保存在此目录中，所以为了数据持久化先手动创建并设置其数据存储位置

    创建基本目录结构
    mkdir -p /usr/local/sonatype-work
    
    创建建数据目录
    mkdir -p /data/nexus-data/{etc,log,tmp}
    
    将数据目录软连接到工作目录
    ln -s /data/nexus-data /usr/local/sonatype-work/nexus3

    更新所有目录权限
    chmod -R 755 /usr/local/{sonatype-work,nexus-3.2.0-01} /data/nexus-data
    chown -R nexus:nexus /usr/local/{sonatype-work,nexus-3.2.0-01} /data/nexus-data

最后启动 nexus 访问 8081 端口即可

    以前台方式运行
    sudo -u nexus /usr/local/nexus-3.2.0-01/bin/nexus run
    
    后台运行
    sudo -u nexus /usr/local/nexus-3.2.0-01/bin/nexus start

    clean compile install -U -Dmaven.test.skip=true
    release:prepare
    release:perform  -Darguments="-Dmaven.javadoc.skip=true

    http://123.57.52.172:8081/
    

### 数据迁移
    
    /usr/local/sonatype-work
    
    tar -czvf sonatype-work.tgz /usr/local/sonatype-work
    
    scp jobs-cashloan.tgz root@123.57.52.172:/root/
    
    

## 2

    wget https://sonatype-download.global.ssl.fastly.net/nexus/oss/nexus-2.1.2-bundle.tar.gz
    tar -xzvf nexus-2.1.2-bundle.tar.gz
    mv nexus-2.1.2 /usr/local
    
    adduser -r -s /sbin/nologin -d /data/nexus-data nexus
    
    创建基本目录结构
    mkdir -p /usr/local/sonatype-work
    
    创建建数据目录
    mkdir -p /data/nexus-data/{etc,log,tmp}
    
    cp /usr/local/nexus-2.1.2/bin/jsw/linux-x86-64/nexus /etc/init.d/nexus
    
    更新所有目录权限
    chmod -R 755 /usr/local/{sonatype-work,nexus-2.1.2} /data/nexus-data
    chown -R nexus:nexus /usr/local/{sonatype-work,nexus-2.1.2} /data/nexus-data
    
    sudo -u nexus /usr/local/nexus-2.1.2/bin/nexus start
        
    后台运行
    sudo -u nexus /usr/local/nexus-2.1.2/bin/nexus start


### jar

    mvn deploy:deploy-file -DgroupId=bouncycastle \
     -DartifactId=bcmail-jdk14 \
     -Dversion=1.4.5 \
     -Dpackaging=jar \
     -Dfile=./bouncycastle/bcmail-jdk14/1.4.5/bcmail-jdk14-1.4.5.jar \
     -DrepositoryId=<id-to-map-on-server-section-of-settings.xml> \
     -Durl=/bouncycastle/bcmail-jdk14/1.4.5/bcmail-jdk14-1.4.5.jar
     