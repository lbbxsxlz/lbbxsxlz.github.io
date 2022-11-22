---
layout: post
title:  "高通面试复盘"
comments: true
categories: Interview
published: false
date:   2022-11-19 20:03:01
---

## 项目相关
* secure boot
* firmware encryption performance
* memory encryption
* attestation and authentication

* secure boot的安全闭环
* RSA 算法原理，私钥和公钥的组成部分  （D，N） （E,N）  
* AES加密算法性能优秀的原因 算法原理 矩阵轮转 + 异或
* 数字签名 数字证书，证书的组成
* (ATF)Trustzone NSbit   AXI bus 
* TZMA 内存划分
* keymaster   gatekeeper 

## 技术背景
* Linux用户态与内核态区别
* 进程状态
* TEE/OpenTEE

## 笔试题
链表反转
程序阅读

## 程序设计
1/2 + 1/3  同单位
strncpy 设计实现，参数(src, dst, srclen, dstlen)，内存重叠，入参检查
测试覆盖，边界检查, 中间值
gcc -w disable warning
函数未声明，会默认使用int返回值
