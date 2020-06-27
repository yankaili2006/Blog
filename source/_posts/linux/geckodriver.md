

#### 安装Xvfb及其他依赖

    yum install xorg-x11-server-Xvfb bzip gtk3

#### 安装火狐

    cd /usr/local
    wget https://ftp.mozilla.org/pub/firefox/releases/56.0.2/linux-x86_64/en-US/firefox-56.0.2.tar.bz2
    tar xjvf firefox-56.0.2.tar.bz2
    
ln -s /usr/local/firefox/firefox /usr/bin/firefox

#### 安装Selenium

    wget https://files.pythonhosted.org/packages/14/d6/650f5d2e149b83cd24989653efedf47a24cafb72e9d2dd03191a9f52f2f4/selenium-3.8.1-py2.py3-none-any.whl
    pip install selenium-3.8.1-py2.py3-none-any.whl
    
这个一定要按照版本来

#### 安装gtk3 gtk2 旧的火狐版本是需要gtk2 的，新的需要gtk3为了不报错。还是全装上吧，

    yum install gtk3
    yum install gtk2

#### 安装火狐驱动

    wget https://github.com/mozilla/geckodriver/releases/download/v0.23.0/geckodriver-v0.23.0-linux64.tar.gz

    tar xzvf geckodriver-v0.23.0-linux64.tar.gz

    cp geckodriver /usr/local/bin/

#### 测试

##### 控制台输入firefox 

出现类似这个说明火狐安装成功。Error: GDK_BACKEND does not match available displays

##### 测试爬虫脚本

    from pyvirtualdisplay import Display
    from selenium import webdriver
    
    display = Display(visible=0, size=(800, 600))
    display.start()
    driver = webdriver.Firefox()
    driver.get('https://www.baidu.com')
    print(driver.title)
    driver.quit()
    display.stop()
    
输出：百度一下，你就知道说明安装成功。



