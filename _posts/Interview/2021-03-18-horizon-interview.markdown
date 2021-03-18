---
layout: post
title:  "地平线面试复盘"
comments: true
categories: Interview
date:   2021-03-18 20:43:07
---

&ensp;&ensp;&ensp;&ensp;2021-3-18号第一轮面试。

## 项目相关
* 安全启动
* 可信环境
* 固件包加密
* 密钥存储
* 大华shell
* 分段升级
* SD卡读写异常
* 网络隧道
* 并发打包

## 知识的深度与广度
* 虚拟地址到物理地址的映射
* 内存分配，_get_free_pages kmalloc vmalloc的内存从哪来
* 内核中断处理过程
* 内核中断下半部机制
* tasklet是什么？
* 中断工作队列机制
* GIC SPI PPI 中断
* 信号量与完成量
* mutex与spinlock   spinockirqsave(解决死锁问题 会关中断)
* irq 与fiq 区别  armv7  armv8
* 中断与CPU绑定    中断号 设置到CPU的亲和力上
* cache 与 TLB


## 总结
整个面试流程较长，不少问题问得挺深入的，需要进一步复习。