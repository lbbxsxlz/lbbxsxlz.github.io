---
layout: post
title:  "How to build Docker images "
comments: true
categories: docker
date:   2020-09-22 21:30:54
---
 
## 拉取 ubuntu 16.04 镜像
```
docker pull ubuntu：16.04
```
# 镜像搜索
```
docker search ubuntu
```
搜索特定的镜像，然后根据搜索结果拉取镜像
```
docker search puppet
docker pull puppet/puppetserver  
```
## 登录docker hub
```
docker login
```
查看认证信息
```
cat ~/.docker/config.json 
```
{<br>
        "auths": {<br>
                "https://index.docker.io/v1/": {<br>
                        "auth": "bGJieHN4bHo6bGJieHN4bHpAMTk4OA=="<br>
                }<br>
        },<br>
        "HttpHeaders": {<br>
                "User-Agent": "Docker-Client/19.03.12 (linux)"<br>
        }<br>
}<br>

## 提交docker镜像,创建镜像
```
docker commit -m "ubuntu with vim" -a "lbbxsxlz" c63f528d0732 lbbxsxlz/ubuntu-vim
```
查看提交的镜像信息
```
docker inspect lbbxsxlz/ubuntu-vim:latest
```
从提交的镜像运行新的容器
```
docker run -i -t lbbxsxlz/ubuntu-vim /bin/bash
```		
## 使用docker file构建镜像
e.p. Dockerfile内容详见此处[here](https://github.com/lbbxsxlz/Docker-Practice/blob/master/Dockerfile)	
```
docker build -t "lbbxsxlz/ubuntu_16.04" . 
docker build -t "lbbxsxlz/ubuntu_16.04" git@github.com:lbbxsxlz/Docker-Practic
```
上文的github仓库路径和"." 路径下里必须包含Dockerfile，不然会报错
## 从新构建的镜像运行容器
```
docker run -d -p 80 --name ubuntu_16.04_nginx lbbxsxlz/ubuntu_16.04 nginx -g "daemon off;"
docker run -d -p 127.0.0.1:32768:80 --name ubuntu_16.04_nginx lbbxsxlz/ubuntu_16.04 nginx -g "daemon off;"
docker run -d -p 127.0.0.1::80 --name ubuntu_16.04_nginx lbbxsxlz/ubuntu_16.04 nginx -g "daemon off;"
docker run -d -P --name ubuntu_16.04_nginx lbbxsxlz/ubuntu_16.04 nginx -g "daemon off;"
```
-P选项表示 对外公开在Dockerfile中通过EXPOSE指令公开的端口
## 查看容器与宿主机端口
```
docker ps -l
```
或
```
docker port 0650f4608e88
docker port `docker ps -l -q`
```
## 访问容器web服务
```
curl 127.0.0.1:32768
```
## 推送镜像到 docker Hub
```
docker push lbbxsxlz/ubuntu_16.04
```
## 删除镜像
```
docker rmi lbbxsxlz/ubuntu_16.04_nginx 
```
## 构建自己的registry
```
docker run -p 5000:5000 registry:2
```
## 给镜像打tag
```
docker tag 4e2eef94cd6b lbbxsxlz-XPS-8930:5000/lbbxsxlz/ubuntu_20.04
```
## 推送镜像到新的registry
```
docker push lbbxsxlz-XPS-8930:5000/lbbxsxlz/ubuntu_20.04
```
## 从新的registry里的镜像启动容器
```
docker run -t -i lbbxsxlz-XPS-8930:5000/lbbxsxlz/ubuntu_20.04 /bin/bash
```
