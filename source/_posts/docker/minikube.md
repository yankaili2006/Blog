

##1.0 install minikube
### for mac

    sysctl -a | grep -E --color 'machdep.cpu.features|VMX'  # 显示非空，则表示环境可以用，否则环境不可用
    brew cleanup or brew cleanup -d -v
    brew install minikube
    for ubuntu

    curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube
    sudo mkdir -p /usr/local/bin/
    sudo install minikube /usr/local/bin/
    minikube version
    
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    sudo touch /etc/apt/sources.list.d/kubernetes.list 
    echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
    sudo apt-get update
    sudo apt-get install -y kubectl

## 2. create kuster
### 2.1 create minikube cluster

    local_ip=10.18.0.18
    alias proxy='export all_proxy=socks5://${local_ip}:1086 ALL_PROXY=socks5://${local_ip}:1086 http_proxy=http://${local_ip}:1087 HTTP_PROXY=http://${local_ip}:1087 https_proxy=http://${local_ip}:1087 HTTPS_PROXY=http://${local_ip}:1087 no_proxy=tsingj.local,localhost,127.0.0.1,10.18.0.19,10.96.0.0/12,192.168.99.0/24,192.168.39.0/24,192.168.0.0/16 NO_PROXY=tsingj.local,localhost,127.0.0.1,10.18.0.19,10.96.0.0/12,192.168.99.0/24,192.168.39.0/24,192.168.0.0/16'
    alias unproxy='unset all_proxy ALL_PROXY http_proxy HTTP_PROXY https_proxy HTTPS_PROXY no_proxy NO_PROXY'  # 注意只有当前terminal窗口有效，可以写到~/.bash_profile或者~/.bashrc
    proxy
    minikube delete #clear minikube’s local state, 报错可以忽略
    minikube start --cpus 4 --memory 10240 --disk-size=100g --image-repository=registry.aliyuncs.com/google_containers --registry-mirror=https://registry.docker-cn.com --insecure-registry=registry.tsingj.local --vm-driver='vmwarefusion'


使用shadowsocks的时候，这样设置：

    local_ip=127.0.0.1
    alias proxy='export all_proxy=socks5://${local_ip}:1080 ALL_PROXY=socks5://${local_ip}:1081 http_proxy=http://${local_ip}:1081 HTTP_PROXY=http://${local_ip}:1081 https_proxy=http://${local_ip}:1081 HTTPS_PROXY=http://${local_ip}:1081 no_proxy=tsingj.local,localhost,127.0.0.1,10.18.0.19,10.96.0.0/12,192.168.99.0/24,192.168.39.0/24,192.168.0.0/16 NO_PROXY=tsingj.local,localhost,127.0.0.1,10.18.0.19,10.96.0.0/12,192.168.99.0/24,192.168.39.0/24,192.168.0.0/16'
    proxy

### 2.2 add hosts to pull images

    minikube ssh
    sudo echo "10.18.0.18 registry.tsingj.local" >>/etc/hosts
    exit

### 3. 停止/开启集群服务

    minikube stop        # 关闭集群服务
    
    minikube start       # 开启集群服务， 注意上述2.1章节proxy的设置是临时的，执行minikube start时需要重新设置proxy

### 问题

#### 1、'vmwarefusion' 驱动程序报告了一个问题： 
vmrun path check: exec: "vmrun": executable file not found in $PATH
建议：Install VMWare Fusion
文档：https://minikube.sigs.k8s.io/docs/reference/drivers/vmwarefusion/
似乎并未安装 vmwarefusions

    brew install docker-machine-driver-vmware
    brew services start docker-machine
    
    minikube delete
    minikube start --vm-driver=virtualbox --registry-mirror=https://registry.docker-cn.com --image-mirror-country=cn --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers
    
    minikube start --vm-driver=hyperkit --registry-mirror=https://registry.docker-cn.com --image-mirror-country=cn --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers
    
    minikube start --cpus 4 --memory 8192 --disk-size=100g --vm-driver=hyperkit --insecure-registry=harbor.tsingj.local --registry-mirror=https://registry.docker-cn.com --image-mirror-country=cn --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers
    minikube start --cpus 4 --memory 8192 --disk-size=100g --vm-driver=docker --insecure-registry=harbor.tsingj.local --registry-mirror=https://registry.docker-cn.com --image-mirror-country=cn --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers
    minikube start --cpus 4 --memory 8192 --disk-size=100g --insecure-registry=harbor.tsingj.local --registry-mirror=https://registry.docker-cn.com --image-mirror-country=cn --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers

    minikube start

### 安装镜像

参考链接
https://kubernetes.io/zh/docs/setup/learning-environment/minikube/

让我们使用名为 echoserver 的镜像创建一个 Kubernetes Deployment，并使用 --port 在端口 8080 上暴露服务。echoserver 是一个简单的 HTTP 服务器。

    kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.10 --port=8080
    
要访问 hello-minikube Deployment，需要将其作为 Service 公开
    
    kubectl expose deployment hello-minikube --type=NodePort
    
获取暴露 Service 的 URL 以查看 Service 的详细信息：

    minikube service hello-minikube --url
    
删除 hello-minikube Service：

    kubectl delete services hello-minikube
    
删除 hello-minikube Deployment：

    kubectl delete deployment hello-minikube    
    
停止本地 Minikube 集群：
    
    minikube stop
    
删除本地 Minikube 集群：
    
    minikube delete
    
### docker-machine-driver-hyperkit
    
    brew install kubectl    
    brew install minikube     
    brew install docker-machine-driver-hyperkit
    sudo chown root:wheel /usr/local/opt/docker-machine-driver-hyperkit/bin/docker-machine-driver-hyperkit
    sudo chmod u+s /usr/local/opt/docker-machine-driver-hyperkit/bin/docker-machine-driver-hyperkit
    minikube start --vm-driver hyperkit
