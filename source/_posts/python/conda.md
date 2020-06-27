
#### mac上jupyterlab 安装

    https://lyric.im/c/the-craft-of-selfteaching/T-appendix.jupyter-installation-and-setup

    cd ~/Downloads/
    wget https://repo.anaconda.com/archive/Anaconda3-2018.12-MacOSX-x86_64.sh
    chmod +x Anaconda3-2018.12-MacOSX-x86_64.sh
    ./Anaconda3-2018.12-MacOSX-x86_64.sh


安装完毕之后，打开 Terminal(Windows 系统需要打开之前安装的 Anaconda Prompt 输入），继续安装几个组件：

    conda update conda
    conda update anaconda
    conda install -c conda-forge nodejs
    conda install -c conda-forge jupyterlab # 这是用来升级 jupyter lab 到最新版的方法
    

安装完毕之后，可以看看各个你将要用到的可执行命令都在什么地方，用 which 命令（windows下用 where 命令）：

    which python
    python --version
    which node
    node -v
    which jupyter
    jupyter lab --version
    jupyter notebook --version
    which pip
    pip --version
    
    
第一次启动 Jupyter lab
打开 Terminal，cd 到你想打开 Jupyter lab 的目录（就是你保存 ipynb 文件的地方，以便在 Jupyter lab 中打开、浏览、编辑 ipynb 文件），在这里以用户根目录为例 ~/：

    cd ~
    jupyter lab

