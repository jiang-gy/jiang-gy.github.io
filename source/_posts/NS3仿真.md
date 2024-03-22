---
title: NS3仿真
top: false
cover: false
toc: true
mathjax: false
date: 2024-02-01 09:29:35
coverImg:
password:jgy123
summary:
tags:
- 网络仿真
categories:

---

# NS3流量激励

## 一 涉及论文

-   Based on Deep Reinforcement Learning with Context Network and Experience pool optimization for Mix-Flow Scheduling in SD-DCN(2023)
    -   Flash: Joint Flow Scheduling and Congestion Control in Data Center Networks
    -   Inside the Social Network’s (Datacenter) Network（流量均在这里面）
-   Asymmetry-Aware Load Balancing With Adaptive Switching Granularity in Data Center(2019)

## 二 代码仓库

-   Ammar, Doreid; Begin, Thomas; Guerin-Lassous, Isabelle (Eds.) (2011): A new tool for generating realistic Internet traffic in NS-3.
    Location 4:	https://github.com/doreidammar/PPBP---network-traffic-generator---ns3
-   https://github.com/SoonyangZhang/possion-traffic/tree/master
-   [keddah - Hadoop Network Traffic Generator in NS3](https://github.com/deng113jie/keddah#keddah---hadoop-network-traffic-generator-in-ns3)
-   https://github.com/SHM91/NS3-RealisticTrafficGen1#ns3-realistictrafficgen

## 三 理论介绍

```c++
#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/internet-module.h"
#include "ns3/applications-module.h"

using namespace ns3;

int main() {
  // 创建节点
  NodeContainer nodes;
  nodes.Create(2);

  // 创建通信信道
  PointToPointHelper pointToPoint;
  pointToPoint.SetDeviceAttribute("DataRate", StringValue("5Mbps"));
  pointToPoint.SetChannelAttribute("Delay", StringValue("2ms"));

  NetDeviceContainer devices;
  devices = pointToPoint.Install(nodes);

  // 安装Internet协议栈
  InternetStackHelper stack;
  stack.Install(nodes);

  // 为节点分配IP地址
  Ipv4AddressHelper address;
  address.SetBase("10.1.1.0", "255.255.255.0");
  Ipv4InterfaceContainer interfaces = address.Assign(devices);

  // 创建PacketSink应用程序
  PacketSinkHelper sinkHelper("ns3::UdpSocketFactory", Address(InetSocketAddress(interfaces.GetAddress(1), 9)));
  ApplicationContainer sinkApps = sinkHelper.Install(nodes.Get(1));
  sinkApps.Start(Seconds(0.0));
  sinkApps.Stop(Seconds(10.0));

  // 创建Data Mining流量生成器
  OnOffHelper onoff("ns3::UdpSocketFactory", Address(InetSocketAddress(interfaces.GetAddress(1), 9)));
  onoff.SetAttribute("PacketSize", UintegerValue(1024));
  onoff.SetAttribute("OnTime", StringValue("ns3::ConstantRandomVariable[Constant=1]"));
  onoff.SetAttribute("OffTime", StringValue("ns3::ConstantRandomVariable[Constant=9]")); // OffTime设置为9秒，使得Offered Load为0.1（1 / (1 + 9) = 0.1）

  // 安装流量生成器
  ApplicationContainer apps = onoff.Install(nodes.Get(0));
  apps.Start(Seconds(1.0));
  apps.Stop(Seconds(10.0));

  // 运行仿真
  Simulator::Run();
  Simulator::Destroy();

  return 0;
}

```

