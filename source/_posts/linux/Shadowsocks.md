
## Shadowsocks

### 配置文件

    {
    "server":"0.0.0.0",
    "server_port":30080,
    "local_port":1080,
    "password":"8880066ccivv",
    "method":"aes-256-cfb",
    "timeout":300
    }

### 启动脚本

    /usr/bin/shadowsocks-server -c /etc/shadowsocks-go/config.json


    vim /usr/local/etc/privoxy/config

    /usr/local/Cellar/privoxy/3.0.26/sbin/privoxy --no-daemon /usr/local/etc/privoxy/config

    brew services restart privoxy
    
    

    vim /Users/yankaili/Library/Application\ Support/ShadowsocksX-NG/ss-local-config.json
    
    
    
    {
      "method" : "aes-128-gcm",
      "server" : "45.77.248.237",
      "password" : "8880066ccIvv",
      "local_address" : "127.0.0.1",
      "server_port" : 8989,
      "timeout" : 60,
      "local_port" : 1086
    }

