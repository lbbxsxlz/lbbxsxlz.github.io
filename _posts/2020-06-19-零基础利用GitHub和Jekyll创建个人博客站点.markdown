---
layout: post
title:  "零基础利用Github和jekyll创建个人博客站点"
date:   2020-06-19 20:58:54
categories: jekyll
comments: true
---
## 前言
&ensp;&ensp;&ensp;&ensp;若干年前，还在读书那会，QQ空间是最流行的个人站点，不管主流还是非主流，都有装饰一番的欲望，朋友之间还会互踩，作为文学爱好者的我基本上每周都写一篇日志。
而工作之后，QQ基本被微信所替代，人也懒了，也逐渐没有了倾述的欲望。

&ensp;&ensp;&ensp;&ensp;此番提起兴致利用github创建个人博客，一是想践行一个短期的计划，另外也是为了能在心血来潮之时能有个地方记录一二。

## 创建blog工程
&ensp;&ensp;&ensp;&ensp;在github的首页点击New repository,在跳出的页面上填写blog的域名与相关描述，如下  
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

## 静态网页
&ensp;&ensp;&ensp;&ensp;在基于github的blog工程上发布或修改新的文章，想要看效果，就必须先把修改提交，然后访问相应的网页查看。这样的操作未免太繁琐，幸好[jekyll](https://jekyllrb.com/)就提供了静态网页的功能。
jekyll基于ruby，即得先安装ruby, 一定要[下载](https://rubyinstaller.org/downloads/)WITH DEVKIT版本，不然后续就有苦吃了，笔者在此入了坑。安装完之后，在dos窗口输入ruby -y，有输出即表述安装成功。
去RubyGems的[官方](https://rubygems.org/pages/download)网站下载zip格式的包，然后解压，在dos命令行中进入到rubygem的解压目录下，执行ruby setup.rb，其安装过程大致如下<br>，
![setup.rb](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/14.png)  

安装完毕之后就可以使用gem install jekyll命令安装jekyll,<br>
![jekyll](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/15.png)

安装jekyll之后，就可以创建静态网页工程，例如使用jekyll new fblog创建第一个博客工程，<br>
![fBlog](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/16.png)

然后使用jekyll server即可启动静态网页，使用127.0.0.1：4000端口即可访问，4000端口是jekyll的默认端口。<br>
![server](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/17.png)
