
## java8 + tomcat

    [root@localhost]# mongo

#### 添加超级管理账号

    > use crawler
    > db.createUser(
         {
           user:"admin",
           pwd:"123",
           roles:[{role:"readWrite",db:"crawler"}]
         }
      )

#### 查看用户是否创建成功

    >show users


## mongodb

    mongoexport -d test -c json_depth -o depth.dat
    mongoexport -d test -c json_trade -o trade.dat
    

    mongoimport -d test -c json_depth depth.dat
    mongoimport -d test -c json_trade trade.dat
    

## chromedriver

    cd /etc/yum.repos.d
    wget http://people.centos.org/hughesjr/chromium/6/chromium-el6.repo 
    yum install chromium==3.11.0

    
    pip install selenium
    
    yum install -y https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
    
    wget https://chromedriver.storage.googleapis.com/2.38/chromedriver_linux64.zip
    unzip chromedriver_linux64.zip
    cp chromedriver /usr/local/bin/
    
#### selenium

在cmd中输入

    python

然后在python界面输入

    import selenium
    help(selenium)


    __version__ = '3.11.0'

## 运行

    java  -Dwebdriver.chrome.driver="/usr/local/Cellar/python@2/2.7.14_3/Frameworks/Python.framework/Versions/2.7/bin/chromedriver" -jar news/target/news-0.0.1-SNAPSHOT.jar
    
    java  -jar stock/target/stock-0.0.1-SNAPSHOT.jar
    
    java  -jar web/target/web-0.0.1-SNAPSHOT.jar
    
    
    java -Dwebdriver.chrome.driver="/usr/local/bin/chromedriver" -jar news-0.0.1-SNAPSHOT.jar
    
    java -jar stock-0.0.1-SNAPSHOT.jar
    
    java -jar web-0.0.1-SNAPSHOT.jar


## react-admin


    npm config set registry https://registry.npm.taobao.org --global
    npm config set disturl https://npm.taobao.org/dist --global




## nginx

    brew install nginx
    
    sudo xcode-select --install
    
    brew services start nginx
    
    /usr/local/var/www
    
    
    
    vim /usr/local/etc/nginx/nginx.conf
    
    location /api/ {
        proxy_pass  http://localhost:8080/api/;
    }
        

    
    /usr/local/nginx/conf/nginx.conf
    
    location / {
            root /root/app/react-admin/build/;
    }

    location /api/ {
            proxy_pass  http://localhost:8080/api/;
    }    
    