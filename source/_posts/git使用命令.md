---
title: git常用命令
date: 2016-12-10 17:02:56
tags: [github,git,hexo]
---

1. hexo更新发布
```bash
# 发布更新
hexo g -d
# 启动本地测试访问 http://localhost:4000/ 查看最新的主站内容.
hexo s
```

2. git上传本地仓库
```bash
# 进入到要发布的github的项目文件目录下
cd /d/github/hexo

# 初始化为git项目
echo "# hexo" >> README.md
git init

# 这里可以直接 git add -A 添加项目到本地git项目
git add README.md
git commit -m "first commit"
# 链接github远程端的项目库
git remote add origin git@github.com:shasky2014/hexo.git
# 完成同步,发布到github
git push -u origin master
```

3. [git更新发布](http://blog.csdn.net/dazhi_100/article/details/38851733)
```bash
# 先发布到本地的git工程
git add -A
git commit
# 发push到github,origin是github工程的别名,master是git工程的别名
git push -u origin master
```