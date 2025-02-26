Server Configuration

text
IP Address: 10.x.y.2
Subnet Mask: 255.255.255.0
Default Gateway: 10.x.y.1

East-Core-Switch Configuration

text
enable
configure terminal
interface FastEthernet 0/3
switchport mode access
switchport access vlan 1
no shutdown
exit

interface vlan 1
ip address 10.x.y.1 255.255.255.0
no shutdown
end

Verification

text
ping 10.x.y.2
