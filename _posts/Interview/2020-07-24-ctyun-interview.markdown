---
layout: post
title:  "天翼云面试复盘"
comments: true
categories: Interview
date:   2020-07-24 16:30:00
---

## 自我介绍
自我介绍不够顺畅，没有分清主次，有待练习加强

## 项目有关问题
* usb热插拔是怎么实现的，内核与用户态怎么交互  中断   libusb热插拔callback
* 块设备加密实现  cryptsetup命令 
* 块设备怎么透传到Windows镜像   Libvirt XML disk对象定义 virsh attach挂载到虚拟机镜像中
* 网络白名单实现  iptables
* Windows镜像快照 qemu镜像格式    Qcow2  qemu-img(快照管理 commit rebase) virsh(libvirt命令 快照管理)
* 教师管理软件的使用场景
* core文件压缩实现原理 管道加可执行文件
* core文件文件格式   [ref](https://blog.csdn.net/_xiao/article/details/22389997)
* 可信环境与可信签名实现原理
* ARM trustZone TEE 技术  [ref](https://www.jianshu.com/p/3f952f2c8bf4)
* LSM模块  [ref](https://www.ibm.com/developerworks/cn/linux/l-lsm/part1/index.html)

## 基础知识
* 堆 和 栈
* bss  data  rodata
* shell -e选项  若指令传回值不等于0，则立即退出   shell $@  传入的参数列表
* shell 脚本处理数据  内容替换（例如exe） 排序  去重  sort  uniq

## 编程相关
```
    char* p = "1234"; 
    *p = "abc";
    
    printf("%s", p);
```
以上内容是否有问题，如果有问题怎么修改

strncpy的实现
```
char * strncpy(char* src, char* dst, int len)
{
	if (NULL == dst || NULL == src)
    {
    	return NULL;
    }
  
  	char* dstTmp = dst;
  
  	char* srcTmp = src;
  	int i;
  
	for (i = 0, i < len; i++)
    {
        dstTmp[i] = srcTmp[i]; 
    }

  	return dst;
}
```

## 自我评价
此次面试前未重点准备，从公司匆匆赶回，状态略有不佳。
	