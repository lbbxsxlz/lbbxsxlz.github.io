---
layout: post
title:  "地平线面试复盘"
comments: true
categories: Interview
date:   2021-03-18 20:43:07
---

&ensp;&ensp;&ensp;&ensp;2021-3-18号第一轮视频面试。2021年3月20号，地平线杭州（知识产权大厦）现场面试，一对二，时长近一个半。二面结束之后的第四天联系HR，无回应，至今没有任何回应。

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
  
* 内核内存泄漏检测（kmemleak）
* kernel ramdump
* 内核中断死锁如何检测
* 如何定位性能卡顿问题（举例）

* 在同事心中你是个什么样的人
* 你的缺点是什么


## 总结
一面整个面试时间较长，不少问题问得挺深入的，需要进一步复习。
二面的过程中有套方案之嫌。
作为创业公司，想招揽人才，却给不起钱。
前段时间还爆出过裁应届生员工的大瓜。

