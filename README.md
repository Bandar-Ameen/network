
# NetWork with IP Phone 


  # Switch1
  enable
configure terminal

interface range fastEthernet 0/1-10
switchport voice vlan 1
exit


# Router0
enable

configure terminal



! ---------------- INTERFACES ----------------

interface fastEthernet 0/0

ip address 192.168.1.1 255.255.255.0

no shutdown



interface fastEthernet 0/1

ip address 193.168.1.1 255.255.255.0

no shutdown



! ---------------- DHCP ----------------

ip dhcp excluded-address 192.168.1.1



ip dhcp pool LAN1

network 192.168.1.0 255.255.255.0

default-router 192.168.1.1

dns-server 8.8.8.8

option 150 ip 192.168.1.1



! ---------------- ROUTING ----------------

ip route 194.168.1.0 255.255.255.0 193.168.1.2

ip route 195.168.1.0 255.255.255.0 193.168.1.2



! ---------------- VOIP ----------------

telephony-service

ip source-address 192.168.1.1 port 2000

max-ephones 4

max-dn 4

auto assign 1 to 4



ephone-dn 1

number 1000



ephone-dn 2

number 1001



ephone-dn 3

number 1002



ephone-dn 4

number 1003



! ---------------- DIAL PEER ----------------

dial-peer voice 10 voip

destination-pattern 3...

session target ipv4:195.168.1.1


# Router1

enable
configure terminal

! ---------------- INTERFACES ----------------
interface fastEthernet 0/1
ip address 193.168.1.2 255.255.255.0
no shutdown

interface fastEthernet 0/0
ip address 194.168.1.1 255.255.255.0
no shutdown

! ---------------- ROUTING ----------------
ip route 192.168.1.0 255.255.255.0 193.168.1.1
ip route 195.168.1.0 255.255.255.0 194.168.1.2





# Router2



enable
configure terminal

! ---------------- INTERFACES ----------------
interface fastEthernet 0/1
ip address 194.168.1.2 255.255.255.0
no shutdown

interface fastEthernet 0/0
ip address 195.168.1.1 255.255.255.0
no shutdown

! ---------------- DHCP ----------------
ip dhcp excluded-address 195.168.1.1

ip dhcp pool LAN2
network 195.168.1.0 255.255.255.0
default-router 195.168.1.1
dns-server 8.8.8.8
option 150 ip 195.168.1.1

! ---------------- ROUTING ----------------
ip route 192.168.1.0 255.255.255.0 194.168.1.1
ip route 193.168.1.0 255.255.255.0 194.168.1.1

! ---------------- VOIP ----------------
telephony-service
ip source-address 195.168.1.1 port 2000
max-ephones 4
max-dn 4
auto assign 1 to 4

ephone-dn 1
number 3000

ephone-dn 2
number 3001

ephone-dn 3
number 3002

ephone-dn 4
number 3003

! ---------------- DIAL PEER ----------------
dial-peer voice 10 voip
destination-pattern 1...
session target ipv4:192.168.1.1





# switch2

enable
configure terminal

interface range fastEthernet 0/1-10
switchport voice vlan 1
exit




# screenshot
![khj](https://raw.githubusercontent.com/Bandar-Ameen/network/refs/heads/main/3_router_connect_with_ip_phone.PNG)
