# **Lab 1.LANs Technology**

​																																							==SILAN HU==|==2009853P-I011-0015==

​																																							==2023-2-23==

#### **Objective**

- Understand the LANs Technologies, including switched LANs, virtual LANs and wireless LANs.



 

#### **Topology**

![image-20230221160441543](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221160441543.png)



#### ==**Address Scheme**==

![image-20230221162049566](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221162049566.png)

## **Part 1 – Switched LANs.**

### ==Step 5 – STP==

#### 10. ==configure the root switch of the spanning-tree protocol== for each vlan.

Reference 1.Q27-Q28

```bash
Switch3(config)#spanning-tree vlan 11 priority 4096
Switch3(config)#spanning-tree vlan 22 priority 4096
Switch3(config)#spanning-tree vlan 88 priority 4096
Switch3(config)#spanning-tree vlan 99 priority 8192


Switch4(config)#spanning-tree vlan 11 priority 8192
Switch4(config)#spanning-tree vlan 22 priority 8192
Switch4(config)#spanning-tree vlan 88 priority 8192
Switch4(config)#spanning-tree vlan 99 priority 4096


Switch1#show spanning-tree vlan 11
VLAN0011
  Spanning tree enabled protocol ieee
  Root ID    Priority    4107
             Address     000B.BE7B.8A54
             Cost        19
             Port        23(FastEthernet0/23)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32779  (priority 32768 sys-id-ext 11)
             Address     000A.F382.ABD5
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/1            Desg FWD 19        128.1    P2p
Fa0/23           Root FWD 19        128.23   P2p
Fa0/24           Altn BLK 19        128.24   P2p
Switch1#show spanning-tree vlan 22
VLAN0022
  Spanning tree enabled protocol ieee
  Root ID    Priority    4118
             Address     000B.BE7B.8A54
             Cost        19
             Port        23(FastEthernet0/23)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32790  (priority 32768 sys-id-ext 22)
             Address     000A.F382.ABD5
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/2            Desg FWD 19        128.2    P2p
Fa0/23           Root FWD 19        128.23   P2p
Fa0/24           Altn BLK 19        128.24   P2p
Switch1#show spanning-tree vlan 88
VLAN0088
  Spanning tree enabled protocol ieee
  Root ID    Priority    4184
             Address     000B.BE7B.8A54
             Cost        19
             Port        23(FastEthernet0/23)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32856  (priority 32768 sys-id-ext 88)
             Address     000A.F382.ABD5
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Desg FWD 19        128.3    Shr
Fa0/23           Root FWD 19        128.23   P2p
Fa0/24           Altn BLK 19        128.24   P2p
Switch1#show spanning-tree vlan 99
VLAN0099
  Spanning tree enabled protocol ieee
  Root ID    Priority    4195
             Address     0010.1135.5876
             Cost        19
             Port        24(FastEthernet0/24)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32867  (priority 32768 sys-id-ext 99)
             Address     000A.F382.ABD5
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/23           Altn BLK 19        128.23   P2p
Fa0/24           Root FWD 19        128.24   P2p


Switch3#show spanning-tree vlan 11
VLAN0011
  Spanning tree enabled protocol ieee
  Root ID    Priority    4107
             Address     000B.BE7B.8A54
             This bridge is the root
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    4107  (priority 4096 sys-id-ext 11)
             Address     000B.BE7B.8A54
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po3              Desg FWD 9         128.27   Shr
Switch3#show spanning-tree vlan 22
VLAN0022
  Spanning tree enabled protocol ieee
  Root ID    Priority    4118
             Address     000B.BE7B.8A54
             This bridge is the root
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    4118  (priority 4096 sys-id-ext 22)
             Address     000B.BE7B.8A54
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po3              Desg FWD 9         128.27   Shr
Switch3#show spanning-tree vlan 88
VLAN0088
  Spanning tree enabled protocol ieee
  Root ID    Priority    4184
             Address     000B.BE7B.8A54
             This bridge is the root
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    4184  (priority 4096 sys-id-ext 88)
             Address     000B.BE7B.8A54
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po3              Desg FWD 9         128.27   Shr
Switch3#show spanning-tree vlan 99
VLAN0099
  Spanning tree enabled protocol ieee
  Root ID    Priority    4195
             Address     0010.1135.5876
             Cost        18
             Port        27(Port-channel3)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    8291  (priority 8192 sys-id-ext 99)
             Address     000B.BE7B.8A54
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po3              Root FWD 9         128.27   Shr


Switch4#show spanning-tree vlan 11
VLAN0011
  Spanning tree enabled protocol ieee
  Root ID    Priority    4107
             Address     000B.BE7B.8A54
             Cost        18
             Port        27(Port-channel4)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    8203  (priority 8192 sys-id-ext 11)
             Address     0010.1135.5876
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po4              Root FWD 9         128.27   Shr
Switch4#show spanning-tree vlan 22
VLAN0022
  Spanning tree enabled protocol ieee
  Root ID    Priority    4118
             Address     000B.BE7B.8A54
             Cost        18
             Port        27(Port-channel4)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    8214  (priority 8192 sys-id-ext 22)
             Address     0010.1135.5876
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po4              Root FWD 9         128.27   Shr
Switch4#show spanning-tree vlan 88
VLAN0088
  Spanning tree enabled protocol ieee
  Root ID    Priority    4184
             Address     000B.BE7B.8A54
             Cost        18
             Port        27(Port-channel4)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    8280  (priority 8192 sys-id-ext 88)
             Address     0010.1135.5876
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po4              Root FWD 9         128.27   Shr
Switch4#show spanning-tree vlan 99
VLAN0099
  Spanning tree enabled protocol ieee
  Root ID    Priority    4195
             Address     0010.1135.5876
             This bridge is the root
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    4195  (priority 4096 sys-id-ext 99)
             Address     0010.1135.5876
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/21           Desg FWD 19        128.21   P2p
Fa0/22           Desg FWD 19        128.22   P2p
Po4              Desg FWD 9         128.27   Shr


Switch99#show spanning-tree vlan 11
VLAN0011
  Spanning tree enabled protocol ieee
  Root ID    Priority    4107
             Address     000B.BE7B.8A54
             Cost        9
             Port        27(Port-channel3)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32779  (priority 32768 sys-id-ext 11)
             Address     0000.0C9D.951B
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Po3              Root FWD 9         128.27   Shr
Po4              Desg FWD 9         128.28   Shr
Switch99#show spanning-tree vlan 22
VLAN0022
  Spanning tree enabled protocol ieee
  Root ID    Priority    4118
             Address     000B.BE7B.8A54
             Cost        9
             Port        27(Port-channel3)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32790  (priority 32768 sys-id-ext 22)
             Address     0000.0C9D.951B
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Po3              Root FWD 9         128.27   Shr
Po4              Desg FWD 9         128.28   Shr
Switch99#show spanning-tree vlan 88
VLAN0088
  Spanning tree enabled protocol ieee
  Root ID    Priority    4184
             Address     000B.BE7B.8A54
             Cost        9
             Port        27(Port-channel3)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32856  (priority 32768 sys-id-ext 88)
             Address     0000.0C9D.951B
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Po3              Root FWD 9         128.27   Shr
Po4              Desg FWD 9         128.28   Shr
Switch99#show spanning-tree vlan 99
VLAN0099
  Spanning tree enabled protocol ieee
  Root ID    Priority    4195
             Address     0010.1135.5876
             Cost        9
             Port        28(Port-channel4)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  Bridge ID  Priority    32867  (priority 32768 sys-id-ext 99)
             Address     0000.0C9D.951B
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/1            Desg FWD 19        128.1    P2p
Fa0/2            Desg FWD 19        128.2    P2p
Po3              Desg FWD 9         128.27   Shr
Po4              Root FWD 9         128.28   Shr
```






 	





## **Part 2 – Virtual LANs.**

### ==Step 1 – VTP==

#### 1. **install the vtp** on ==all switches== and ==configure the trunk ports between switches==.

   Reference 2.Q5~Q6

```bash
Switch1(config)#vtp version 2
Switch1(config)#vtp domain must
Changing VTP domain name from NULL to must
Switch1(config)#vtp mode server
Device mode already VTP SERVER.
Switch1(config)#interface range FastEthernet 0/23-24
Switch1(config-if-range)#switchport trunk native vlan 1
Switch1(config-if-range)#switchport mode trunk
Switch1(config-if-range)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up
Switch1#show vtp status
VTP Version                     : 2
Configuration Revision          : 0
Maximum VLANs supported locally : 255
Number of existing VLANs        : 5
VTP Operating Mode              : Server
VTP Domain Name                 : must
VTP Pruning Mode                : Disabled
VTP V2 Mode                     : Enabled
VTP Traps Generation            : Disabled
MD5 digest                      : 0x60 0x59 0x49 0x60 0x35 0xAA 0x84 0x9C 
Configuration last modified by 0.0.0.0 at 3-1-93 00:01:32
Local updater ID is 0.0.0.0 (no valid interface found)


Switch2(config)#interface range FastEthernet 0/23-24
Switch2(config-if-range)#switchport trunk native vlan 1
Switch2(config-if-range)#switchport mode trunk
Switch2(config-if-range)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up
Switch2(config-if-range)#


Switch3(config)#interface range FastEthernet 0/21-24
Switch3(config-if-range)#switchport trunk encapsulation dot1q
Switch3(config-if-range)#switchport trunk native vlan 1
Switch3(config-if-range)#switchport mode trunk
Switch3(config-if-range)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up
Switch3(config-if-range)#


Switch4(config)#interface range FastEthernet 0/21-24
Switch4(config-if-range)#switchport trunk encapsulation dot1q
Switch4(config-if-range)#switchport trunk native vlan 1
Switch4(config-if-range)#switchport mode trunk
Switch4(config-if-range)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up
Switch4(config-if-range)#


Switch99(config)#interface range FastEthernet 0/21-24
Switch99(config-if-range)#switchport trunk native vlan 1
Switch99(config-if-range)#switchport mode trunk
```



### ==Step 2 – VLAN==

#### 2. create the new vlans on all switches. (==4 vlans for teachers, students, guests and servers.==)

Reference 2.Q11

```bash
Switch1(config)#vlan 11
Switch1(config-vlan)#name Teacher_VLAN_11
Switch1(config-vlan)#vlan 22
Switch1(config-vlan)#name Student_VLAN_22
Switch1(config-vlan)#vlan 88
Switch1(config-vlan)#name Wireless_VLAN_88
Switch1(config-vlan)#vlan 99
Switch1(config-vlan)#name Server_VLAN_99


Switch2(config)#vlan 11
Switch2(config-vlan)#name Teacher_VLAN_11
Switch2(config-vlan)#vlan 22
Switch2(config-vlan)#name Student_VLAN_22
Switch2(config-vlan)#vlan 88
Switch2(config-vlan)#name Wireless_VLAN_88
Switch2(config-vlan)#vlan 99
Switch2(config-vlan)#name Server_VLAN_99


Switch3(config)#vlan 11
Switch3(config-vlan)#name Teacher_VLAN_11
Switch3(config-vlan)#vlan 22
Switch3(config-vlan)#name Student_VLAN_22
Switch3(config-vlan)#vlan 88
Switch3(config-vlan)#name Wireless_VLAN_88
Switch3(config-vlan)#vlan 99
Switch3(config-vlan)#name Server_VLAN_99


Switch4(config)#vlan 11
Switch4(config-vlan)#name Teacher_VLAN_11
Switch4(config-vlan)#vlan 22
Switch4(config-vlan)#name Student_VLAN_22
Switch4(config-vlan)#vlan 88
Switch4(config-vlan)#name Wireless_VLAN_88
Switch4(config-vlan)#vlan 99
Switch4(config-vlan)#name Server_VLAN_99


Switch99(config)#vlan 11
Switch99(config-vlan)#name Teacher_VLAN_11
Switch99(config-vlan)#vlan 22
Switch99(config-vlan)#name Student_VLAN_22
Switch99(config-vlan)#vlan 88
Switch99(config-vlan)#name Wireless_VLAN_88
Switch99(config-vlan)#vlan 99
Switch99(config-vlan)#name Server_VLAN_99
```



#### 3. ==assign the access ports== to the new vlans on all access switches (==Switch1==, ==Switch2==, ==Switch99==)

Reference 2.Q18

```bash
Switch1(config)#interface FastEthernet 0/1
Switch1(config-if)#switchport mode access
Switch1(config-if)#switchport access vlan 11
Switch1(config-if)#interface FastEthernet 0/2
Switch1(config-if)#switchport mode access
Switch1(config-if)#switchport access vlan 22
Switch1(config-if)#interface FastEthernet 0/3
Switch1(config-if)#switchport mode access
Switch1(config-if)#switchport access vlan 88
Switch1#show vlan
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/4, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Gig0/1
                                                Gig0/2
11   Teacher_VLAN_11                  active    Fa0/1
22   Student_VLAN_22                  active    Fa0/2
88   Wireless_VLAN_88                 active    Fa0/3
99   Server_VLAN_99                   active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
11   enet  100011     1500  -      -      -        -    -        0      0


Switch2(config)#interface FastEthernet 0/1
Switch2(config-if)#switchport mode access
Switch2(config-if)#switchport access vlan 11
Switch2(config-if)#interface FastEthernet 0/2
Switch2(config-if)#switchport mode access
Switch2(config-if)#switchport access vlan 22
Switch2(config-if)#interface FastEthernet 0/3
Switch2(config-if)#switchport mode access
Switch2(config-if)#switchport access vlan 88
Switch2#show vlan
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/4, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Gig0/1
                                                Gig0/2
11   Teacher_VLAN_11                  active    Fa0/1
22   Student_VLAN_22                  active    Fa0/2
88   Wireless_VLAN_88                 active    Fa0/3
99   Server_VLAN_99                   active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
11   enet  100011     1500  -      -      -        -    -        0      0


Switch99(config)#interface FastEthernet 0/1
Switch99(config-if)#switchport mode access
Switch99(config-if)#switchport access vlan 99
Switch99(config-if)#interface FastEthernet 0/2
Switch99(config-if)#switchport mode access
Switch99(config-if)#switchport access vlan 99
Switch99(config-if)#interface FastEthernet 0/3
Switch99(config-if)#switchport mode access
Switch99(config-if)#switchport access vlan 99
Switch99#show vlan
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/4, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Gig0/1, Gig0/2
11   Teacher_VLAN_11                  active    
22   Student_VLAN_22                  active    
88   Wireless_VLAN_88                 active    
99   Server_VLAN_99                   active    Fa0/1, Fa0/2, Fa0/3
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
11   enet  100011     1500  -      -      -        -    -        0      0
22   enet  100022     1500  -      -      -        -    -        0      0

```



#### 4. ==configure the ip address on all PCs and servers==, and then ==test the connectivity of intra-vlan communication==.

- **configure the ip address on all PCs and servers**
  - Teacher-PC1
    - ![image-20230221170104983](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170104983.png)
  - Teacher-PC2
    - ![image-20230221170251398](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170251398.png)
  - Student-PC1
    - ![image-20230221170404721](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170404721.png)
  - Student-PC2
    - ![image-20230221170447278](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170447278.png)
  - Guest-Laptop1
    - ![image-20230221170632915](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170632915.png)
  - Guest-Laptop2
    - ![image-20230221170722571](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170722571.png)
    - Web-Server
      - ![image-20230221170823432](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170823432.png)
    - FTP-Server
      - ![image-20230221170915743](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221170915743.png)
  - test the connectivity of intra-vlan communication
    - Vlan 11
      - ![image-20230221171244000](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221171244000.png)
    - Vlan 22
      - ![image-20230221171341135](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221171341135.png)
    - Vlan 99
      - ![image-20230221171924771](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221171924771.png)

#### 5. enable the routing process, and ==configure the gateway of each vlan== in the distribution switches (Switch3, Switch4).

Reference 2.Q25-Q26

```bash
Switch3(config)#interface vlan 11
Switch3(config-if)#ip address 192.168.11.1 255.255.255.0
Switch3(config-if)#no shutdown
Switch3(config-if)#interface vlan 22
Switch3(config-if)#ip address 192.168.22.1 255.255.255.0
Switch3(config-if)#no shutdown
Switch3(config-if)#interface vlan 88
Switch3(config-if)#ip address 192.168.88.1 255.255.255.0
Switch3(config-if)#no shutdown
Switch3(config-if)#interface vlan 99
Switch3(config-if)#ip address 192.168.99.1 255.255.255.0
Switch3(config-if)#no shutdown
%LINK-5-CHANGED: Interface Vlan11, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan11, changed state to up
%LINK-5-CHANGED: Interface Vlan22, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan22, changed state to up
%LINK-5-CHANGED: Interface Vlan88, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan88, changed state to up
%LINK-5-CHANGED: Interface Vlan99, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan99, changed state to up
Switch3(config-if)#


Switch4(config)#interface vlan 11
Switch4(config-if)#ip address 192.168.11.2 255.255.255.0
Switch4(config-if)#no shutdown
Switch4(config-if)#interface vlan 22
Switch4(config-if)#ip address 192.168.22.2 255.255.255.0
Switch4(config-if)#no shutdown
Switch4(config-if)#interface vlan 88
Switch4(config-if)#ip address 192.168.88.2 255.255.255.0
Switch4(config-if)#no shutdown
Switch4(config-if)#interface vlan 99
Switch4(config-if)#ip address 192.168.99.2 255.255.255.0
Switch4(config-if)#no shutdown
%LINK-5-CHANGED: Interface Vlan11, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan11, changed state to up
%LINK-5-CHANGED: Interface Vlan22, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan22, changed state to up
%LINK-5-CHANGED: Interface Vlan88, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan88, changed state to up
%LINK-5-CHANGED: Interface Vlan99, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan99, changed state to up
Switch4(config-if)#
```



#### 6. ==configure the gateway== on all PCs and servers, and ==test the connectivity of inter-vlan communication==.

- configure the gateway on all PCs and servers
  - ![image-20230221183712635](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221183712635.png)
  - ![image-20230221183925377](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221183925377.png)
  - ![image-20230221184029710](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221184029710.png)
  - ![image-20230221184056334](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221184056334.png)
  - ![image-20230221184159789](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221184159789.png)
  - ![image-20230221184228765](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221184228765.png)
- test the connectivity of inter-vlan communication
  - vlan 11 -> vlan 22[Teacher-PC1->Student-PC1]
    - ![image-20230221184543515](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221184543515.png)
  - vlan 11 -> vlan 99[Teacher-PC1->Web-Server]
    - ![image-20230221184827225](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221184827225.png)
  - vlan 99 -> vlan 22[Web-Server->Student-PC1]
    - ![image-20230221184920416](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221184920416.png)



### ==Step 3 – Link Aggregation==

#### 7. ==configure the ether-channel== on the interfaces that connected to switches. 
(==interfaces between Switch3 and Switch99; interfaces between Switch4 and Switch99==)

Reference 2.Q30

```bash
Switch3(config)#interface range FastEthernet 0/23-24
Switch3(config-if-range)#channel-protocol lacp
Switch3(config-if-range)#channel-group 3 mode active
Switch3(config-if-range)#
Creating a port-channel interface Port-channel 3
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up
Switch3(config-if-range)#
Switch3#show etherchannel summary
Flags:  D - down        P - in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      f - failed to allocate aggregator
        u - unsuitable for bundling
        w - waiting to be aggregated
        d - default port
Number of channel-groups in use: 1
Number of aggregators:           1
Group  Port-channel  Protocol    Ports
------+-------------+-----------+----------------------------------------------
3      Po3(SU)           LACP   Fa0/23(P) Fa0/24(P) 


Switch4(config)#interface range FastEthernet 0/23-24
Switch4(config-if-range)#channel-protocol lacp
Switch4(config-if-range)#channel-group 4 mode active
Switch4(config-if-range)#
Creating a port-channel interface Port-channel 4
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up
Switch4(config-if-range)#
Switch4#show etherchannel summary
Flags:  D - down        P - in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      f - failed to allocate aggregator
        u - unsuitable for bundling
        w - waiting to be aggregated
        d - default port
Number of channel-groups in use: 1
Number of aggregators:           1
Group  Port-channel  Protocol    Ports
------+-------------+-----------+----------------------------------------------
4      Po4(SU)           LACP   Fa0/23(P) Fa0/24(P) 


Switch99(config)#interface range FastEthernet 0/21-22
Switch99(config-if-range)#channel-protocol lacp
Switch99(config-if-range)#channel-group 3 mode active
Switch99(config-if-range)#interface range FastEthernet 0/23-24
Switch99(config-if-range)#channel-protocol lacp
Switch99(config-if-range)#channel-group 4 mode active
Creating a port-channel interface Port-channel 3
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/21, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/21, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/22, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/22, changed state to up
%LINK-5-CHANGED: Interface Port-channel3, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Port-channel3, changed state to up
Switch99(config-if-range)#
Creating a port-channel interface Port-channel 4
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up
%LINK-5-CHANGED: Interface Port-channel4, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Port-channel4, changed state to up
Switch99(config-if-range)#
Switch99#show etherchannel summary
Flags:  D - down        P - in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      f - failed to allocate aggregator
        u - unsuitable for bundling
        w - waiting to be aggregated
        d - default port
Number of channel-groups in use: 2
Number of aggregators:           2
Group  Port-channel  Protocol    Ports
------+-------------+-----------+----------------------------------------------
3      Po3(SU)           LACP   Fa0/21(P) Fa0/22(P) 
4      Po4(SU)           LACP   Fa0/23(P) Fa0/24(P)
```





### ==Step 4 – Redundant Gateway== 

#### 8. ==configure the active gateway== and ==standby gateway== for each vlan on the distribution switches (Switch3, Switch4).

Reference 2.Q35

```bash
Switch3(config)#interface vlan 11
Switch3(config-if)#standby 11 ip 192.168.11.254
Switch3(config-if)#standby 11 priority 101
Switch3(config-if)#standby 11 preempt
Switch3(config-if)#interface vlan 22
Switch3(config-if)#standby 22 ip 192.168.22.254
Switch3(config-if)#standby 22 priority 101
Switch3(config-if)#standby 22 preempt
Switch3(config-if)#interface vlan 88
Switch3(config-if)#standby 88 ip 192.168.88.254
Switch3(config-if)#standby 88 priority 101
Switch3(config-if)#standby 88 preempt
Switch3(config-if)#interface vlan 99
Switch3(config-if)#standby 99 ip 192.168.99.254
Switch3(config-if)#standby 99 priority 99
Switch3(config-if)#standby 99 preempt
Switch3(config-if)#
%HSRP-6-STATECHANGE: Vlan11 Grp 11 state Speak -> Standby
%HSRP-6-STATECHANGE: Vlan11 Grp 11 state Standby -> Active
%HSRP-6-STATECHANGE: Vlan99 Grp 99 state Speak -> Standby
%HSRP-6-STATECHANGE: Vlan99 Grp 99 state Standby -> Active
%HSRP-6-STATECHANGE: Vlan88 Grp 88 state Speak -> Standby
%HSRP-6-STATECHANGE: Vlan88 Grp 88 state Standby -> Active
%HSRP-6-STATECHANGE: Vlan22 Grp 22 state Speak -> Standby
%HSRP-6-STATECHANGE: Vlan22 Grp 22 state Standby -> Active
Switch3(config-if)#
Switch3#show standby brief
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State    Active          Standby         Virtual IP
Vl11        11   101 P Active   local           192.168.11.2    192.168.11.254 
Vl22        22   101 P Active   local           192.168.22.2    192.168.22.254 
Vl88        88   101 P Active   local           192.168.88.2    192.168.88.254 
Vl99        99   99  P Standby  192.168.99.2    local           192.168.99.254
Switch3#


Switch4(config)#interface vlan 11
Switch4(config-if)#standby 11 ip 192.168.11.254
Switch4(config-if)#standby 11 priority 99
Switch4(config-if)#standby 11 preempt
Switch4(config-if)#interface vlan 22
Switch4(config-if)#standby 22 ip 192.168.22.254
Switch4(config-if)#standby 22 priority 99
Switch4(config-if)#standby 22 preempt
Switch4(config-if)#interface vlan 88
Switch4(config-if)#standby 88 ip 192.168.88.254
Switch4(config-if)#standby 88 priority 99
Switch4(config-if)#standby 88 preempt
Switch4(config-if)#interface vlan 99
Switch4(config-if)#standby 99 ip 192.168.99.254
Switch4(config-if)#standby 99 priority 101
Switch4(config-if)#standby 99 preempt
Switch4(config-if)#
%HSRP-6-STATECHANGE: Vlan99 Grp 99 state Standby -> Active
%HSRP-6-STATECHANGE: Vlan22 Grp 22 state Speak -> Standby
%HSRP-6-STATECHANGE: Vlan11 Grp 11 state Speak -> Standby
%HSRP-6-STATECHANGE: Vlan88 Grp 88 state Speak -> Standby
Switch4#show standby brief
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State    Active          Standby         Virtual IP
Vl11        11   99  P Standby  192.168.11.1    local           192.168.11.254 
Vl22        22   99  P Standby  192.168.22.1    local           192.168.22.254 
Vl88        88   99  P Standby  192.168.88.1    local           192.168.88.254 
Vl99        99   101 P Active   local           192.168.99.2    192.168.99.254 
```

#### 9. ==configure the virtual gateway== on all ==PCs and servers==, and ==trace the path between the PCs/servers and the active gateway==.

- configure the virtual gateway on all PCs and servers

  - ![image-20230221193823951](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221193823951.png)

  - ![image-20230221223051611](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221223051611.png)
  - ![image-20230221223137945](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221223137945.png)
  - ![image-20230221223200827](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221223200827.png)
  - ![image-20230221223235108](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221223235108.png)
  - ![image-20230221223257812](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230221223257812.png)

- trace the path between the PCs/servers and the active gateway

  - vlan 11 -> vlan 99[Teacher-PC1->Web-Server]

    - ![image-20230222155417370](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230222155417370.png)
  

    ```bash
    C:\>tracert 192.168.99.101
    Tracing route to 192.168.99.101 over a maximum of 30 hops: 
      1   0 ms      0 ms      0 ms      192.168.11.1
      2   0 ms      0 ms      0 ms      192.168.99.101
    Trace complete.
    ```
  
  - vlan 11 -> vlan 22[Teacher-PC2->Student-PC1]
  
    - ![image-20230222155417370](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230222155417370.png)

  
    ```bash
    C:\>tracert 192.168.22.101
    Tracing route to 192.168.22.101 over a maximum of 30 hops: 
      1   0 ms      0 ms      0 ms      192.168.11.1
      2   0 ms      0 ms      0 ms      192.168.22.101
    Trace complete.
    ```

  - vlan 22 -> vlan 99[Student-PC1->Web-Server]
  
    - ![image-20230223133333031](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223133333031.png)

  
    ```bash
    C:\>tracert 192.168.99.101
    Tracing route to 192.168.99.101 over a maximum of 30 hops: 
      1   0 ms      0 ms      0 ms      192.168.22.1
      2   0 ms      0 ms      0 ms      192.168.99.101
    Trace complete.
    ```



 

## **Part 3 – Wireless LANs.**

### ==Step 6 – Wireless AP==

#### 11. ==configure the wireless== access point using WPA2 PSK.

Reference 3.Q22-Q27

- <img src="/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223132553532.png" alt="image-20230223132553532" style="zoom: 80%;" />
- <img src="/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223132703209.png" alt="image-20230223132703209" style="zoom:80%;" />

#### 12. ==connect the wireless== clients to the access point.

- <img src="/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223132440144.png" alt="image-20230223132440144" style="zoom:50%;" /> <img src="/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223132411459.png" alt="image-20230223132411459" style="zoom:50%;" />
- <img src="/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223132801838.png" alt="image-20230223132801838" style="zoom:50%;" /> <img src="/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223132831237.png" alt="image-20230223132831237" style="zoom:50%;" />
- ![image-20230223132930955](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223132930955.png)

#### 13. ==configure the ip address and gateway on all laptops==, and then ==test the connectivity of wireless connection==.

- configure the ip address and gateway on all laptops

  - ![image-20230223135342930](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223135342930.png)

  - ![image-20230223135451185](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223135451185.png)

- test the connectivity of wireless connection

  - Guest-Laptop1->Guest-Laptop2

    ![image-20230223135634794](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223135634794.png)

  - Guest-Laptop1->Web-Server

    ![image-20230223135854316](/home/qingbolan/snap/typora/76/.config/Typora/typora-user-images/image-20230223135854316.png)