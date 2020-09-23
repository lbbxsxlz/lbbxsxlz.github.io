---
layout: post
title:  "hello docker"
comments: true
categories: docker
date:   2020-09-12 20:10:54
---

## ubuntu 16.04 docker 安装
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker info
```
## 卸载docker
```
sudo apt-get purge docker-ce docker-ce-cli containerd.io
sudo rm -rf /var/lib/docker
```
## 添加lbbxsxlz用户到docker用户组
```
sudo groupadd docker
sudo usermod -aG docker lbbxsxlz
```
## docker运行
```
docker run --name lbbxsxlz_docker_test -i -t ubuntu /bin/bash
docker start lbbxsxlz_docker_test ; docker attach lbbxsxlz_docker_test
```
## docker停止运行
```
docker stop lbbxsxlz_docker_test
docker kill cf8027c5ffbb
```
## 后台运行
```
docker run --name lbbxsxlz_docker_test_daemon -d ubuntu /bin/sh -c "while true; do echo hello world;sleep 1;done"
```
## 显示容器信息
```
docker ps -a
```
显示最近$x个容器
``` 
docker ps -n $x
```
显示容器的ID
```
docker ps -a -q
```

## 容器内日志获取
```
docker logs lbbxsxlz_docker_test_daemon
docker logs --tail 0 -ft lbbxsxlz_docker_test_daemon
```
## 查看容器内进程
```
docker top lbbxsxlz_docker_test_daemon
```
## 查看容器运行情况
```
docker stats
```
## 容器运行后台任务
```
docker exec -d lbbxsxlz_docker_test touch /lbbxsxlz_test
docker exec -t -i  lbbxsxlz_docker_test /bin/bash
```
## 查看容器详细信息
```
docker inspect lbbxsxlz_docker_test
docker inspect lbbxsxlz_docker_test --format='{{.Id}}'
docker inspect lbbxsxlz_docker_test --format='{{.NetworkSettings.Networks.bridge}}'
docker inspect --format '{{.Id}} {{.Name}}' lbbxsxlz_docker_test
```
## 容器删除 
```
docker rm $id/$name
```
删除运行中的容器
```
docker rm -f $id
```
删除所有的容器
```
docker rm `docker ps -a -q`
```
