# NAT地址的动静态转换实验
<img width="1239" height="591" alt="image" src="https://github.com/user-attachments/assets/481fc0e1-aaaa-45a8-9506-84b70465f5e0" />

前置条件 AR1 sysname R1
interface GigabitEthernet0/0/0 ip address 192.168.1.254 255.255.255.0
interface GigabitEthernet0/0/1 ip address 10.0.1.1 255.255.255.0

AR2 sysname R2
interface GigabitEthernet0/0/0 ip address 10.0.1.2 255.255.255.0
interface GigabitEthernet0/0/1ip address 192.168.2.254 255.255.255.0

## 静态nat 
nat static global 172.16.1.1 inside 192.168.1.1 netmask 255.255.255.255 
*静态地址转换指定某个地址全局应用*

## 动态nat

acl number 2000*创建基本规则*

rule 5 permit source 192.168.1.0 0.0.0.255*规则指定网端和反掩码*

nat address-group 1 172.16.1.1 172.16.1.5*设置转换后的地址组*

nat outbound 2000 address-group 1 no-pat*设置接口应用基本规则以及可用地址组*

ip route-static 172.168.1.0 255.255.255.0 10.0.1.2
*给一个静态路由指定网端*

### 知识要点

NAT地址转换技术||静态NAT||1V1转换||动态NAT

给一个地址池|判断哪些地址需要转换：1、创建地址组2、创建访问控制规则3、进入outbuond口设置not-pet
