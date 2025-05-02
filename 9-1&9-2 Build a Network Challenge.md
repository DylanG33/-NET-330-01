# 9-1
## BTV Router
```
interface FastEthernet 0/0
ip address 172.16.10.1 255.255.255.0
no shutdown
interface Serial 0/1/0
ip address 172.16.0.1 255.255.255.252
no shutdown
router ospf 1
default-information originate
network 172.16.10.0 0.0.0.255 area 0
network 172.16.0.0 0.0.0.3 area 0
```
## MTL Router:
```
interface FastEthernet 0/0
ip address 172.16.20.1 255.255.255.0
no shutdown
interface Serial 0/1/0
ip address 172.16.0.2 255.255.255.252
no shutdown
exit
router ospf 1
network 172.16.20.0 0.0.0.255 area 0
network 172.16.0.0 0.0.0.3 area 0
```
## BTV Multilayer Switch:
```
ip routing
interface vlan 1
no shutdown
interface vlan 5
no shutdown
ip address 172.16.5.1 255.255.255.0
interface vlan 6
no shutdown
ip address 172.16.6.1 255.255.255.0
interface vlan 10
no shutdown
ip address 172.16.10.2 255.255.255.0
interface range FastEthernet 0/2
switchport acess vlan 5
interface range FastEthernet 0.6
switchport access vlan 6
interface range FastEthernet 0/1
switchport access vlan 10
router ospf 10
network 172.16.5.0 0.0.0.255 area 0
network 172.16.6.0 0.0.0.255 area 0
network 172.16.10.0 0.0.0.255 area 0
```

# 9-2
## Vermont ISP:
```
interface FastEthernet 0/0
ip address 192.168.1.1 255.255.255.252
no shutdown
interface FastEthernet 0/1
ip address 192.168.2.1 255.255.255.252
no shutdown
router bgp 1010
neighbor 192.168.2.2 remote-as 3033
neighbor 192.168.1.2 remote-as 2054
network 192.168.1.0 mask 255.255.255.252
```
## BTV Router:
```
interface FastEthernet0/1
ip address 192.168.2.2 255.255.255.0 
ip route 0.0.0.0 0.0.0.0 192.168.2.1
router bgp 3033
neighbor 192.168.2.1 remote-as 1010
redistribute ospf 1
network 192.168.2.0 mask 255.255.255.252
```
## Pacific ISP:
```
interface FastEthernet 0/0
ip address 192.168.1.2 255.255.255.252
no shutdown
interface FastEthernet 0/1
ip address 192.168.3.1 255.255.255.252
no shutdown
interface Serial 0/1/0
ip address 192.168.4.1 255.255.255.252
no shutdown
router bgp 2054
neighbor 192.168.1.1 remote-as 1010
neighbor 192.168.3.2 remote-as 34908
neighbor 192.168.4.2 remote-as 5132
network 192.168.3.0 mask 255.255.255.252
network 192.168.4.0 mask 255.255.255.252
```
## Customer Router:
```
interface FastEthernet 0/0
ip address 10.200.24.1 255.255.255.0
no shutdown
interface Serial 0/1/0
ip address 192.168.4.2 255.255.255.252
no shutdown
router bgp 5132
neighbor 192.168.4.1 remote-as 2054
network 10.200.24.0 mask 255.255.255.0
```
## Partner-Router:
```
interface FastEthernet 0/0
ip address 192.168.3.2 255.255.255.252
no shutdown
interface FastEthernet 0/1
ip address 10.15.6.1 255.255.255.0
no shutdown
router bgp 34908
neighbor 192.168.3.1 remote-as 2054
network 10.15.6.0 mask 255.255.255.0
```













