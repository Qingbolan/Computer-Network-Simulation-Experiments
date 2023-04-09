# **Lab 2. Addressing Technology**

​																										                 			==SILAN HU==|==2009853P-I011-0015==


#### ==**Objective**==

- Understand the Addressing Technologies, including DHCP, NAT and IPv6 transition.





 

#### ==**Topology**==

![image-20230311225640298](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230311225640298.png)



#### ==**Address Scheme**==

**Inside:**

![image-20230314120706916](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314120706916.png)

==**Outside:**==

![image-20230314120804544](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314120804544.png)

==**Translation:**==

![image-20230314120859727](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314120859727.png)

## **Part 1 – DHCP.**

> Requirement:
> 1.1 Dynamic IP addresses to Teacher-PCs/Student-PCs. (DHCP via Gatway-Router1)
> 1.2 Dynamic IP addresses to Guest-Laptops. (DHCP via DHCP-Server)

### ==Step 1 – DHCP Router==

#### 1. ==configure the DHCP pool== on the router (e.g. Gateway-Rotuer1).

Reference 4. DHCP .Q 22 ~24

```bash
Gatweay-Router1(config)#service dhcp
Gatweay-Router1(config)#ip dhcp pool Teacher-DHCPPool
Gatweay-Router1(dhcp-config)#network 192.168.11.0 255.255.255.0
Gatweay-Router1(dhcp-config)#default-router 192.168.11.254
Gatweay-Router1(dhcp-config)#ip dhcp excluded-address 192.168.11.1 192.168.11.100
Gatweay-Router1(config)#ip dhcp excluded-address 192.168.11.200 192.168.11.255
Gatweay-Router1(config)#ip dhcp pool Student-DHCPPool
Gatweay-Router1(dhcp-config)#network 192.168.22.0 255.255.255.0
Gatweay-Router1(dhcp-config)#default-router 192.168.22.254
Gatweay-Router1(dhcp-config)#ip dhcp excluded-address 192.168.22.1 192.168.22.100
Gatweay-Router1(config)#ip dhcp excluded-address 192.168.22.200 192.168.22.255
```




#### 2. ==configure the DHCP relay== from PCs to the router (e.g. Gateway-Rotuer1).

Reference 4.DHCP.Q25;

```bash
Switch3(config)#interface vlan 11
Switch3(config-if)#ip helper-address 192.168.101.1
Switch3(config-if)#interface vlan 22
Switch3(config-if)#ip helper-address 192.168.101.1


Switch4(config)#interface vlan 11
Switch4(config-if)#ip helper-address 192.168.102.1
Switch4(config-if)#interface vlan 22
Switch4(config-if)#ip helper-address 192.168.102.1
```

Reference 4.DHCP.Q9,12; Q13,19

```bash
Switch3(config)#interface FastEthernet 0/1
Switch3(config-if)#switchport mode access
Switch3(config-if)#switchport access vlan 101
% Access VLAN does not exist. Creating vlan 101
Switch3(config-if)#interface vlan 101
Switch3(config-if)#ip address 192.168.101.2 255.255.255.0
Switch3(config-if)#no shutdown
%LINK-5-CHANGED: Interface Vlan101, changed state to up


Switch4(config)#interface FastEthernet 0/1
Switch4(config-if)#switchport mode access
Switch4(config-if)#switchport access vlan 102
% Access VLAN does not exist. Creating vlan 102
Switch4(config-if)#interface vlan 102
Switch4(config-if)#ip address 192.168.102.2 255.255.255.0
Switch4(config-if)#no shutdown
%LINK-5-CHANGED: Interface Vlan102, changed state to up


Gatweay-Router1(config)#interface FastEthernet 0/0
Gatweay-Router1(config-if)#ip address 192.168.101.1 255.255.255.0
Gatweay-Router1(config-if)#no shutdown
Gatweay-Router1(config-if)#interface FastEthernet 0/1
Gatweay-Router1(config-if)#ip address 192.168.102.1 255.255.255.0
Gatweay-Router1(config-if)#no shutdown
Gatweay-Router1(config-if)#exit
Gatweay-Router1(config)#ip route 192.168.0.0 255.255.0.0 192.168.101.2
Gatweay-Router1(config)#ip route 192.168.99.0 255.255.255.0 192.168.102.2
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up
%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/1, changed state to up
```

![image-20230314155444271](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314155444271.png)

![image-20230314155344956](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314155344956.png)

![image-20230314155636892](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314155636892.png)

![image-20230314155315854](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314155315854.png)

![image-20230314155517848](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230314155517848.png)

```bash
Gatweay-Router1#show ip dhcp binding
IP address       Client-ID/              Lease expiration        Type
                 Hardware address
192.168.11.101   0000.0C73.9546           --                     Automatic
192.168.11.102   0005.5E39.9EEA           --                     Automatic
192.168.22.101   0001.4375.E3C1           --                     Automatic
192.168.22.102   00D0.9725.71B8           --                     Automatic
```




### ==Step 2 – DHCP Server==

#### 3. configure the DHCP pool on the server (e.g. DHCP-Server).

- setting the server address

![image-20230316174657620](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316174657620.png)

- DHCP service(VLAN88)

![image-20230316175539810](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316175539810.png)

- access vlan 99 on Switch99

  ```bash
  Switch99(config)#int FastEthernet 0/3
  Switch99(config-if)#switchport mode access
  Switch99(config-if)#switchport access vlan 99
  ```

#### 4. configure the DHCP relay from Laptops to the server (e.g. DHCP-Server).

Reference 4.DHCP.Q25

```bash
Switch3(config)#interface vlan 88
Switch3(config-if)#ip helper-address 192.168.99.103


Switch4(config)#interface vlan 88
Switch4(config-if)#ip helper-address 192.168.99.103
```

- Laptop-anto-config

  ![image-20230316180710321](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316180710321.png)

  ![image-20230316180739716](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316180739716.png)

## **Part 2 – NAT.**

> Requirement:

> 2.1 Internet-PC -> Web-Server/FTP-Server. (Static NAT)
> 2.2 Teacher-PCs/Student-PCs/Guest-Laptops -> Internet-PC. (Dynamic NAT) 

### ==Step 3 – Static NAT==

#### 5. configure the static nat for server translation on the border router (Gateway-Router1).

Reference 4.NAT.Q30~31

```bash
Gatweay-Router1(config)#ip nat inside source static 192.168.99.101 200.200.123.2
Gatweay-Router1(config)#ip nat inside source static 192.168.99.102 200.200.123.3
Gatweay-Router1(config)#interface range FastEthernet 0/0-1
Gatweay-Router1(config-if-range)#ip nat inside
Gatweay-Router1(config-if-range)#interface range FastEthernet 1/0
Gatweay-Router1(config-if-range)#ip nat outside
```






#### 6. configure the route from border router (Gateway-Router1) to ISP router.

Reference 4.NAT.Q13,16,17;

![image-20230316181153770](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316181153770.png)

Reference 4.NAT.Q18,20,21

![image-20230316181328165](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316181328165.png)

```bash
Gatweay-Router1(config)#interface f 1/0
Gatweay-Router1(config-if)#ip address 200.200.200.2 255.255.255.252
Gatweay-Router1(config-if)#no shutdown
Gatweay-Router1(config-if)#
%LINK-5-CHANGED: Interface FastEthernet1/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet1/0, changed state to up


ISP-Router(config)#interface f 0/0
ISP-Router(config-if)#ip address 1.1.1.1 255.0.0.0
ISP-Router(config-if)#no shutdown
ISP-Router(config-if)#interface f 1/0
ISP-Router(config-if)#ip address 200.200.200.1 255.255.255.252
ISP-Router(config-if)#no shutdown
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up
%LINK-5-CHANGED: Interface FastEthernet1/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet1/0, changed state to up
```

```bash
Switch3(config)#ip route 0.0.0.0 0.0.0.0 192.168.101.1


Switch4(config)#ip route 0.0.0.0 0.0.0.0 192.168.102.1


Gatweay-Router1(config)#ip route 0.0.0.0 0.0.0.0 200.200.200.1


ISP-Router(config)#ip route 200.200.123.0 255.255.255.248 200.200.200.2
```

- **From : Internet-PC to FTP-Server**

  ![image-20230316183543762](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316183543762.png)

- **From : Teacher-PC to Internet-PC**

![image-20230316195109516](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316195109516.png)






### ==Step 4 – Dynamic NAT==

#### 7. configure the dynamic nat for PC translation on the border router (Gateway-Router1).

Reference 4.NAT.Q37~39

```bash
Gatweay-Router1(config)#ip access-list standard NAT-List
Gatweay-Router1(config-std-nacl)#permit 192.168.11.0 0.0.0.255
Gatweay-Router1(config-std-nacl)#permit 192.168.22.0 0.0.0.255
Gatweay-Router1(config-std-nacl)#permit 192.168.88.0 0.0.0.255
Gatweay-Router1(config-std-nacl)#exit
Gatweay-Router1(config)#ip nat pool NAT-Pool 200.200.123.1 200.200.123.1 netmask 255.255.255.248
Gatweay-Router1(config)#ip nat inside source list NAT-List pool NAT-Pool overload
```



## **Part 3 – IPv6 transition.**

> Requirement:
> 3.1 IPv6-PC -> IPv6-Server. (Tunneling)
> 3.2 IPv6-PC -> Web-Server/FTP-Server. (NATPT)

### ==Step 5 – IPv6 tunnel==
#### 1. configure the ipv6 subnet on the PC site.

- configure IPV6-Router interface

```bash
IPv6-Router(config)#ipv6 unicast-routing
IPv6-Router(config)#interface f 0/0
IPv6-Router(config-if)#ipv6 address 2001:2345:6789:66::6/64
IPv6-Router(config-if)#no shutdown

IPv6-Router(config-if)#interface f 0/1
IPv6-Router(config-if)#ip address 192.168.66.6 255.255.255.0
IPv6-Router(config-if)#no shutdown
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up
%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/1, changed state to up
```

- configure each PC

![image-20230316195814325](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316195814325.png)

![image-20230316194039983](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230316194039983.png)

#### 2. configure the ipv6 subnet on the Server site.

```bash
Router99(config)#ipv6 unicast-routing
Router99(config)#interface f 0/0
Router99(config-if)#ipv6 address 2001:2345:6789:99::6/64
Router99(config-if)#no shutdown

Router99(config-if)#interface f 0/1
Router99(config-if)#ip address 192.168.99.6 255.255.255.0
Router99(config-if)#no shutdown
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up
%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/1, changed state to up
```

#### 3. configure the ipv4 subnets between the PC site and Server site.

```bash
Switch3(config)#interface f 0/6
Switch3(config-if)#switchport mode access
Switch3(config-if)#switchport access vlan 66
% Access VLAN does not exist. Creating vlan 66
Switch3(config-if)#
%HSRP-6-STATECHANGE: Vlan99 Grp 99 state Speak -> Standby

Switch3(config)#interface vlan 66
Switch3(config-if)#ip address 192.168.66.1 255.255.255.0
Switch3(config-if)#no shutdown
Switch3(config-if)#standby 66 ip 192.168.66.254
Switch3(config-if)#standby 66 priority 99
Switch3(config-if)#standby 66 preempt
%LINK-5-CHANGED: Interface Vlan66, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan66, changed state to up


Switch4(config)#interface vlan 66
Switch4(config-if)#ip address 192.168.66.2 255.255.255.0
Switch4(config-if)#no shutdown
Switch4(config-if)#standby 66 ip 192.168.66.254
Switch4(config-if)#standby 66 priority 101
Switch4(config-if)#standby 66 preempt
%LINK-5-CHANGED: Interface Vlan66, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan66, changed state to up
%HSRP-6-STATECHANGE: Vlan66 Grp 66 state Standby -> Active
```

```bash
Switch99(config)#int f 0/6
Switch99(config-if)#switchport mode access
Switch99(config-if)#switchport access vlan 99
```

#### 4. configure the ipv6 over ipv4 tunnel between the routers of the PC site and Server site.

Reference 4. tunnel

```bash
IPv6-Router(config-if)#tunnel source f 0/1
IPv6-Router(config-if)#tunnel destination 192.168.99.6
IPv6-Router(config-if)#tunnel mode ipv6ip
IPv6-Router(config-if)#ipv6 address 2001:2345:6789:64::66/64
%LINK-5-CHANGED: Interface Tunnel64, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Tunnel64, changed state to up


Router99(config)#interface tunnel 64
Router99(config-if)#tunnel source fastEthernet 0/1
Router99(config-if)#tunnel destination 192.168.66.6
Router99(config-if)#tunnel mode ipv6ip
Router99(config-if)#ipv6 address 2001:2345:6789:64::99/64
%LINK-5-CHANGED: Interface Tunnel64, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Tunnel64, changed state to up
```

#### 5. configure the ipv4 route and ipv4 route between the routers of the PC site and Server site.

```bash
IPv6-Router(config)#ip route 192.168.99.0 255.255.255.0 192.168.66.254
IPv6-Router(config)#ipv6 route 2001:2345:6789:99::/64 2001:2345:6789:64::99

Router99(config)#ip route 192.168.66.0 255.255.255.0 192.168.99.254
Router99(config)#ipv6 route 2001:2345:6789:66::/64 2001:2345:6789:64::66
```


#### 6. test the connectivity of the tunnel between the PC site and Server site.

- From IPv6-PC1 to IPv6-Server

  ![image-20230319125357817](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230319125357817.png)

- From IPv6-Server  to IPv6-PC2

  ![image-20230319125923223](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230319125923223.png)

### Step 6 – NAT-PT

#### 11. configure the nat-pt on IPv6-Router.

Reference 4.natpt. Configuration Examples for NAT-PT for IPv6

```bash
IPv6-Router(config)#interface f 0/0
IPv6-Router(config-if)#ipv6 nat
IPv6-Router(config)#interface f 0/1
IPv6-Router(config-if)#ipv6 nat

IPv6-Router(config)#ipv6 access-list v6List
IPv6-Router(config-ipv6-acl)#permit ipv6 2001:2345:6789:66::/64 2001:2345:6789:99::192.168.99.101/128
IPv6-Router(config-ipv6-acl)#permit ipv6 2001:2345:6789:66::/64 2001:2345:6789:99::192.168.99.102/128

IPv6-Router(config-ipv6-acl)#exit

IPv6-Router(config)#ipv6 nat v6v4 pool v4Pool 192.168.66.101 192.168.66.199 prefix-length 24
IPv6-Router(config)#ipv6 nat v6v4 source list v6List pool v4Pool

IPv6-Router(config)#ipv6 nat prefix 2001:2345:6789:99::/96
IPv6-Router(config)#interface f 0/0
IPv6-Router(config-if)#ipv6 nat prefix 2001:2345:6789:99::/96 v4-mapped v6List
```

- From IPv6-PC1 to FTP-Server

  ![image-20230319154326316](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230319154326316.png)

```bash
IPv6-Router#show ipv6 nat translations
Prot  IPv4 source              IPv6 source
      IPv4 destination         IPv6 destination
---   192.168.66.101           2001:2345:6789:66:260:70FF:FE4C:7D9B
---   ---                      ---                     

IPv6-Router#show ipv6 nat translations
Prot  IPv4 source              IPv6 source
      IPv4 destination         IPv6 destination
icmp  192.168.66.101,13        2001:2345:6789:66:260:70FF:FE4C:7D9B,13
      192.168.99.102,13        2001:2345:6789:99::C0A8:6366,13

icmp  192.168.66.101,14        2001:2345:6789:66:260:70FF:FE4C:7D9B,14
      192.168.99.102,14        2001:2345:6789:99::C0A8:6366,14

icmp  192.168.66.101,15        2001:2345:6789:66:260:70FF:FE4C:7D9B,15
      192.168.99.102,15        2001:2345:6789:99::C0A8:6366,15

icmp  192.168.66.101,16        2001:2345:6789:66:260:70FF:FE4C:7D9B,16
      192.168.99.102,16        2001:2345:6789:99::C0A8:6366,16

---   192.168.66.101           2001:2345:6789:66:260:70FF:FE4C:7D9B
---   ---                      ---                     
```

