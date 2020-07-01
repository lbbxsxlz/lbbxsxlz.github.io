---
layout: post
title:  "零基础利用Github和jekyll创建个人博客站点"
date:   2020-06-19 20:58:54
categories: jekyll
comments: true
---
## 前言
若干年前，还在读书那会，QQ空间是最流行的个人站点，不管主流还是非主流，都有装饰一番的欲望，朋友之间还会互踩，作为文学爱好者的我基本上每周都写一篇日志。
而工作之后，QQ基本被微信所替代，人也懒了，也逐渐没有了倾述的欲望。

此番提起兴致利用github创建个人博客，一是想践行一个短期的计划，另外也是为了能在心血来潮之时能有个地方记录一二。

## 创建blog工程
在github的首页点击New repository,在跳出的页面上填写blog的域名与相关描述，如下
![blog工程](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/1.png)

在Windows上安装git，点击[下载](https://git-scm.com/downloads)安装，安装完毕之后，右击，可以看到有Git GUI Here和Git Bash Here两个选项，如图，
![git选项](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/2.png)

然后选择Git Bash Here，配置git的用户邮箱与用户名。接着使用使用ssh-keygen工具创建连接github的ssh密钥，整个工程如下，
![git配置](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/3.png)

![ssh-key](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/4.png)

接着右击Git GUI Here，再单击Help菜单下的Show SSH Key,即可显示上一步生成的密钥内容，拷贝密钥内容。
![ssh-key2](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/7.png)

回到github首页，点击头像，然后选择setting，在跳出的页面上选择SSH and GPG Keys。
![setting](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/8.png)
![SSH and GPG](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/9.png)
![keys](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/10.png)

点击NeW SSH Key，将拷贝的key填入Key框中，然后在title框中填入可记忆的标题，然后再点击Add SSH key。
![Addkeys](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/11.png)

再次回到git bash界面，使用命令ssh -T git@github.com测试连接是否正常，测试结果如下。
![ssh -T](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/12.png)

连接正常后，选择存放blog工程的目录，然后git clone加工程路径，下载工程的分支。
![git clone](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/13.png)