
2017-03-19，mysql启动失败，耽误了很长时间。[解决方案](http://www.cnblogs.com/ivictor/p/5146247.html)
    
    
    
    mkdir -p /var/run/mysqld/
    ls -ld /var/run/mysqld/
    chown mysql.mysql /var/run/mysqld/
    /etc/init.d/mysqld start
    
CREATE DATABASE phone CHARACTER SET utf8 COLLATE utf8_general_ci;
    