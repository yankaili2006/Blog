
#### hexo

    npm install hexo-cli -g
    hexo init blog
    cd blog
    npm install
    hexo server

#### [install theme](https://github.com/cofess/hexo-theme-pure)
    
    git clone https://github.com/cofess/hexo-theme-pure.git themes/pure
        

- [hexo](https://hexo.io/zh-cn/)

#### jekyll

- [jekyll doc](https://jekyllrb.com/docs/)
- [markdown语法备忘](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [jekyll themes](http://jekyllthemes.org/)

#### 依赖的项目

    https://github.com/yankaili2006/hexo-theme-pure
    

#### hexo 发布到 github pages

    npm install hexo-deployer-git --save

You can configure this plugin in _config.yml.

    # You can use this:
    deploy:
      type: git
      repo: <repository url>
      branch: [branch]
      token: ''
      message: [message]
      name: [git user]
      email: [git email]
      extend_dirs: [extend directory]
      ignore_hidden: false # default is true
      ignore_pattern: regexp  # whatever file that matches the regexp will be ignored when deploying

执行命令：

    hexo clean
    hexo deploy
    