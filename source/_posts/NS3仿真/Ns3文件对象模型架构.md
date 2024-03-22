# Ns3对象之间的关联

```cpp
m_ipv4->GetObject<Node> ()->GetId ()
```

## 网络层对象

具体代码存在于`src/internet/model/ipv4-l3-protocol.h`中

```cpp
  /**
   * \brief Get an interface.
   * \param i interface index
   * \return IPv4 interface pointer
   */
  Ptr<Ipv4Interface> GetInterface (uint32_t i) const;
  uint32_t GetNInterfaces (void) const;

  int32_t GetInterfaceForAddress (Ipv4Address addr) const;
  int32_t GetInterfaceForPrefix (Ipv4Address addr, Ipv4Mask mask) const;
  int32_t GetInterfaceForDevice (Ptr<const NetDevice> device) const;
  bool IsDestinationAddress (Ipv4Address address, uint32_t iif) const;
```

## 链路层对象

主要文件位于`src/network/model/net-device.h`

```cpp
  /**
   * \param index ifIndex of the device 
   */
  virtual void SetIfIndex (const uint32_t index) = 0;
  /**
   * \return index ifIndex of the device 
   */
  virtual uint32_t GetIfIndex (void) const = 0;

```

