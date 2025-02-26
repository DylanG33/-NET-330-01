VLAN Creation

text
enable
configure terminal
vlan 100
name FacStaff
exit
vlan 110
name Student
exit
vlan 130
name StuLab1
exit
vlan 140
name StuLab2
exit

Interface Range Configuration

text
interface range FastEthernet 0/4-12
switchport mode access
switchport access vlan 100
spanning-tree portfast
exit

interface range FastEthernet 0/13-20
switchport mode access
switchport access vlan 110
spanning-tree portfast
exit

Trunk Port Configuration

text
interface FastEthernet 0/1
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 1,100,110,130,140
no shutdown
exit

Enable Routing (Core Switch)

text
ip routing
interface vlan 100
ip address 10.x.100.1 255.255.255.0
no shutdown
exit
interface vlan 110
ip address 10.x.110.1 255.255.255.0
no shutdown
exit

Verification Commands

text
show vlan brief
show interfaces trunk
show ip route
