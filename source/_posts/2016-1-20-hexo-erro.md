title: HEXO 部署Git的坑
date: 2016-1-20 20:08:08
updated: 2016-11-30 20:08:08
tags:
	- HEXO
categories:
  - Test
---

# 部署Git 第一步配置config.yml 文件
找到根目录下的_config.yml，修改配置
```
deploy:
    type: git
    repo: https://github.com/pyrinelaw/pyrinelaw.github.io.git
    branch: master
```
注意`type`为`git`,不是`github`.
`repo`也可以写`repository`,后面地址为你要`push`的git地址,用http或者git都可以.
`branch`为你要`push`的分支,master为主分支.
如果repo配置git,且ssh 配置正确,部署过程会弹出提示框叫你输入ssh的秘钥,确认即可.
如果repo配置https,部署过程中会弹出提示框,输入账户名和密码.

# 1.部署提示找不到git (Can not find ***)
**解决办法**
在Hexo 3.0版本后deploy git 被分开的，所以需要安装，安装命令如下:
`npm install hexo-deployer-git --save`
安装好后在尝试一下就ok。

<!--more-->

# 2.部署提示 ｀event type error ***｀ ｀ spawn git ENOENT｀ 
**解决办法**
安装了`git bash`路径没有配置到环境变量path中.将你的git bash 安装路径添加到环境变量path中即可.我的是:
C:\Program Files\Git\mingw64\libexec\git-core
C:\Program Files\Git\bin

# 3.读取不到Git分支
```
Please make sure you have the correct access rights
and the repository exists.
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io
cs/troubleshooting.html
Error: fatal: 'github.com/pyrinelaw/pyrinelaw.github.io.git' does not appear
be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
**解决办法**
卸载Git 2.5版本，安装1.9版本，问题解决.
也可以尝试换https地址再试一下.

# 4.部署的时候执行：hexo  deploy 命令行没有任何输出，也没有错误。 
**解决办法**
在部署的_config.yml文件中，找到`deploy:`标签，在每个冒号后面必须要空格，否则就会出现上述问题。
比如：
```
    type:git
```
改为
```
    type: git
```

# 5.修改主题样式配置不起作用，而且hexo  generate还报错 
**解决办法**
需要到相应的主题文件夹下面进行修改.
比如我的主题为：themes\yelee 则在根目录下的`themes`找到该文件夹下，修改_config.yml文件，根目录下面也有个同样的名字，不注意，容易弄混，要主要修改的文件是否正确。并且注意加上空格

# 6.执行hexo server错误
**解决办法**
是因为在安装hexo 没有安装`hexo-server`模块
`npm install hexo-server --save` 解决

# 7.执行hexo server显示running at http://0.0.0.0:4000/ 
运行成功显示的http://0.0.0.0:4000/ 是没办法访问的，
可以尝试访问 http://localhost:4000/ 或 http://127.0.0.1:4000/
或者用`hexo s -p 80`把端口改为80,直接访问http://127.0.0.1

# 8.hexo d  ｀fatal: 'username.github.io' does not a....｀
**解决办法**
一 是检查 repo 的名字是否合乎规范、是否含有大写字母、config.yml 中的 deploy 配置是否正确，
二 是把 git bash 关掉，重新打开再执行命令。

# 9.莫名其妙的问题
**解决办法**
删除根目录下.deplou_git 文件夹重试
检查ssh是否配置正确
[官方教程配置ssh](https://help.github.com/articles/generating-an-ssh-key/)

# 10.hexo 3.0支持简写

hexo g ==  hexo generate

hexo d ==  hexo deploy

hexo s ==  hexo server

hexo n ==  hexo new

