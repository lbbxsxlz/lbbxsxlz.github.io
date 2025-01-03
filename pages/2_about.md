---
layout: page
title: about
comments: true
permalink: /about/
---

* content
{:toc}

## 关于这个网站
这个网站使用github和jekyll创建。仅用来记录个人的一些技术心得与人生体会。

## 关于我

![me](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/about/me.png)

从事软件行业，存粹是因缘际会，目前算是一个合格的程序员吧。热爱动漫，是海贼王的忠实粉丝。

## 工作经历
    ---
    *** 英特尔亚太研发有限公司 ***
        Pooled Memory SOC and Support CXL Dynamic Capacity Device(DCD)
            Fabric Manager CXL DCD集成，处理HOST的内存请求，DPA管理
            BMC Daemon与其他组件交互，CCI command处理，RESTful API交互
            Pooled Memory SOC\BMC\HOST使用RPC，Redfish完成注册与电源管理
            Pooled Memory SOC与BMC\HOST之间的Device Attestation
            Pooled Memory SOC Power On期间的疑难杂症(Crash, Hang)解决
        SOC安全设计、评估、验证;IP Authentication and Attestation
            Device Identifier Composition Engine（DICE）
            Security Protocol and Data Model (SPDM)
            Memory Security Engine(Mutli-Key Total Memory Encryption)
        Dbus service development
            SMBIOS over PLDM
            PLDM over MCTP
        RISC-V Privileged Architecture and Virtualization
        ARM CCA(RME) vs. Intel TDX/TDX-IO

    *** 浙江大华技术股份有限公司 ***
        方向一：设备安全与设备溯源
            uBoot多级安全启动，kernel验证启动；Kernel、根文件系统、应用程序固件加解密。
            类似TRUST Zone的设备可信执行环境；设备RSA签名验证升级，密钥统一管理与分发。
            Boot下与用户态的OTP接口，用于防窜货与源回溯。安全漏洞修复工具。
        方向二：性能分析与工具开发
            core文件实时压缩工具，保证core文件与APP之间的对应关系，core文件分区整理。
            栈回溯工具，匹配ARM架构的栈回溯接口，周期性获取与筛选内核信息。
            重构程序打包流程，优化程序中squashfs文件系统制作。设备启动时间优化。
            应用程序升级方案优化，差分升级实现，小内存安全升级方案实现。
        方向三：驱动开发与维护
            以太网FlowControl、NAT、VLAN、mode and duplex AutoChange、IP search
            4G、5G、WiFi、SD Card; 双4G NAT实时切换 TUN/TAP虚拟网卡

    *** 锐捷网络有限公司 ***
        工作一：基于本地虚拟化的云办公系统开发
            工作系统镜像libvirt快照，秒级创建系统，一分钟还原系统
            可移动存储设备块级加密，USB设备插拔监控
            用户网路访问信息采集与网络白名单
        工作二：基于VDI虚拟化桌面上的教学管理软件开发
            X视窗的桌面截取、H264编码与鼠标绘制
            视频流硬解码与渲染，分辨率自适应
    ---

## 联系我
- [github](https://github.com/lbbxsxlz)
- email:lbbxsxlz@gmail.com binbinlz@163.com
