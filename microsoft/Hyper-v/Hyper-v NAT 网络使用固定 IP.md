# Hyper-v NAT 网络使用固定 IP

1. 查看 nat 网络

       Get-NetNat

   如果已经存在 NAT 网络，需要先删除

       Remove-NetNat

2. 创建虚拟交换机

       New-VMSwitch -SwitchName "hyper-v-nat" -SwitchType Internal -Verbose

3. 查看虚拟交换机的接口索引

       Get-NetAdapter

   `ifIndex`：虚拟交换机的接口索引

4. 配置 NAT 网关

       New-NetIPAddress -IPAddress 192.168.10.1 -PrefixLength 24 -InterfaceIndex <ifIndex> -Verbose

   `IPAddress`：NAT 网关 IP  
   `PrefixLength`：NAT 子网前缀长度  
   `InterfaceIndex`：虚拟交换机的接口索引

5. 配置 NAT 网络

       New-NetNat -Name NATNetwork -InternalIPInterfaceAddressPrefix 192.168.10.0/24 -Verbose

   `Name`：NAT 网络的名称  
   `InternalIPInterfaceAddressPrefix`：NAT 网关 IP 前缀