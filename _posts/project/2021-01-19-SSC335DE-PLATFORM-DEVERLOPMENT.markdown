---
layout: post
title:  "SSC335DE deverlopment"
date:   2021-01-19 20:14:54
categories: Project
comments: true
---
*** SSC335DE平台开发记录 ***

## U-Boot
1、根据厂家提供的偏移地址制作引导程序<br>
2、在uboot-2010基础上添加代码，包括Makefile的改动<br>
3、调试网络与存储介质驱动<br>
4、更改头文件中的配置，例如系统启动地址、分区地址、启动参数等<br>

## Kernel
1、根据厂家提供的配置文件修改制作产品相符配置文件<br>
2、修改dts文件，添加默认分区信息<br>
3、依据需要添加相关的内核配置，例如NFS、CIFS<br>

## 根文件系统
1、busybox中添加挂载所需的命令<br>
2、修改启动脚本<br>
3、修改相关命令的软链接<br>
4、mount命令支持nfs正常挂载需要对应的RPC头文件<br>

## 驱动
1、添加交叉编译器<br>
2、根据产品定义添加功能<br>
3、添加相关的调试功能，例如proc读写接口、debugfs等<br>
4、相关外设的改动，例如内置的RTC的初始化取决于内核中RTC的配置<br>
5、部分外设需要根据厂家提供的管脚复用修改对应的配置

## SD卡
1、内核对应厂商的dts中需要添加检测引脚，检测引脚的配置需要根据实际电路来设置<br>
2、内核中开启厂商对应的SD_MMC配置

## USB
1、需要在usb的core中添加proc文件系统，对应的内核配置为CONFIG_USBDEVICEFS<br>
2、内核配置中开启HCD配置（适配USB2.0）

## wifi
1、设置wifi模块使能引脚，增加相应的配置
2、根据能力加载wifi驱动

