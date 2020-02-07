# （一） 树莓派，安卓手机（LinuxDeploy），Linux Geth 私链搭建，安装，配置，运行

> 本文档为混合教程，为 Geth 的私链搭建教程，目标为构建 windows 电脑，linux 服务器，安卓手机，树莓派的混合私链集群，有疑问请在 github 上的 issues 中提出或者在下方评论区回复，或者加群 457053357

##关键词：安卓手机配置区块链，LinuxDeploy 安装区块链，Geth 配置，以太坊配置

### 1.安卓手机配置（树莓派或者 Linux 可直接跳过）

> 小米手机一台，root，安装 LinuxDeploy
> 本例使用**红米 5a，2gRAM，16g 内存，4 核 ARM64**
> 删除温控,超频等操作来优化体验（使用内核调教等软件，酷安自寻）
> <img src="https://img-blog.csdnimg.cn/20200207200109620.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg3NzkwMA==,size_16,color_FFFFFF,t_70" width="50%"><img src="https://img-blog.csdnimg.cn/20200207200418246.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg3NzkwMA==,size_16,color_FFFFFF,t_70" width="50%">

> 以使用 Debian 为例 镜像源修改为

    http://mirrors.163.com/debian/

> 镜像大小

    8000mb

> 本地化选择

    zh_CN.UFT-8

> DNS 修改为

    114.114.114.114

> 启用 SSH

##### ！！！！不要开启图形界面

> 直接安装即可

### 2.控制台配置 Dbian，安装依赖

<img src="https://img-blog.csdnimg.cn/20200207200857513.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg3NzkwMA==,size_16,color_FFFFFF,t_70" width="100%">

> 先看看是用的哪个 shell

    ls -al /bin/sh

> 如果是 dash，切换到 bash,然后重新连接

    sudo ln -fs /bin/bash /bin/sh

> 安装 wget，git，gcc,make

    sudo apt-get  build-dep  gcc

    sudo apt-get install wget

    sudo apt-get install git

    sudo apt-get install make

> 安装 go ARM64 最新版本链接可在官网查询

    wget https://dl.google.com/go/go1.12.6.linux-arm64.tar.gz
    tar -xzvf go1.12.6.linux-arm64.tar.gz
    sudo mv go /usr/local

> 配置 GOPATH 以及解决 make 中的资源获取慢问题

    sudo nano ~/.profile

> 在最后加上

    #设置GOPATH
    export PATH=$PATH:/usr/local/go/bin
    #解决golang.org资源速度慢问题
    export GOPROXY=https://goproxy.cn

    sudo source ~/.profile

> 修正域名解析问题，然后重新启动 LinuxDeploy（测试地址是否 ping 通用 socket: permission denied，Temporary failure in name resolution 等错误）,**否则无法 wget，gitclone** https://github.com/meefik/linuxdeploy/issues/1158

    sudo usermod -aG aid_inet jiajia #jiajia为登录的用户名

> 修改 host，解决 git clone 速度过慢问题（速度正常请不要修改）

    sudo nano /etc/hosts

    #具体地址请参照百度教程
    13.250.177.223 github.com
    151.101.229.194 github.global.ssl.fastly.net

    sudo /etc/init.d/networking restart #更新DNS

> 测试

    ping baidu.com

> 不成功则重启 linuxdeploy

## 欢迎修改 https://github.com/jiajiayao/Docunent
