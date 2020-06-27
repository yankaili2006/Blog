


    $ go get -u github.com/Masterminds/glide
    $ git clone https://github.com/btcsuite/btcd $GOPATH/src/github.com/btcsuite/btcd
    $ cd $GOPATH/src/github.com/btcsuite/btcd
    $ glide install
    $ go install . ./cmd/..



    [WARN]    Unable to checkout golang.org/x/crypto
    [ERROR]    Update failed for golang.org/x/crypto: Cannot detect VCS
    [ERROR]    Failed to do initial checkout of config: Cannot detect VCS


    $ rm -rf ~/.glide
    $ mkdir -p ~/.glide
    $ glide mirror set https://golang.org/x/mobile https://github.com/golang/mobile --vcs git
    $ glide mirror set https://golang.org/x/crypto https://github.com/golang/crypto --vcs git
    $ glide mirror set https://golang.org/x/net https://github.com/golang/net --vcs git
    $ glide mirror set https://golang.org/x/tools https://github.com/golang/tools --vcs git
    $ glide mirror set https://golang.org/x/text https://github.com/golang/text --vcs git
    $ glide mirror set https://golang.org/x/image https://github.com/golang/image --vcs git
    $ glide mirror set https://golang.org/x/sys https://github.com/golang/sys --vcs git
    
    然后在项目中执行
    $ glide init
    $ glide install



### cow和ss配合

    export http_proxy=http://127.0.0.1:7777
    export https_proxy=http://127.0.0.1:7777


### 安装golang.org/x/crypto

    cd $GOPATH/src/golang.org/x/
    rm -rf *
    
    go get -u -v golang.org/x/tools
    go get -u -v golang.org/x/crypto
    go get -u -v golang.org/x/image
    go get -u -v golang.org/x/mobile
    go get -u -v golang.org/x/net
    go get -u -v golang.org/x/sys
    go get -u -v golang.org/x/text




### 设置代理

    export GOPROXY=https://goproxy.io
