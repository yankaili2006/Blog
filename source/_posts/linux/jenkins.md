


### 安装
    
    yum -y install java 
    curl http://pkg.jenkins-ci.org/redhat/jenkins.repo -o /etc/yum.repos.d/jenkins.repo
    rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
    yum -y install jenkins
    
    
### 起停

    systemctl enable jenkins
    service jenkins start

### 配置

  WAR包位于: `/usr/lib/jenkins/`
  
  配置文件位于： `/etc/sysconfig/jenkins` 一般不需要配置
  
  home目录是：`/var/lib/jenkins`，开始的时候是空的，一般启动jenkins服务，就开始出现各种文件。
  
  日志文件是：`/var/log/jenkins/jenkins.log`

### jenkins执行docker命令

#### jenkins 加入 docker 用户组

这样在jenkin中可以直接执行docker命令

    sudo usermod -aG docker  jenkins
    sudo systemctl restart jenkins

#### 命令

    sudo /bin/docker build





### jenkins install

    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
    
    sudo yum install jenkins
    
    sudo service jenkins start
    sudo service jenkins stop
    sudo service jenkins restart<br><br>
    
    sudo chkconfig jenkins on
    
    systemctl status jenkins.service
    
  