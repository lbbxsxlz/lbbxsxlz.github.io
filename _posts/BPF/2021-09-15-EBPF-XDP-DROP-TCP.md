---
layout: post
title:  "使用EBPF验证XDP丢弃TCP报文"
comments: true
categories: BPF
date:   2021-09-15 15:52:54
---

## 验证丢弃TCP报文
按照惯例先上代码：
```
#include <uapi/linux/bpf.h>
#include <linux/if_ether.h>
#include <linux/ip.h>
#include <linux/in.h>

typedef unsigned short u16;
typedef unsigned int u32;
typedef unsigned long long u64;

#define htons(x) __cpu_to_be16(x)

#define SEC(NAME) __attribute__((section(NAME), used))


static int handle_ipv4(void *data, u64 nh_off, void *data_end)
{
    struct iphdr *iph = data + nh_off;

    if ((void *)(iph + 1) > data_end)
         return XDP_DROP;

    if (IPPROTO_TCP == iph->protocol)
                return XDP_DROP;

        return XDP_PASS;
}

SEC("xdp-tcp")

int xdp_drop_tcp(struct xdp_md *ctx) {
    void *data_end = (void *)(long)ctx->data_end;
    void *data = (void *)(long)ctx->data;
    struct ethhdr *eth = data;

    u16 h_proto;
    u64 nh_off;

    nh_off = sizeof(*eth);
    if (data + nh_off > data_end)
        return XDP_DROP;

    h_proto = eth->h_proto;

    if (h_proto == htons(ETH_P_IP)) 
        return handle_ipv4(data, nh_off, data_end);

    return XDP_PASS;
}

char _license[] SEC("license") = "GPL";
```

我们使用容器来验证，先启动容器
```
docker build -t lbbxsxlz/nginx .
docker run -d -p 80 --name firstWeb -v $PWD/html:/var/www/html lbbxsxlz/nginx nginx
```
Dockerfile以及相关依赖见项目[Docker-Practice](https://github.com/lbbxsxlz/Docker-Practice/tree/master/firstWebTest)
```
docker ps -a
```

	CONTAINER ID   IMAGE            COMMAND   CREATED          STATUS          PORTS                                     NAMES
	71fae414918b   lbbxsxlz/nginx   "nginx"   11 seconds ago   Up 10 seconds   0.0.0.0:49153->80/tcp, :::49153->80/tcp   firstWeb

使用curl访问，
```
curl 127.0.0.1:49153
```

	<head>

	<title>Test website</title>

	</head>

	<body>

	<h1>This is a test website for docker!</h1>

	<h2> html testing  </h2>

	</body>

屏蔽tcp报文
```
sudo ip link set dev vetha17714e xdp obj xdp-drop-tcp.o sec xdp-tcp verbose
```

	Prog section 'xdp-tcp' loaded (5)!
	 - Type:         6
	 - Instructions: 21 (0 over limit)
	 - License:      GPL

	Verifier analysis:

	0: (b7) r0 = 1
	1: (61) r2 = *(u32 *)(r1 +4)
	2: (61) r1 = *(u32 *)(r1 +0)
	3: (bf) r3 = r1
	4: (07) r3 += 14
	5: (2d) if r3 > r2 goto pc+14
	 R0=inv1 R1=pkt(id=0,off=0,r=14,imm=0) R2=pkt_end(id=0,off=0,imm=0) R3=pkt(id=0,off=14,r=14,imm=0) R10=fp0
	6: (71) r3 = *(u8 *)(r1 +12)
	7: (71) r4 = *(u8 *)(r1 +13)
	8: (67) r4 <<= 8
	9: (4f) r4 |= r3
	10: (b7) r0 = 2
	11: (55) if r4 != 0x8 goto pc+8
	 R0=inv2 R1=pkt(id=0,off=0,r=14,imm=0) R2=pkt_end(id=0,off=0,imm=0) R3=inv(id=0,umax_value=255,var_off=(0x0; 0xff)) R4=inv8 R10=fp0
	12: (bf) r3 = r1
	13: (07) r3 += 34
	14: (b7) r0 = 1
	15: (2d) if r3 > r2 goto pc+4
	 R0=inv1 R1=pkt(id=0,off=0,r=34,imm=0) R2=pkt_end(id=0,off=0,imm=0) R3=pkt(id=0,off=34,r=34,imm=0) R4=inv8 R10=fp0
	16: (71) r1 = *(u8 *)(r1 +23)
	17: (b7) r0 = 1
	18: (15) if r1 == 0x6 goto pc+1
	 R0=inv1 R1=inv(id=0,umax_value=255,var_off=(0x0; 0xff)) R2=pkt_end(id=0,off=0,imm=0) R3=pkt(id=0,off=34,r=34,imm=0) R4=inv8 R10=fp0
	19: (b7) r0 = 2
	20: (95) exit

	from 18 to 20: R0=inv1 R1=inv6 R2=pkt_end(id=0,off=0,imm=0) R3=pkt(id=0,off=34,r=34,imm=0) R4=inv8 R10=fp0
	20: (95) exit

	from 15 to 20: safe

	from 11 to 20: safe

	from 5 to 20: safe
	processed 25 insns, stack depth 0

此时，使用curl命令访问，curl 127.0.0.1:49153 / curl 172.17.0.2:80 卡住无输出

使用命令
```
sudo ip link set dev vetha17714e xdp off
```
后恢复，即可正常访问

注：获取容器网卡与ip见上一篇文章中的描述

