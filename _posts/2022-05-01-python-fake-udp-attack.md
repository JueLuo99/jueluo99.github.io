---
layout: post
title: 使用 Python 构造一个伪装来源的 UDP 攻击
date: 2022-05-01 03:19
category: 
author: 
tags: []
summary: 
---

## 获取方式

```bash
wget https://raw.githubusercontent.com/JueLuo99/network-tools/master/fake_udp_attack.py

# 或者使用下面这个地址
wget https://git.jueluo.tech/jueluo/network-tools/raw/branch/master/fake_udp_attack.py
```

## 环境需求

- Linux 需要 root 权限（Windows未知）
- Python 3.6+
- 安装 `scapy` 库：`sudo pip3 install scapy`

## 使用方式

```bash
sudo python3 fake_udp_attack.py <source_ip> <source_port> <dest_ip> <dest_port> <payload>
```

### 举个例子

发送端：

```bash
$ sudo python3 fake_udp_attack.py 8.8.8.8 8888 192.168.2.15 4567 Hello
.
Sent 1 packets.
```

接收端：
```bash
$ sudo nc -luvvp 4567
Listening on [0.0.0.0] (family 2, port 4567)
Connection from dns.google 8888 received!
Hello
```

可见成功伪装成 Google DNS 的地址发送了一个 UDP 报文，并且接收端收到了这个报文。

## 注意事项

该功能可能会因 NAT 技术等原因在公网上工作不正确，亦可能直接被网关丢弃