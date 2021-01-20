---
layout: post
title:  "SSC335DE deverlopment"
date:   2021-01-19 20:14:54
categories: Project
comments: true
---
*** SSC335DE平台开发 ***

## U-Boot
1、根据厂家提供的偏移地址制作引导程序
2、在uboot-2010基础上添加代码

## Kernel
1、根据厂家提供的配置文件修改制作产品相符配置文件
2、修改dts文件，添加默认分区信息

## 根文件系统
1、busybox中添加挂载所需的命令
2、修改启动脚本

## 驱动
1、添加交叉编译器

