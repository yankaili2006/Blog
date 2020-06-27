
### 重启整个服务  迅物联

    docker restart dubbo-xwl-v2
    docker restart client-lyygrl-v2
    docker restart client-xwltqdh-v2
    docker restart client-wxtsdsdt-v2
    docker restart client-hbtrxxjs-v2
    docker restart client-jtxtrd-v2
    docker restart client-dchh-v2
    docker restart client-zxrr-v2
    docker restart client-wxtsd-v2
    docker restart client-xwl-v2
    docker restart client-hbwh-v2
    docker restart xwl-web-v2

    
### 重启服务 知讯通达

    docker restart dubbo-zxtd
    docker restart client-zxtd
    docker restart web-zxtd
    

### 清理文件命令

    

清理大文件

    find . -size +100M -exec ls -lh {} \;

    find . -name '*.log' -size +100M -exec rm -rf {} \;

