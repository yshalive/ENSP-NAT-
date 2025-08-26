

nat
前置条件
AR1
sysname R1
#
interface GigabitEthernet0/0/0
ip address 192.168.1.254 255.255.255.0
#
interface GigabitEthernet0/0/1
ip address 10.0.0.1 255.255.255.0
AR2
sysname R2
#
interface GigabitEthernet0/0/0
ip address 10.0.0.2 255.255.255.0
#
interface GigabitEthernet0/0/1
ip address 192.168.2.254 255.255.255.0
#
静态nat
nat static global 172.16.1.1 inside 192.168.1.1 netmask 255.255.255.255
动态nat
AR1
#
acl number 2000
rule 5 permit source 192.168.1.0 0.0.0.255
#
nat address-group 1 172.16.1.1 172.16.1.5
#
interface GigabitEthernet0/0/0
ip address 192.168.1.254 255.255.255.0
#
interface GigabitEthernet0/0/1
ip address 10.0.0.1 255.255.255.0
nat outbound 2000 address-group 1 no-pat
#
ip route-static 192.168.2.0 255.255.255.0 10.0.0.2

AR2
ip route-static 172.16.1.0 255.255.255.0 10.0.0.1
ip route-static 192.168.1.0 255.255.255.0 10.0.0.1
