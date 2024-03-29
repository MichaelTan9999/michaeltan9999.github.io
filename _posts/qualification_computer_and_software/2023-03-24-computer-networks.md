---
title: 软考笔记 - 计算机网络
date: 2023-03-24 17:00:00 +0800
categories: 软考
math: true
mermaid: true
---
2022年5月左右的预测。

![2022-May-CN-bullet-points.png](https://s2.loli.net/2023/03/24/WG5aSUZkTOmAl9w.png)

## TCP/IP协议簇

常见的协议和它们的端口号：

- POP3：110，邮件收取
- SMTP：25，邮件发送
- FTP：20数据/21控制，文件传输
- DHCP：67，IP地址分配
- SNMP：161，简单网络管理协议
- DNS：53，域名解析
- ICMP：因特网控制协议
- IGMP：组播协议
- ARP：地址解析协议，IP转MAC
- RARP：反向地址解析协议，MAC转IP

### OSI七层模型的基础两层

在OSI七层模型中，在数据链路层之前，每一层级加报头后给到下一级。数据链路层称数据为帧，会加上帧头和帧尾。在物理层转换为比特进行传输。

OSI物理层以二进制传输，中继器作信号放大的作用，集线器是多端口中继器（集线器的端口接入的信号在同一冲突域）

OSI数据链路层以帧为单位传输，网桥可以直接沟通两台电脑，交换机是多端口网桥

OSI网络层主要功能是分组传输和路由选择，由路由器（三层交换机）沟通不同的冲突域

### DNS服务

递归查询：服务器必须回答目标IP与域名的映射关系。

迭代查询：服务器收到一次迭代查询结果，这个结果可能是IP与域名的关系，也可能是其他DNS服务器的地址。

一般来说本地域名服务器与主机之间的请求，是递归查询。

浏览器输入域名：HOSTS--->本地DNS缓存--->本地DNS服务器--->根域名服务器--->顶级域名服务器--->权限域名服务器

主域名服务器：本地缓存--->区域记录--->转发域名服务器--->根域名服务器

### DHCP

DHCP是C/S模型，同一网络中可以有多个DHCP服务器，它可以管理多个网段。租约过半时，客户机需要向DHCP申请续租；租约过87.5%时，没有和当初提供IP的DHCP服务器联系上的话，则开始联系其他的DHCP服务器。在DHCP服务器上，DHCP服务默认关闭。

分配方式：固定分配（管理员绑定静态的固定IP）、动态分配（租期无限长），自动分配（租期有一定期限）

无效地址：169.254.0.0/16（Windows），0.0.0.0（Linux）

## 网络规划与设计

```mermaid
flowchart LR
需求分析 --> 通信规范分析 --> 逻辑网络设计 --> 物理网络设计 --> 实施阶段
```

### 逻辑网络设计

利用前两个阶段需求分析和现有网络体系分析的产物（需求规范和通信规范），选择适宜的网络逻辑结构，得到一份逻辑网络设计文档。网络设计文档主要包含：

- 逻辑网络设计图
- IP地址方案
- 安全管理方案
- 软硬件（不需要定下型号，只需要知名到交换机or路由器即可）、广域网连接设备和基本的网络服务
- 网管的招聘培训、软硬件和服务的费用估算

### 物理网络设计

物理网络设计是对逻辑网络设计的物理实现，通过对设备的具体物理分布、运行环境等确定，确保网络的物理连接符合逻辑连接的要求。主要包含：

- 物理网络结构图和布线方案
- 设备和部件的详细列表清单
- 详细的预算
- 安装日程表
- 安装后系统测试计划、用户培训计划

### 分层设计

- 核心层（接Internet路由器）：高速数据交换、出口路由，常用冗余机制；
- 汇聚层：访问策略控制、数据包过滤、策略路由、广播域定义、寻址
- 接入层：针对用户端、实现用户接入、计费管理、MAC认证记过滤等，在接入层可以使用集线器代替交换机

## 网络存储技术

几大分类：

- 直连式存储（DAS）：服务器直连存储设备
- 网络附加存储（NAT）：服务器连接到一个管理存储设备的主机
- 存储区域网络（SAN）：存储设备接入大规模网络由一个或多个服务器对外提供服务。分为IPSAN/iSCSI（核心枢纽是IPSAN服务器和以太网交换机）和FC-SAN（核心枢纽是光纤通道交换机）

### Raid的分类

- Raid0（条块化）：性能最高，并行处理，无冗余，损坏无法恢复
- Raid1（镜像结构）：可用性、可修复性好，仅有50%利用率
- Raid1E：至少由三个逻辑盘组成，备份数据均匀贯穿于所有盘中，利用率仍为50%，坏一个盘可恢复
- Raid1ADM，Raid1Triple：每个数据块有两个备份，利用率仅有1/3，用于容错要求高的领域，如财政、金融等
- Raid0+Raid1（Raid10）：两个磁盘都可以读写，但是仍然只有50%的利用率
- Raid3（奇偶校验并行传送）：N+1模式，有固定的校验盘，坏一个盘可恢复，利用率$\frac{N}{N+1}$
- Raid5（分布式奇偶校验的独立磁盘）：N+1模式，一次分布式验证，无固定的校验盘（每个盘都有一部分作校验），坏一个盘可恢复
- Raid6（两种存储的奇偶校验）：N+2模式，两次分布式验证，无固定的校验盘（两个校验盘大小的容量），坏两个盘可恢复
- Raid50：外层Raid0，内层Raid5
- Raid60：外层Raid0，内层Raid6

多个盘不一致的情况下，以最小的磁盘为基准计算存储空间。

## IP协议相关

### IPv6

IPv6的几个特点：

- 寻址能力增强，地址扩大$2^{128}\div2^{32}=2^{96}$倍
- 灵活的IP报文头部格式：用固定格式的扩展头部取代IPv4的可变长度选项，路由器可以快速路过选项不做处理，**加快报文处理速度**
- 简化了报文头部，字段只有8个，**加快报文转发，提高吞吐量**
- 提高安全性
- 支持更多服务类型、允许协议继续演变

地址记录上，IPv4采用点分十进制，IPv6采用冒分十六进制。高位0可以省略，一段4个0可以用一个0表示，连续多段0用一个双冒号表示。

IPv6分为单播地址、组播地址和任播地址。

- 单播地址（Unicast）：用于单个接口的标识符，传统的点对点通信；
- 组播地址（Multicast）：一点对多点的通信。数据包交付到一组计算机中的每一个。IPv6没有广播的术语，而是将广播看成多播的特例。
- 任播地址（Anycast）：IPv6的新增类型。目的是一组计算机，但是数据包只交付给其中一个，通常是最近的那个。

IPv6每个网卡最少3个IPv6地址，分别为链路本地地址、全球单播地址和回送地址（站点本地地址）。多播前缀11111111（8个1）；任播前缀固定，其余位置为0；可聚合全球单播地址：前缀001，本地单播fe80，1111111010，站点本地1111111011。

IPv6把自动地址配置作为标准功能。IPv6地址分为全状态自动配置和无状态自动配置。全状态自动配置继承了IPv4的DHCP服务，无状态自动配置使主机通过两个阶段分别获得链路本地地址和可聚合全球单播地址。

过渡技术：双协议栈技术（节点对IPv4和IPv6双协议支持）、隧道技术（6to4/6over4/ISATAP）、NAT-PT（网关进行协议翻译和地址映射）

### IP地址与子网划分

![IPv4-address-classification.png](https://s2.loli.net/2023/03/28/w6YSdoXpEW9Nmn4.png)

在IPv4中，主机号全0或者全1不能做主机号，全0是网络号，全1是广播地址。DE类暂未使用。

特殊的几个IP地址：127.0.0.0/8网段本地回环地址，localhost；169.254.0.0是DHCP在Windows系统失败；0.0.0.0是DHCP在Linux系统失败。

子网划分：将一个网络划分成多个子网，本质上是取部分主机号作为内部的子网标识。路由汇聚：将多个网络合并成一个大网络，本质上是取部分网络号当主机号。当然网络汇聚会使得聚合网主机号“变大"，实则只是保留了这个部分作为寻址而已。

![merge-two-subnet.png](https://s2.loli.net/2023/03/28/uE6eRG7WH9xZaDg.png)

## 网络接入技术

分为有线接入技术和无线接入技术。有线主要有非对称数字用户线路（ADSL），同轴光纤（HFC）等；无线主要有Wi-Fi（IEEE 802.11)，蓝牙（IEEE 802.15），红外（IrDA），Zigbee。5G：高性能低延迟高容量。

## 综合布线系统

![network-wiring-system.png](https://s2.loli.net/2023/03/28/soe5dBabyT7Uhku.png)

## 物联网

物联网的核心和基础仍然是互联网，其用户端延伸和扩展到了任何物体与物体之间。分为三层：感知层、网络层和应用层。

- 感知层：识别物体、采集信息
- 网络层：传递信息
- 应用层：处理信息与人机交互
