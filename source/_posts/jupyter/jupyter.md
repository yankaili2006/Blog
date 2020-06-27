
jupyter的改进，越来越小

### 插件开发

    pip3 install ipython
    pip3 install requests tornado pandas


### jupyter 插件安装和启用

https://mlln.cn/2018/03/31/jupyter%20notebook%E6%89%A9%E5%B1%95%E5%BC%80%E5%8F%91%E4%B9%8B%E5%89%8D%E7%AB%AF%E6%8F%92%E4%BB%B6%E5%BC%80%E5%8F%91/


https://www.osgeo.cn/jupyter/examples/Notebook/Distributing%20Jupyter%20Extensions%20as%20Python%20Packages.html


您可以使用以下命令来安装nbextension：

1
jupyter nbextension install path/to/my_extension/ [--user|--sys-prefix]
默认安装是系统范围的。您可以使用–user来执行每个用户的安装，或者使用–sys-prefix来安装到Python的前缀（例如，在虚拟或conda环境中）。 my_extension是包含Javascript文件的目录。这会将其复制到Jupyter数据目录（确切位置取决于操作系统/平台 - 请参阅Data Files）。

如果插件正在开发中, 还没发布，您可以使用--symlink标志来链接您的扩展，而不是复制它，这样不需要在更改后重新安装。

要使用你的扩展，你还需要启用它，它告诉笔记本接口加载它。你可以用另一个命令来做到这一点：

jupyter nbextension enable my_extension/main [--sys-prefix]

该参数引用包含您的load_ipython_extension函数的Javascript模块，在本例中为my_extension / main.js。有一个相应的禁用命令来停止使用扩展程序而不卸载它。

在版本4.2中进行了更改：添加了--sys-prefix参数

####

OAuth + JupyterHub Authenticator = OAuthenticator


### jupyter

    pip3 install jupyter

一个便捷获取配置文件所在路径的命令：

    jupyter notebook --generate-config

    jupyter notebook
    
    
#### jupyter hub的架构

    https://zero-to-jupyterhub.readthedocs.io/en/latest/administrator/architecture.html
    
#### jupyter插件    
    
    https://github.com/yuvipanda/jupyterlab-nbmetadata
    
    
    from ipykernel.kernelapp import IPKernelApp
    from .kernel import IPrivpyKernel
    
    IPKernelApp.launch_instance(kernel_class=IPrivpyKernel)

    
    
    """An example Jupyter kernel"""
    
    __version__ = '0.1'
    
    from .kernel import IPrivpyKernel


#### jupyterhub认证方式

    https://github.com/jupyterhub/jupyterhub/wiki/Authenticators
    
    ldapauthenticator
    CASAuthenticator for CAS Single Sign-on SSO
    JSONWebToken Authenticator 
    
#### jupyterhub存储pgcontents

    https://github.com/quantopian/pgcontents