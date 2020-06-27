#### redis

`https://www.jianshu.com/p/af33284aa57a`

    brew install redis

To have launchd start redis now and restart at login:

    brew services start redis

Or, if you don't want/need a background service you can just run:

    redis-server /usr/local/etc/redis.conf



    set a 123;//设置缓存：a=>123
    EXPIRE a 3600;//设置缓存时间（秒）
    TTL a；//查看缓存剩余时间

#### 给redis设置密码

/usr/local/etc/redis.conf 中找到

    # requirepass foobared
    
修改为

    requirepass qwe!@#123
    
    