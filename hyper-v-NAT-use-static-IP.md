---
title: hyper-v NAT 网络使用固定 IP
date: 2020-05-18 16:44:19
urlname: hyper-v-use-nat
categories:
  - [windows]
  - [hyper-v]
tags:
  - [windows]
  - [hyper-v]
---
Hyper-v NAT 网络使用固定 IP
<!--more-->
# Hyper-v NAT 网络使用固定 IP

## 查看 nat 网络

```
Get-NetNat
```

如果已经存在 NAT 网络，需要先删除

```
Remove-NetNat
```

## 创建虚拟交换机

```
New-VMSwitch -SwitchName "hyper-v-nat" -SwitchType Internal -Verbose
```

## 查看虚拟交换机的接口索引

```
Get-NetAdapter
```

|参数|描述|
|:-|:-|
|`ifIndex`|虚拟交换机的接口索引|

## 配置 NAT 网关

```
New-NetIPAddress -IPAddress 192.168.10.1 -PrefixLength 24 -InterfaceIndex <ifIndex> -Verbose
```

|参数|描述|
|:-|:-|
|`IPAddress`|NAT 网关 IP|
|`PrefixLength`|NAT 子网前缀长度|
|`InterfaceIndex`|虚拟交换机的接口索引|

## 配置 NAT 网络

```
New-NetNat -Name NATNetwork -InternalIPInterfaceAddressPrefix 192.168.10.0/24 -Verbose
```

|参数|描述|
|:-|:-|
|`Name`|NAT 网络的名称|
|`InternalIPInterfaceAddressPrefix`|NAT 网关 IP 前缀|