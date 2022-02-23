---
layout: post
title: 华为网络设备部分命令速查
date: 2022-02-15 13:25
category: 网络
tags: [huawei, cheatsheet, router, switch, ensp]
---


## 关于 eNSP 的一些吐槽

1. VirtualBox 版本必须为 eNSP 安装时提示的对应版本，否则在主程序启动时会有个错误提示，且设备不能正常启动
1. `ping` 命令展示的耗时远比思科模拟器或现实环境要长，原因未知

<!-- more -->

# 静态路由及默认路由

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

# RIP 的配置

## RIPv1 和 v2 配置

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

## RIPv2 路由汇总和认证

### 拓扑图

![](/assets/2022/003.png)

基础配置与 IP 配置过程略

### 配置 RIPv2

在 R1 R2 R3 上配置路由协议 RIPv2

```
[R3]rip 1 
[R3-rip-1]network 172.16.0.0 
[R3-rip-1]network 10.0.0.0 
[R3-rip-1]version 2 
```

### 在 R2 上配置 RIP 手动路由汇总

```
[R2]interface serial 0/0/1 
[R2-Serial0/0/1]rip summary-address 172.16.0.0 255.255.0.0 
```

对比执行前后 R1 的路由表变化

### 配置路由认证

#### 明文认证

设置认证密码为 `password`

```
[R1]interface serial 0/0/1 
[R1-Serial0/0/1]rip authentication-mode simple password
```

R2 操作同上

#### MD5 认证

设置认证密码为 `password`

```
[R2]interface serial 0/0/2 
[R2-Serial0/0/2]rip authentication-mode md5 usual password
```

R3 操作同上

# OSPF 的配置

## OSPF 单区域配置

### 拓扑图

![](/assets/2022/004.png)

基础配置与 IP 配置过程略

### OSPF 配置

定义 R1 的 Loopback0 接口地址 `10.0.1.1` 作为 R1 的 Router ID
，使用默认的 OSPF 进程号 `1`，将 `10.0.12.0/24`、`10.0.13.0/24` 和 `10.0.1.0/24` 三个网段定义到 OSPF 区域 0

```
[R1]ospf 1 router-id 10.0.1.1 
[R1-ospf-1]area 0 
[R1-ospf-1-area-0.0.0.0]network 10.0.1.0 0.0.0.255 
[R1-ospf-1-area-0.0.0.0]network 10.0.13.0 0.0.0.255 
[R1-ospf-1-area-0.0.0.0]network 10.0.12.0 0.0.0.255 
```

同一个路由器可以开启多个 OSPF 进程，由于进程号只具有本地意义，所以同一路由域的不同路由器可以使用相同或不同的 OSPF 进程号

注意 `network` 命令后面需要使用反掩码

### 查看 OSPF 相关信息命令

查看通过 OSPF 学到的路由

`display ip routing-table protocol ospf`

查看 OSPF 邻居状态

`display ospf peer`

以更简洁的方式查看

`display ospf peer brief`

### OSPF Hello 和 Dead 时间参数修改

两端网络的 Hello Time 和 Dead Time 不一致会导致 OSPF 邻居建立失败

### OSPF 缺省路由发布及验证

在 R3 上配置默认路由并发布到 OSPF 域内

```
[R3]ip route-static 0.0.0.0 0 LoopBack 2 
[R3]ospf 1 
[R3-ospf-1]default-route-advertise 
```


### OSPF DR/BDR 选举控制

### 问题

#### 三个路由器均配置有环回接口，掩码定义为 24 位。为什么环回口连接的网络被其他路由器学习到之后，会显示对应的路由掩码为 32 位？

Loopbacks are considered host routes in OSPF, and they are advertised as /32. For more information, see section 9.1 of RFC 2328 .

## OSPF 多区域、认证配置

### 拓扑图

![](/assets/2022/005.png)

基础配置与 IP 配置过程略

### OSPF 多区域配置

R1 为 ABR（Area Border Router），`10.0.12.0/24` 网段属于区域 0，`10.0.13.0/24` 与 `10.0.1.0/24` 网段属于区域 1

```
[R1]ospf 1 router-id 10.0.1.1 
[R1-ospf-1]area 0 
[R1-ospf-1-area-0.0.0.0]network 10.0.12.0 0.0.0.255 
[R1-ospf-1-area-0.0.0.0]quit 
[R1-ospf-1]area 1 
[R1-ospf-1-area-0.0.0.1]network 10.0.13.0 0.0.0.255 
[R1-ospf-1-area-0.0.0.1]network 10.0.1.0 0.0.0.255 
```

R2 是骨干区域普通内部路由器，属于区域 0

```
[R2]ospf 1 router-id 10.0.2.2 
[R2-ospf-1]area 0 
[R2-ospf-1-area-0.0.0.0]network 10.0.12.0 0.0.0.255 
[R2-ospf-1-area-0.0.0.0]network 10.0.2.0 0.0.0.255 
```

R3 是 ASBR（Autonomous System Boundary Router），`10.0.13.0/24` 和 `10.0.3.0/24` 两个网段属于区域 1，`172.16.0.0/24` 网段不属于 OSPF 路由域，不用通告 OSPF 进程

```
[R3]ospf 1 router-id 10.0.3.3 
[R3-ospf-1]area 1 
[R3-ospf-1-area-0.0.0.1]network 10.0.3.0 0.0.0.255 
[R3-ospf-1-area-0.0.0.1]network 10.0.13.0 0.0.0.255 
```

### OSPF 外部路由引入

在 R3 上使用 `import-route` 命令引入直连外部路由

```
[R3]ospf 1 
[R3-ospf-1]import-route direct 
```

### OSPF 认证配置

#### 明文认证

将 R1 接口 S0/0/1 配置为 OSPF 接口认证模式，明文，密码为 `password`

```
[R1]interface Serial 0/0/1 
[R1-Serial0/0/1]ospf authentication-mode simple plain password
```

R2 同样配置完认证后，可重新与 R1 建立邻居

#### MD5 认证

将 R1 的区域 1 配置为 OSPF 区域认证模式，加密方式为 MD5，密码为明文形式 `password`

```
[R1]ospf 1 
[R1-ospf-1]area 1 
[R1-ospf-1-area-0.0.0.1]authentication-mode md5 1 cipher password
```

R3 同样配置完认证后，可重新与 R1 建立邻居

# RIP、OSPF 相互引入路由

## RIP、OSPF 相互引入路由

### 拓扑图

![](/assets/2022/006.png)

基础配置与 IP 配置过程略

### OSPF 协议配置

```
[R1]ospf 1 router-id 10.0.1.1 
[R1-ospf-1]area 0 
[R1-ospf-1-area-0.0.0.0]network 10.0.12.0 0.0.0.255 
```

```
[R2]ospf 1 router-id 10.0.2.2 
[R2-ospf-1]area 0 
[R2-ospf-1-area-0.0.0.0]network 10.0.12.0 0.0.0.255 
[R2-ospf-1-area-0.0.0.0]network 10.0.2.0 0.0.0.255
```

### RIPv2 协议配置

```
[R1]rip 1 
[R1-rip-1]version 2 
[R1-rip-1]network 10.0.0.0 
```

```
[R3]rip 1 
[R3-rip-1]version 2 
[R3-rip-1]network 10.0.0.0 
[R3-rip-1]network 172.16.0.0 
```

### RIPv2 和 OSPF 协议相互引入配置

到目前为止，R2 和 R3 未学习到对方的路由信息，原因是它们不在同一种路由区域

在 R1 上将 RIP 学到的路由引入到 OSPF 路由表中

```
[R1]ospf 1 
[R1-ospf-1]import-route rip 1 cost 100 
```

在 R1 上将 OSPF 路由引入到 RIP 路由域

```
[R1]rip 1 
[R1-rip-1]import-route ospf 1 cost 1 
```

### （可选）在 R3 上配置 RIP 手动路由汇总

```
[R3]interface GigabitEthernet 0/0/0
[R3-GigabitEthernet0/0/0]rip summary-address 172.16.0.0 255.255.252.0
```

验证 R1 和 R2 的路由表

# 以太网及生成树协议

## 以太网接口及链路配置

### 拓扑图

![](/assets/2022/007.png)

### 基本配置

```
<Huawei>system-view
[Huawei]sysname S1
```

取消自动协商，手动设定速率和全双工模式

```
[S1]interface GigabitEthernet 0/0/9 
[S1-GigabitEthernet0/0/9]undo negotiation auto 
[S1-GigabitEthernet0/0/9]speed 100 
[S1-GigabitEthernet0/0/9]duplex full
```

接口 0/0/10 和 S2 配置同理

### 配置手动链路聚合

在 S1 上创建 Eth-trunk-1，并将接口 0/0/9 加入到 Eth-trunk-1 中

```
[S1]interface Eth-Trunk 1 
[S1-Eth-Trunk1]quit 
[S1]interface GigabitEthernet 0/0/9 
[S1-GigabitEthernet0/0/9]eth-trunk 1 
```

接口 0/0/10 和 S2 配置同理

查看配置结果

```
[S1]display eth-trunk 1
```

## STP 配置

### 拓扑图

![](/assets/2022/008.png)

### STP 配置

在 S1 上

```
<Huawei>system-view 
[Huawei]sysname S1 
[S1]stp mode stp 
[S1]stp root secondary 
```

在 S2 上

```
[S2]stp mode stp 
[S2]stp root primary
```

在 S3 上

```
[S3]stp mode stp
```

S4 同上

使用 `display stp brief` 查看各接口简要 STP 状态

使用形如 `display stp interface GigabitEthernet 0/0/9` 查看特定接口详细 STP 状态

### 控制根桥选举

定义优先级

```
[S1]undo stp root 
[S1]stp priority 4096 
[S2]undo stp root 
[S2]stp priority 8192 
```

再使用 `display stp` 命令可以看出 S1 成了新的根桥

此时如果关闭 S1 的 G0/0/9、G0/0/10、G0/0/13、G0/0/14 四个接口，隔离 S1，那么 S2 就会由备份根桥变成新的根桥

开启 S1 之前关闭的接口，S1 会被重新选举成为根桥

### 根端口选举控制

端口优先级默认值为 128，可以通过以下命令设置

```
[S1]interface GigabitEthernet 0/0/9 
[S1-GigabitEthernet0/0/9]stp port priority 32
```

在 S2 上使用 `display stp brief` 可以看到 S2 的 `G0/0/10` 被选举成了新的根端口，`G0/0/9` 成为了替代端口

此时关闭 S2 上的根端口 G0/0/10，G0/0/9 就会被选举成为新的根端口


### 边缘端口配置

将连接用户终端设备的端口配置成边缘端口，可以使该端口无需经历 STP 计算过程快速进入转发状态

```
[S3]interface GigabitEthernet 0/0/3
[S3-GigabitEthernet0/0/3]stp edged-port enable
```

配置完成后，计算机网线接入到 S3 的接口 G0/0/3 上，可以看到 G0/0/3 端口状态变成了 Forwarding 状态，连接到其他没有配置到边缘端口的端口后，则要等待约 30 秒才能到达 Forwarding 状态

## VLAN 配置

### 拓扑图

![](/assets/2022/009.png)

### Eth-trunk 链路聚合

在 S1 和 S2 之间有两条链路，如果开启 STP 则会有一条链路被禁用，造成带宽浪费；如果不使用 STP 则会造成环路；这种情况下，使用链路聚合，可以很好解决这个问题

S1 和 S2 采用两种方式配置，结果相同

```
[S1]interface gigabitethernet0/0/9 
[S1-GigabitEthernet0/0/9]eth-trunk 1 
[S1-GigabitEthernet0/0/9]quit
[S1]interface gigabitethernet0/0/10 
[S1-GigabitEthernet0/0/10]eth-trunk 1 
```

```
[S2]interface eth-trunk 1 
[S2-Eth-Trunk1]trunkport GigabitEthernet 0/0/9 
[S2-Eth-Trunk1]trunkport GigabitEthernet 0/0/10
```

接口默认的链路类型为 Hybird 类型，可以修改链路类型为 Trunk 类型

默认情况下，接口的 Trunk 功能禁止所有的 VLAN 数据传输过去

```
[S1]interface Eth-Trunk 1 
[S1-Eth-Trunk1]port link-type trunk 
[S1-Eth-Trunk1]port trunk allow-pass vlan all 
```

S2 配置同上

### 配置 VLAN

下面展示配置号码连续的多个 VLAN 的两种方式和定义 VLAN 与接口的对应关系的两种方式

```
[S1]interface GigabitEthernet0/0/13 
[S1-GigabitEthernet0/0/13]port link-type access 
[S1-GigabitEthernet0/0/13]quit
[S1]interface GigabitEthernet0/0/1 
[S1-GigabitEthernet0/0/1]port link-type access 
[S1-GigabitEthernet0/0/1]quit
[S1]vlan 3 
[S1-vlan3]port GigabitEthernet0/0/13 
[S1-vlan3]quit
[S1]vlan 4 
[S1-vlan4]port GigabitEthernet0/0/1 
[S1-vlan4]quit
[S1]vlan 5
```

```
[S2]vlan batch 3 to 5 
[S2]interface GigabitEthernet 0/0/3 
[S2-GigabitEthernet0/0/3]port link-type access 
[S2-GigabitEthernet0/0/3]port default vlan 4 
[S2-GigabitEthernet0/0/3]quit
[S2]interface GigabitEthernet 0/0/24 
[S2-GigabitEthernet0/0/24]port link-type access 
[S2-GigabitEthernet0/0/24]port default vlan 5 
```

### 规划地址

R1、R3、S3、S4 模拟为客户端，测试 VLAN 配置效果

交换机物理接口无法配置地址，在 VLANIF1 接口配置 IP 地址

```
[S3]interface vlanif 1 
[S3-vlanif1]ip address 10.0.3.3 24
```

S4 配置过程类似，R1、R3 配置过程略

### 掌握 Hybird 接口的配置

Hybird 接口与 Trunk 接口类似，但是增加了一些功能，可以实现在不同 VLAN 的用户通讯

修改 S3 与 R3 地址

```
[S3]interface Vlanif 1 
[S3-Vlanif1]ip address 10.0.6.3 24

[R3]interface GigabitEthernet 0/0/2 
[R3-GigabitEthernet0/0/2]ip address 10.0.6.4 24 
```

定义 S1 的 G0/0/13 接口为 Hybird 接口，属于 VLAN3。对 VLAN3 和 VLAN4 定义为 Untagged。注意修改链路类型之前，需要删除接口的额外配置。

```
[S1]interface GigabitEthernet0/0/13 
[S1-GigabitEthernet0/0/13]undo port default vlan 
[S1-GigabitEthernet0/0/13]port link-type hybrid 
[S1-GigabitEthernet0/0/13]port hybrid pvid vlan 3 
[S1-GigabitEthernet0/0/13]port hybrid untagged vlan 3 to 4
```

定义 S2 的 G0/0/3 接口为 Hybird 接口，属于 VLAN4。对 VLAN3 和 VLAN4 定义为 Untagged。

```
[S2]interface GigabitEthernet0/0/3 
[S2-GigabitEthernet0/0/3]undo port default vlan 
[S2-GigabitEthernet0/0/3]port link-type hybrid 
[S2-GigabitEthernet0/0/3]port hybrid pvid vlan 4 
[S2-GigabitEthernet0/0/3]port hybrid untagged vlan 3 to 4 
```

此时 S3 与 R3 虽然在不同网段，但是可以实现互通

```
[S3]ping 10.0.6.4
```




# 附录

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
| BGP                | 255    |

注：优先级数字越小，优先级越高

## 名词解释

### STP

- IEEE 802.1D 中定义的 STP（Spanning Tree Protocol）
- IEEE 802.1W 中定义的快速生成树协议 RSTP（Rapid Spanning Tree Protocol）
- IEEE 802.1S中定义的多生成树协议MSTP（Multiple Spanning Tree Protocol）