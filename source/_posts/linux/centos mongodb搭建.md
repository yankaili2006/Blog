
### 一、安装环境及配置yum

    vi /etc/yum.repos.d/mongodb-org-3.2.repo


    
    [mongodb-org-3.2]
    name=MongoDB Repository
    baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/
    gpgcheck=1
    enabled=1
    gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc



## 二、安装MongoDB


    yum -y install mongodb-org


## 三、验证


    /etc/init.d/mongod start
    mongo

## 配置端口

查看端口：
    
    firewall-cmd --list-ports

添加端口

    firewall-cmd --zone=public --add-port=8185/tcp --permanent
    firewall-cmd --zone=public --add-port=8443/tcp --permanent
    
生效

    firewall-cmd --reload    

    /sbin/iptables -I INPUT -p tcp --dport 27017 -j ACCEPT
    
    貌似没用：
    
    
    
    
    /sbin/iptables -I INPUT -p tcp --dport 9999 -j ACCEPT




    brew install mongodb
    

注意：/data/db 是 MongoDB 默认的启动的数据库路径(–dbpath)


    sudo mkdir -p /data/db
    sudo chown -R yankaili /data/db
    cd /usr/local/Cellar/mongodb/3.6.3/bin
    mongod
    

把mongod加入环境变量中

    vim ~/.bash_profile
    export PATH=/usr/local/Cellar/mongodb/3.6.3/bin:$PATH
    source ~/.bash_profile

配置文件在

    /usr/local/etc/mongod.conf
    

开一个新终端 启动客户端

    mongo
    
    use admin
    
    db.createUser({ user: "root", pwd: "StarChat@123", roles: [{ role: "userAdminAnyDatabase", db: "admin" }] })
    db.createUser({ user: "root", pwd: "StarChat@123", roles: [{ role: "userAdminAnyDatabase", db: "admin" }, { role: "dbOwner", db: "limayq" }] })
    
    db.grantRolesToUser( "root", [ { role: "dbOwner", db:"admin"} ] )
    db.grantRolesToUser( "root", [ { role: "dbOwner", db:"limayq"} ] )
    use limayq
    
    db.createUser({ user: "root", pwd: "StarChat@123", roles: [{ role: "dbOwner", db: "limayq" }] })
    
    use limayq
    db.auth("root", "StarChat@123")
    
    db.dropUser("root")
    db.getUsers()
    
    
    mongoexport -h 172.18.0.1 --port 27017 -u root -p StarChat@123 -d limayq -c sjmh_report2019032709 -o sjmh_report2019032709.json
    mongoexport -h 172.18.0.1 --port 27017 -u root -p StarChat@123 -d limayq -c sjmh_basedata_json2019032709 -o sjmh_basedata_json2019032709.json
    mongoexport -h 172.18.0.1 --port 27017 -u root -p StarChat@123 -d limayq -c cl_sjmhope_call_record -o cl_sjmhope_call_record.json
    
    
    
    docker cp 3657ef3e12ed47d8b70e6979bc0765bc20d62a67e39006efbcd5633a51495e0c:/sjmh_report2019032709.json .
    docker cp 3657ef3e12ed47d8b70e6979bc0765bc20d62a67e39006efbcd5633a51495e0c:/sjmh_basedata_json2019032709.json .
    docker cp 3657ef3e12ed47d8b70e6979bc0765bc20d62a67e39006efbcd5633a51495e0c:/cl_sjmhope_call_record.json .
    
    
    
    