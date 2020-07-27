---
layout: post
title:  "阿里云面试复盘"
comments: true
categories: Interview
date:   2020-07-27 20:30:07
---

&ensp;&ensp;&ensp;&ensp;从2020年三月中旬开始面试阿里云混合云全栈研发专家/架构师岗位，共经历五轮面试，耗时一个月，于四月中旬走完HR面。五十多天后被告知职业经历与职位要求略有差异而被拒。

## 自我介绍
&ensp;&ensp;&ensp;&ensp;每次的自我介绍都差不多，这是个严重的问题。需要根据面试官的职位特征，有针对性的删减与突出。

## 项目有关问题
* core文件实时压缩工具的实现背景与原理
* backtrace工具实现的原理
* 程序打包与发布优化是如何实现的
* 云桌面虚拟化的业务场景是怎样的
* 硬件安全、可信加载的实现原理
* 现在项目中的最大问题是什么，如何优化解决
* 项目中遇到的最大挑战是什么，哪个项目让你最有成就感
* 你现在的工作对阿里云的业务有何贡献

## 价值观
* 什么是成功
* 什么是你不可接受的
* 周边的人是怎么影响你的

## 知识的深度与广度
* ELF的段（section）是否有数量限制
* 形参 是否保存在栈中
* linux 内核是怎么管理内存的
* 有了伙伴算法，为什么还需要slab
* kmalloc与vmalloc的区别
* rpm yum deb包
* shell命令如何调试
* df与du的区别
* ifconfig与ifup的区别
* 自旋锁与互斥量的区别
* free 中的buf与cache区别
* tcp协议的连接状态，什么时候进入TIME_WAIT状态
* uboot启动内核过程
* x86_64的linux服务器panic时如何调试
* crash命令使用细节
* x86架构与arm架构的差别
* 如何设计一个高可用的系统

## 编程相关
判断大端还是小端
```
int IsBigEndian(void)
{
    int short = 0x1234;
    char *ptr = &num;
  
    if (ptr[0] == 0x34)
    {
        return 0;
    }
    else
    {
        return 1;
    }
}
```
memcpy的实现，源地址与目的地址有重叠
```
void * mymemncpy(void* src, void* dst, int len)
{
    if (NULL == dst || NULL == src)
    {
        return NULL;
    }
  
    char* dstTmp = char*(dst);
    char* srcTmp = char*(src);
    int i;
  
    //重叠部分处理
    if (dstTmp > srcTmp && dstTmp < srcTmp + len)
    {
        for (i = len -1; i != -1; --i)
        {
            dstTmp[i] = srcTmp[i];
        }      
    }
    else
    {
        for (i = 0, i < len; i++)
        {
            dstTmp[i] = srcTmp[i]; 
        }
    }
  
    return dst;
}
```
	