## BTV Router
```
hostname btv-router
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
hostname mtl-router
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
hostname btv-multilayer-switch
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

















