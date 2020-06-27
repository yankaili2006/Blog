

### JDK

    yum search java | grep -i --color JDK
    yum install -y java-1.8.0-openjdk-devel.x86_64

### Mysql

    yum install -y mysql
    yum install -y mysql-devel

    wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
    rpm -ivh mysql-community-release-el7-5.noarch.rpm
    yum install -y mysql-community-server

配置

    service mysqld restart

    systemctl start  mysqld.service

    mysql -u root 
    set password for 'root'@'localhost' =password('xposedfP8[+3bmx@s3.eq}k');
    grant all privileges on *.* to root@'%'identified by 'xposedfP8[+3bmx@s3.eq}k';
    flush privileges;

/etc/my.cnf

    [client]  
    default-character-set=utf8mb4  
      
    [mysqld]  
    character-set-server = utf8mb4  
    collation-server = utf8mb4_unicode_ci  
    init_connect='SET NAMES utf8mb4'  
    skip-character-set-client-handshake = true  
      
    [mysql]  
    default-character-set = utf8mb4  


    create database onesatoshiblog CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    
放开端口

    /sbin/iptables -I INPUT -p tcp --dport 3306 -j ACCEPT
    
### nginx

    sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
    
    sudo yum install -y nginx
    
    sudo systemctl start nginx.service
    sudo systemctl enable nginx.service
    
/etc/nginx/nginx.conf


### iptables
    
    iptables -L -n
     
    iptables -A INPUT -p tcp --dport 8443 -j ACCEPT　
    iptables -A INPUT -p tcp --dport 8185 -j ACCEPT　
    iptables -A INPUT -p tcp --dport 18080 -j ACCEPT　

### firewall
    
查看端口：
    
    firewall-cmd --list-ports

添加端口

    firewall-cmd --zone=public --add-port=8185/tcp --permanent
    firewall-cmd --zone=public --add-port=8443/tcp --permanent
    
生效

    firewall-cmd --reload    

    firewall-cmd --zone=public --add-port=80/tcp --permanent
    firewall-cmd --zone=public --add-port=8443/tcp --permanent
    firewall-cmd --zone=public --add-port=8185/tcp --permanent
    firewall-cmd --zone=public --add-port=8999/tcp --permanent
    
    
    firewall-cmd --zone=public --add-port=3306/tcp --permanent
    
    firewall-cmd --zone=public --remove-port=3306/tcp --permanent
    
    firewall-cmd --reload
    
### redis
    
    yum install -y epel-release
    yum install -y redis
    
    vim /etc/redis.conf 

找到下面这一行 `bind 127.0.0.1` 注释掉 `#bind 127.0.0.1`
    
    #requirepass foobared
    
    service redis restart
    
    chkconfig redis on
    
    
### config

    update sys_config set site_url = 'http://198.13.54.170:8443', static_web_site = 'http://198.13.54.170:8443';
    
    update sys_config set site_url = 'http://www.xposed.store', static_web_site = 'http://www.xposed.store';
    
    