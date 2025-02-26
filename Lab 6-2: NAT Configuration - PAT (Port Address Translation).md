
### Objective

Configure Port Address Translation (PAT) on Router1 so that PCs on the 192.168.0.0/24 network can share a single public IP address (30.0.0.120) to access external networks.

### Router Interface Configuration

#### Router 1

enable
configure terminal
interface FastEthernet 0/0
ip address 192.168.0.1 255.255.255.0
no shutdown
exit
interface Serial 0/0/0
ip address 30.0.0.1 255.0.0.0
no shutdown
exit



#### Router 2

enable
configure terminal
interface FastEthernet 0/0
ip address 20.0.0.1 255.0.0.0
no shutdown
exit
interface Serial 0/0/0
ip address 30.0.0.2 255.0.0.0
no shutdown
exit


### Configure Routing

#### Router 1 - Default Route

enable
configure terminal
ip route 0.0.0.0 0.0.0.0 30.0.0.2
end



### Configure PAT on Router 1

1.  **Define Inside and Outside Interfaces**

enable
configure terminal
interface FastEthernet 0/0
ip nat inside
exit
interface Serial 0/0/0
ip nat outside
exit


2.  **Create Address Pool**

ip nat pool test 30.0.0.120 30.0.0.120 netmask 255.0.0.0



3.  **Create Access List**

access-list 1 permit 192.168.0.0 0.0.0.255



4.  **Assign Pool and Access Rule**

ip nat inside source list 1 pool test overload
end



### Verification

From a PC, access the web service on the server (20.0.0.2).  Then, check the NAT table on Router1:

enable
show ip nat translations



The output should show translations similar to this:

Pro Inside global Inside local Outside local Outside global
icmp 30.0.0.120:1 192.168.0.7:1 20.0.0.2:1 20.0.0.2:1
icmp 30.0.0.120:2 192.168.0.7:2 20.0.0.2:2 20.0.0.2:2


### Tech Journal Entries - Key Commands and Explanation

*   **`ip nat inside`**:  Configures an interface as the inside (private) interface for NAT.
*   **`ip nat outside`**: Configures an interface as the outside (public) interface for NAT.
*   **`ip nat pool <pool-name> <start-ip> <end-ip> netmask <mask>`**: Creates a pool of public IP addresses for NAT.
*   **`access-list <access-list-number> permit <source-network> <wildcard-mask>`**: Defines which internal IP addresses are allowed to use NAT.
*   **`ip nat inside source list <access-list-number> pool <pool-name> overload`**:  Links the access list and NAT pool, enabling PAT. The `overload` keyword allows multiple internal addresses to share a single public IP address using different port numbers.
*   **`show ip nat translations`**: Displays the active NAT translations table.
