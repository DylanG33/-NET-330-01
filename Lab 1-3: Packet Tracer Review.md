Router Interface Configuration

text
enable
configure terminal
interface FastEthernet 0/0
ip address 192.168.3.1 255.255.255.0
no shutdown
exit
interface FastEthernet 0/1
ip address 192.168.1.1 255.255.255.0
no shutdown
end

Save Router Configuration

text
enable
copy running-config startup-config

Verification

text
ping 192.168.1.2
