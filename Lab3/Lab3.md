# **Lab 3.WANs Technology**



#### ==**Objective**==

- Understand the WANs Technologies, including dedicated, circuit-switched and packet-switched networks.

#### ==**Topology**==

![image-20230409191300367](assets/image-20230409191300367.png)



#### ==**Address Scheme**==

##### ==**Inside:**==

![image-20230409191333772](assets/image-20230409191333772.png)

![image-20230409191352891](assets/image-20230409191352891.png)

==**Outside:**==

![image-20230409191434980](assets/image-20230409191434980.png)

==**Translation:**==

![image-20230409191531417](assets/image-20230409191531417.png)

## **Part 1 – Dedicated Network.**

>  Requirement:
>
> - 1.1 Gateway-Router -> Internet-PC using Enterprise DSL
>
> - 1.2 DSL-PC -> Internet-PC using Personal DSL

### ==Step 1 – Enterprise DSL==

#### 1. configure the DSL on the provider’s site (e.g. ISP-Router)

Reference 5.Q5

```bash
ISP-Router(config)#interface FastEthernet 1/0
ISP-Router(config-if)#ip address 201.201.201.1 255.255.255.0
ISP-Router(config-if)#pppoe enable
ISP-Router(config-if)#no shutdown

ISP-Router(config-if)#no ip route 200.200.123.0 255.255.255.248 200.200.200.2
ISP-Router(config)#ip route 200.200.123.0 255.255.255.248 201.201.201.2
%LINK-5-CHANGED: Interface Virtual-Access1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Virtual-Access1, changed state to up
```

![image-20230409192024472](assets/image-20230409192024472.png)

#### 2. configure the DSL on the subscriber’s site. (e.g. Gateway-Router1)

Reference 5.Q13

```bash
Gateway-Router1(config)#interface FastEthernet 1/0
Gateway-Router1(config-if)#ip address 201.201.201.2 255.255.255.0
Gateway-Router1(config-if)#pppoe enable
Gateway-Router1(config-if)#no shutdown

Gateway-Router1(config-if)#no ip route 0.0.0.0 0.0.0.0 200.200.200.1
Gateway-Router1(config)#ip route 0.0.0.0 0.0.0.0 201.201.201.1
%LINK-5-CHANGED: Interface Virtual-Access1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Virtual-Access1, changed state to up
```

![image-20230409211957522](assets/image-20230409211957522.png)

#### 3. test the connectivity of the DSL connection.

- From **Gateway-Router1** to **Internet-PC**

```bash
Gateway-Router1#ping 1.2.3.4

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.2.3.4, timeout is 2 seconds:
..!!!
Success rate is 60 percent (3/5), round-trip min/avg/max = 42/49/60 ms
```

- From **Teacher-PC1** to **Internet-PC**

![image-20230409212344380](assets/image-20230409212344380.png)



### ==Step 2 – Personal DSL==

#### 4. configure the DSL on the provider’s site (e.g. ISP-Router)

Reference 5.Q1~5

![image-20230409212542773](assets/image-20230409212542773.png)

```bash
ISP-Router(config)#ip local pool Personal-PPPoEPool 201.201.201.101 201.201.201.199

ISP-Router(config)#interface Virtual-Template 1
ISP-Router(config-if)#ip unnumbered FastEthernet 1/0
ISP-Router(config-if)#peer default ip address pool Personal-PPPoEPool

ISP-Router(config-if)#ppp authentication chap callin
AAA: Warning, authentication list callin is not defined for PPP.
ISP-Router(config-if)#exit

ISP-Router(config)#username DSL-User password Hello

ISP-Router(config)#bba-group pppoe MyGroup
ISP-Router(config-bba)#virtual-template 1

ISP-Router(config-bba)#interface FastEthernet 1/0
ISP-Router(config-if)#pppoe enable group MyGroup
```



#### 5. configure the DSL on the subscriber’s site. (e.g. DSL-PC)

Reference 5.Q7~11


#### 6. test the connectivity of the DSL connection.

 

## **Part 2 – Circuit-switched Network.**

> Requirement:
> 2.1 Dialup-PC -> Internet-PC using analog dialup
> 2.2 Dialup-PC -> Teacher-PC/Student-PC/Servers using analog dialup


### Step 3 – Analog dialup

#### 7. configure analog dialup on the provider’s site (e.g. ISP-Router)

Reference 6.Q1~3




#### 8. configure analog dialup on the campus’s site (e.g. Gateway-Router1)
Reference 6.Q10~12


#### 9. configure analog dialup on the subscriber’ site (e.g. Dialup-PC)
Reference 6.Q5~9; Q14~18


#### 10. test the connectivity of the analog dialup connection.


## **Part 3 – Packet-switched Network.**
> Requirement:
> 3.1 Branch-PC -> Teacher-PC/Student-PC/Servers using Frame Relay
> 3.2 Branch-PC -> Internet-PC


### Step 4 – Frame Relay

#### 11. configure frame relay on all site (including Gateway-Router1~3~4)
Reference 7.Q1,2,5,6,12~14

 

### Step 5 – Routing
#### 12. configure the routing information, dhcp, and nat, so that all PCs can ping each other.

#### 13. test the connectivity of the frame relay connection.
