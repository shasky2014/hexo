---
title: hexo+git+github配置个人博客
date: 2016-11-06 12:22:19
tags: "github","git","hexo"
---


### 本地安装git

##### 1. 链接`github`[个人账户](https://shasky2014.github.io/)

```bash
$ git config --global user.name 'shasky2014'

$ git config --global user.email '249398363@qq.com'

$ git config --list

$ ssh-keygen -t rsa -C "249398363@qq.com" //邮箱同上

$ cat /home/linx/.ssh/id_rsa.pub //复制里面的密钥
# 到github网页中登陆自己的账号，然后再account setting中，找到SSH KEY讲复制的密钥加入（需要再次输入github的密码）


~$ ssh Git@github.com 
ssh: connect to host github.com port 22: Connection timed out
# 开始报了错,继续解决...
```
###### 报错解决

```bash

# 主要是国内墙了github,改用配置方式翻墙.
~$ cd ~/.ssh/
~$ touch config

~$ vim config
# 添加如下信息
host github.com
user 249398363@qq.com
hostname ssh.github.com
preferredAuthentications publickey
identityFile ~/.ssh/id_rsa
port 443

# 测试连接是否成功
$ ssh -T git@github.com
Hi shasky2014! You ve successfully authenticated, but GitHub does not provide shell access.
# 到此成功用 git 连上 github
```
##### 2. 下载`github`工程,更新工程文件

```bash
# 下载项目 clone
$ git clone git@github.com:shasky2014/study_C-.git


# 修改本地内容后,更新当前项目

$ git add -A
$ git commit -m 'add testtxt'
$ git push origin  master

```
##### 3. 配置个人博客主页


在github中建一个`shasky2014.github.io`的项目库(`repository`)

在项目库中建`index.html`,个人github主页就建好了

##### 3.1 使用hexo工具建个性化博客.

使用hexo建立主页,省的自己搭建博客,方便.

hexo需要先安装node.js,去[node.js官网](http://nodejs.cn/)下载,安装

然后命令行下载`hexo`

```bash
$ npm install -g hexo-cli
...
```


切到博客目录下,安装hexo-deployer-git插件,初始化hexo

```bash
$ cd ~/hexo/
$ npm install hexo-deployer-git --save
   ...
$ hexo init 
   ...
```


配置hexo,关联到个人github主页,这里登陆权限不用再配置了,使用本地git的信息登陆.

打开`~\Hexo`文件夹中的`_config.yml`文件，找到如下位置，填写

```bash
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy: 
  type: git
  repo: git@github.com:MyGithub/MyGithub.github.io
```


最后,把本地的hexo同步到github项目库中.
```bash
hexo g -d
```
