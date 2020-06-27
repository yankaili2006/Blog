### mysql

#### 临时密码丢失

    https://blog.csdn.net/lihaitao_1/article/details/54024652

### sql_mode=only_full_group_by] with root cause
    
    ; bad SQL grammar []; nested exception is com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: Expression #20 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'c.commentCount' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by] with root cause
    com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: Expression #20 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'c.commentCount' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by
    
#### 两种解决方法
    
    set sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
    
    set global sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
        
#### 彻底解决方法

    sudo vim /etc/my.cnf
    
    [mysqld]
    sql_mode='NO_AUTO_VALUE_ON_ZERO,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION,PIPES_AS_CONCAT,ANSI_QUOTES'


###  MAC OX命令行启动/停止/重启MySQL命令:

    sudo /usr/local/mysql/support-files/mysql.server start

    sudo /usr/local/mysql/support-files/mysql.server stop
    
    sudo /usr/local/mysql/support-files/mysql.server restart



### sql文件太大

SET GLOBAL max_allowed_packet=1073741824;



### mysql导入报错

    ERROR 1840 (HY000) at line 24: @@GLOBAL.GTID_PURGED can only be set when @@GLOBAL.GTID_EXECUTED is empty.


进入mysql模式，重置master

    # mysql -u root -p

输入密码
    
    mysql> reset master; 
　　
#### 重启sql

    mkdir -p /var/run/mysqld/
    ls -ld /var/run/mysqld/
    chown mysql.mysql /var/run/mysqld/
    service mysqld restart
    /etc/init.d/mysqld start


### centos 安装mysql

    https://typecodes.com/linux/yuminstallmysql5710.html 
    
    systemctl restart  mysqld.service
   
### 创建数据库
    
    CREATE DATABASE IF NOT EXISTS zxtd DEFAULT CHARSET utf8 COLLATE utf8_general_ci;


### 允许root远程登录

    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'xposedfP8[+3bmx@s3.eq}k' WITH GRANT OPTION;
    FLUSH PRIVILEGES
    
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'fuyinhy123' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
    
    use mysql;
    update user set host='%' where user='root' AND host='localhost';
    FLUSH PRIVILEGES;
    
    
### 查看mysql库各表容量大小

    select 
    table_schema as '数据库',
    table_name as '表名',
    table_rows as '记录数',
    truncate(data_length/1024/1024, 2) as '数据容量(MB)',
    truncate(index_length/1024/1024, 2) as '索引容量(MB)'
    from information_schema.tables
    where table_schema='cashloansc_nuanshou'
    order by data_length desc, index_length desc;
    
    
    