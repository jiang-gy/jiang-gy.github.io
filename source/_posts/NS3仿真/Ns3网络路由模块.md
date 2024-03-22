```cpp
Ptr<Node> node = m_ipv4->GetObject<Node> ();  //获取相应的结点模型
Ptr<TrafficControlLayer> tc = node->GetObject<TrafficControlLayer> ();  //通过结点，获取相应的TC层
Ipv4RoutingTableEntry* route = allRoutes.at (i);   
uint32_t interfaceIdx = route->GetInterface ();  //获取队列端口号
// cout<<"ID "<<m_ipv4->GetObject<Node> ()->GetId ()<<"  interfaces "<<interfaceIdx<<endl;
Ptr<NetDevice> device = m_ipv4->GetNetDevice(interfaceIdx);  //获得对应的网络设备
Ptr<QueueDisc> root = tc -> GetRootQueueDiscOnDevice(device);  //获得相应网络设备对应的队列
uint32_t rootBytes = root->GetNBytes();  //获得队列中包含的字节量信息
cout<<"ID "<<m_ipv4->GetObject<Node> ()->GetId ()<<"  interfaces "<<interfaceIdx<<" Bytes "<<rootBytes<<endl;
```

