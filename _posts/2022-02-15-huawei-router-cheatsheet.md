---
layout: post
title: 华为网络设备部分命令速查
date: 2022-02-15 13:25
category: 网络
tags: [huawei, cheatsheet, router, switch, ensp]
---

## 关于 eNSP 的一些吐槽

1. VirtualBox 版本必须为 eNSP 安装时提示的对应版本，否则在主程序启动时会有个错误提示，且设备不能正常启动
1. `ping` 命令展示的耗时远比思科模拟器和现实环境要长，原因未知

## 静态路由及默认路由

### 拓扑图

![](/assets/2022/001.png)

### 基础配置与 IP 编址

路由器 R1 配置过程

```
<Huawei>system-view
[Huawei]sysname R1
[R1]interface Serial 0/0/1
[R1-Serial0/0/1]ip address 10.0.12.1 24 
[R1-Serial0/0/1]quit
[R1]interface GigabitEthernet 0/0/0
[R1-GigabitEthernet0/0/0]ip address 10.0.13.1 24 
[R1-GigabitEthernet0/0/0]description This port connect to R3-G0/0/0 
[R1-GigabitEthernet0/0/0]interface loopback 0 
[R1-LoopBack0]ip address 10.0.1.1 24
```

路由器 R2 R3 配置过程略

### 在 R2 上配置静态路由

```
<R2>system-view 
[R2]ip route-static 10.0.13.0 24 10.0.23.3
[R2]ip route-static 10.0.13.0 255.255.255.0 Serial 0/0/1 preference 80 
```

## RIP 的配置

### 拓扑图

![](/assets/2022/002.png)

基础配置与 IP 配置过程略

### 配置 RIPv1

```
[R1]rip 1 
[R1-rip-1]network 10.0.0.0
```

R2 R3 配置过程同上

### RIPv2 协议配置

```
[R1]rip 1 
[R1-rip-1]version 2
```
R2 R3 配置过程同上

### RIPv2 静态路由引入配置

R3 配置 Loopback 接口

```
[R3]interface LoopBack 1 
[R3-LoopBack1]ip address 172.16.3.3 24 
```

此时 R1 没有去往 172.16.3.3 的路由，所以无法通讯

在 R2 上配置静态路由

```
<R2>system-view 
[R2]ip route-static 172.16.3.0 24 10.0.23.3 
```

将静态路由引入 RIPv2 路由协议

```
[R2]rip 1 
[R2-rip-1]import-route static
```

## 速查表

### 华为路由器各路由协议的默认优先级

| 路由协议或路由种类 | 优先级 |
| ------------------ | ------ |
| Direct             | 0      |
| OSPF               | 10     |
| IS-IS              | 15     |
| Static             | 60     |
| RIP                | 100    |
| OSPF ASE           | 150    |
| BGPD               | 255    |

注：优先级数字越小，优先级越高