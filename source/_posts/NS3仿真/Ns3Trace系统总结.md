# Ns3 Trace系统

## Trace变量配置

​	由于Ns3初始化并没有提供Trace变量的初始值，创建变量时无法根据配置好的函数指针初始化Trace变量，因此只能在已存在的C++对象上配置Trace变量。

​	在对象未创建、未分配内存时，Trace变量是无法配置的，即使配置相关属性，也不能成功使用。因此，Trace变量的配置操作必须放在网络拓扑用户应用建立完成之后，但必须放在`Simulation::Run()`之前。为保证每次成功配置并成功运行，十分建议养成在**程序末尾配置Trace + 开启仿真运行的习惯**。

### 1. ipv4-l3-protocol发送数据包

```cpp
//src/internet/model/ipv4-l3-protocol.cc
TypeId 
Ipv4L3Protocol::GetTypeId (void)
{
    ...
	.AddTraceSource ("TxTrace",
                     "Send ipv4 packet to outgoing interface.",
                     MakeTraceSourceAccessor (&Ipv4L3Protocol::m_adTrace),
                     "ns3::Ipv4L3Protocol::AdressCallback")
    ...
}


void
Ipv4L3Protocol::CallTxTrace (const Ipv4Header & ipHeader, Ptr<Packet> packet,
                                    Ptr<Ipv4> ipv4, uint32_t interface)
{
  Ptr<Packet> packetCopy = packet->Copy ();
  packetCopy->AddHeader (ipHeader);
  m_txTrace (packetCopy, ipv4, interface);
}

//src/internet/model/ipv4-l3-protocol.h
...
  // The following two traces pass a packet with an IP header
  /// Trace of transmitted packets
  /// \deprecated The non-const \c Ptr<Ipv4> argument is deprecated
  /// and will be changed to \c Ptr<const Ipv4> in a future release.
  TracedCallback<Ptr<const Packet>, Ptr<Ipv4>,  uint32_t> m_txTrace;
...
```



