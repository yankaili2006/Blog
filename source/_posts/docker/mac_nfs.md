### mac nfs

#### create dir

    mkdir -p /data/nfs_data/data_privpy_dev/data/auth
    mkdir -p /data/nfs_data/data_privpy_dev/data/scripts
    sudo chmod -R 777 /data

    vi /etc/exports

添加：

    /opt/data/k8s -alldirs  -maproot=root:wheel -network=192.168.0.0 -mask=255.255.0.0

默认为可读写，加入 -ro 为只读 readonly
-alldirs 是共享 /Users 目录下所有文件
-network -mask 制定工作在那个网段内
-maproot=root:wheel，把client端的root用户映射为Mac OS上的root，client端的root组映射为Mac OS上的wheel (gid=0) 组。这个参数非常重要，否则会nfsroot链接失败。
修改配置后使用sudo nfsd checkexports进行检查。

#### 控制服务

    sudo nfsd enable
    
    sudo nfsd disable
    
    sudo nfsd start
    
    sudo nfsd stop
    
    sudo nfsd restart
    
    sudo nfsd status

查看共享状态

    showmount -e


#### 设置nfs server权限

    sudo vi /etc/nfs.conf

添加：

    nfs.server.mount.require_resv_port = 0
    
    sudo nfsd restart

#### 测试

    mount -t nfs 192.168.50.120:/data/nfs_data/ /tmp/nfs_data
