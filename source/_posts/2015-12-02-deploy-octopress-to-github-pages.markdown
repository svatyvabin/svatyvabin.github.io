---
layout: post
title: "在 Github Pages 上使用 Octopress 创建自己的博客"
date: 2015-12-02 19:50:37 +0800
author: svatyvabin
comments: true
categories:
- Octopress
- Github Pages
- Blog
---

## 1. [安装 Octopress](http://octopress.org/docs/setup/)
### 1.1 安装必要的软件
在终端下输入：
```
sudo apt-get install ruby ruby-dev nodejs rbenv

sudo gem install execjs
```

gem 下载速度比较慢，耐心等待，如果提示 ``Error`` 或者一直没有响应，可以用淘宝提供的[ gem 镜像](https://ruby.taobao.org/)，修改 gem 和 bundle 这两个镜像。

### 1.2 安装 Octopress
下载 octopress，并进入 octopress 目录：
```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
```

然后安装依赖：
```
sudo gem install bundler
rbenv rehash
bundle install
```
注意每条命令的提示，确保每一步都是正确的。如果命令出错，应该是缺少某个软件，可以谷歌搜索一下解决。

最后安装默认的主题：
```
rake install
```

## 2. [部署到 Github Pages 上](http://octopress.org/docs/deploying/github/)
### 2.1 创建 Github Pages
根据 [Github Pages](https://pages.github.com/) 官网的简易教程，就可以创建一个自己的 Github Pages 网站了。
需要注意的是，repository 名称前缀必须是你的用户名，例如你的用户名是 joe，那你的 repository 名称就必须是 joe.github.io。

创建成功后，为了方便以后使用 git 命令，建议在 [github](https://github.com/settings/ssh) 的设置中添加本机的 ``SSH keys``，这样就不需要输入密码了，如何生成 ``SSH keys`` 可以参考[上面的官方教程](https://help.github.com/articles/generating-ssh-keys/#platform-linux)。

### 2.2 部署到 Github Pages
在 octopress 目录下，使用命令：
```
rake setup_github_pages
```
之后会要求你输入 repository 地址，在你刚刚创建的 repository 主页上复制类似 ``git@github.com:joe/joe.github.io.git`` 的地址就粘贴到这里就行了（快捷键 ``Ctrl + Shift + V``）。

之后使用命令：
```
rake generate
```
生成博客。

使用命令：
```
rake deploy
```
将网站上传到你的 Github Pages 上

同时将 octopress 下的 source 上传到 Github 上：
```
git add .
git commit -m "commit"
git push origin source
```
注意，这里必须 push 到 ``source`` 分支上，``source`` 分支上保存着文章等信息。``master`` 分支会自己调用 ``source`` 分支上的信息。

现在就可以访问 ``joe.github.io`` 来查看你的博客是否部署成功了。

## 3. [写博客](http://octopress.org/docs/blogging/)
网站部署好了，终于可以开始写博客了。

使用命令：
```
rake new_post["First post"]
```
就会自动在 ``source/_posts/`` 目录下生成一个文件名为 ``2015-12-02-first-post.markdown`` 的文件
使用 ``rake new_post`` 的时候，博客标题尽量用英文，然后在编辑的时候将 title 改成中文，这样文件名就会有意义，如果用中文标题，文件名会自动改成汉字拼音。

然后就可以使用喜欢的编辑器去编辑这个文件了：
```
---
layout: post
title: "First post"
date: 2015-12-02 20:47:13 +0800
comments: true
categories: 
---
Hello, Octopress.
```
除了最后一行外，其他的内容是创建博客的时候自动生成的。

写好博客后，就可以发布到自己的 Github Pages 上了：
```
rake generate
rake deploy

git add .
git commit -m "post title"
git push origin source
```

## 4. 待续
{% img ./hitcat.gif %}

```shell One command to push  
rake generate;rake deploy;git add .;git commit -m "post title";git push origin source;
```
