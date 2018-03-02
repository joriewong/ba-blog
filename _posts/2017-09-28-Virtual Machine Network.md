---
  layout: post
  title: Virtual Machine Network
  categories: [OPS]
---

## NAT(Network Address Translation)

### 网络地址转换

Guest访问网络的所有数据都是由Host提供，Guest能访问到Host能访问到的所有网络，但Guest不真实存在于网络中，主机和其他机器都访问不到Guest。

### 端口转发

添加端口转发规则，可使用Host的IP和端口访问Guest

![image_1bqeemj9d1geh1dntijmt8b19t39.png-32.9kB][1]

## Bridged Adapter

### 桥接网络

Guest通过主机网卡，直接连入到网络中，Guest会被分配独立的IP，其网络功能和网络中的真实机器完全相同，Guest均可和Host及其他同一网段机器互相访问。

## Internal

### 内网模式

Guest与外网完全断开，只允许Guest之间互相访问。

## Host—only Adapter

### 主机模式

Guest模拟专供Guest使用的网卡，该网卡与Host不属于同一网段，所有Guest都连接到该网卡，通过该网卡实现很多网络功能。Guest之间可以搭建内网，Guest可以通过桥接网络访问外网，Guest和Host可以通过设置网段互相访问。


  [1]: http://static.zybuluo.com/wongjorie/qs1zd6kebidfydn34towqqx5/image_1bqeemj9d1geh1dntijmt8b19t39.png
